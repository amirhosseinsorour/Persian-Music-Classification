# Reproduction notes

## Status and provenance

The initial repository package contains the 31 notebooks supplied in `CODE.zip`. Each file is copied without changing its source, outputs, or metadata. Folder names and filenames are retained beneath `notebooks/` so they can be matched to the original project inventory.

The review covered notebook structure, imports, data loading, model definitions, saved outputs, and the original thesis text. No notebook was executed, no model was retrained, and no accuracy result was independently reproduced. Audio files, feature pickles, split manifests, and saved model files were not included in the code archive.

## Inputs required by the original notebooks

| Notebook group | External inputs |
| --- | --- |
| Initial preprocessing | Nava audio recordings under `NavaDataset/Data` |
| Encoder/decoder and alpha experiments | `DATA_MFCC30_MEL128.pkl` |
| FFT-window experiments | Matching `DATA_NFFT{window}_HOP{hop}.pkl` files |
| Refined preprocessing | Audio recordings plus `all_train.txt`, `test.txt`, and `dev.txt` |
| Refined training notebooks | `FINAL_DATA_TRAIN.pkl`, `FINAL_DATA_TEST.pkl`, and `FINAL_DATA_DEV.pkl` |
| Initial evaluation report | A saved model and `DATA_MFCC30_MEL128.pkl` |
| Refined evaluation report | A saved model and `FINAL_DATA_MFCC_MEL_TEST.pkl` |

These are the filenames referenced by the archived source. Their presence or mutual compatibility has not been verified. In particular, the refined report's test-feature filename differs from the refined preprocessing output filename.

## Environment and paths

The notebooks mount Drive at `/content/drive` and reference paths beneath `/content/drive/MyDrive/AUT/Project/` and `/content/drive/MyDrive/NavaDataset/`. These paths belong to the original workflow and must be updated for another user's storage.

`requirements.txt` lists dependency names found in the source. It deliberately does not invent version pins for the original environment. The notebooks mix `tensorflow.keras` and standalone `keras` imports; a current installation may require API and saved-model compatibility work. See the [Keras installation and legacy-version guidance](https://keras.io/getting_started/).

The evaluation notebooks also contain Persian plotting/font examples. Their local font paths and demonstration cells are separate from the model's numerical evaluation.

## Source issues to resolve before execution

### Initial preprocessing

In `Process&Evaluation/Preprocess.ipynb`, the `DATA` feature dictionary is used without an initialization in the supplied code cells. In addition, the line that computes `mel_spectrogram` is commented out, while the variable is subsequently used in feature storage. Both need to be addressed before a fresh execution of this notebook.

The preprocessing code assumes audio files can be loaded directly from the configured dataset directory and infers class labels from filename positions. The actual dataset layout and label encoding must be checked against those assumptions.

### Refined preprocessing

`Refinements/Ref -- Preprocess.ipynb` assigns tracks to partitions using the supplied split manifests, then segments the audio. It defaults unrecognized tracks to the training partition. Before using it as a benchmark pipeline, verify that the three manifests are disjoint, cover the intended recordings, and use filenames matching the audio files.

Its last inspection cell references `DATA`, although its defined dictionaries are `DATA_TRAIN`, `DATA_TEST`, and `DATA_DEV`.

### Refined combined-feature model

In `Refinements/Ref -- Conv1D-MFCCs_Conv2D-MEL_EN-LSTM_DE-GRU.ipynb`:

- `sk_shuffle` is used without a corresponding import in the supplied notebook.
- `load_data()` returns nine arrays, while its caller expects six objects.
- The data loader reads MFCC features without assembling the Mel-spectrogram input expected by the two-input model.

Its retained outputs therefore cannot establish that the current saved source runs from a fresh kernel. The notebook should be reconciled with the intended final workflow before it is presented as the canonical executable version.

### Evaluation reports

Both report notebooks call `classification_report` with predictions first and ground truth second. The [documented argument order](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.classification_report.html) is ground truth followed by predictions. This affects interpretation of per-class precision, recall, and support; it is separate from the confusion-matrix calls, which use ground truth first.

The refined report loads a model path whose name identifies a GRU encoder / LSTM decoder. Confirm the intended saved model before associating its output with the LSTM encoder / GRU decoder architecture in the thesis abstract.

The notebooks contain `!pip install PIL`; the dependency to install is [Pillow](https://pillow.readthedocs.io/en/stable/installation/basic-installation.html), already named in `requirements.txt`. An old ImportError output is retained in the initial report notebook.

## Experimental interpretation

### Loss scaling

The alpha notebooks set the instrument loss weight to `alpha * 4.7` and the Dastgah loss weight to `alpha`. Changing alpha scales both task losses while keeping their 4.7:1 ratio fixed. These notebooks should be described as joint-loss scaling experiments, rather than experiments that change the relative importance of the tasks. The shared model also contains regularization terms.

### Dataset partitioning

The earlier experiment notebooks randomly split extracted feature segments. That procedure does not, by itself, establish that recordings or performers are independent across train, validation, and test partitions. The refined preprocessing uses recording-name manifests, whose contents were not supplied. Any claim of recording-independent or performer-independent performance requires checking the corresponding manifests and evaluation procedure.

### Plot labels

Some learning-curve legends use the word "Test" for values taken from Keras history keys beginning with `val_`. Those curves correspond to validation data passed to `model.fit`; the later `model.evaluate` call is a separate evaluation.

### Reported and saved results

The README's 98.9% instrument accuracy and 94.07% Dastgah accuracy are the thesis abstract's reported results. Saved outputs in the archive vary across notebook revisions. Some outputs match across notebooks whose current source differs, so saved outputs should be treated as historical records until source, data partitions, and model artifacts are reconciled.

## Suggested next development step

Choose one preprocessing/training/evaluation workflow and make its paths and inputs explicit. Resolve the issues above for that workflow, preserve the original notebooks as a reference, record an environment that actually runs, and then reproduce a held-out evaluation. Record fresh results separately from the thesis-reported values.
