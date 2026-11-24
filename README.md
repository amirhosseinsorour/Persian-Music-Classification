# Instrument and Scale (Dastgah) Recognition in Persian Traditional Music

**BSc thesis · Amirkabir University of Technology · 2023**

Automatic recognition of musical instruments and Dastgahs in Persian traditional music using audio features and multi-task deep learning.

The project brings together music information retrieval, signal processing, neural-network modelling, and comparative experiments. A recording is classified by its instrument and its Dastgah, the modal framework used in Persian traditional music.

This repository preserves the original research notebooks, including their saved outputs. The original dataset, extracted features, and trained model files are external to this repository. The notebooks have been inspected as source; training and evaluation have not been reproduced in a fresh environment.

## Project at a glance

| Item | Description |
| --- | --- |
| Tasks | Instrument recognition and Dastgah recognition |
| Dataset | Nava Persian traditional music dataset |
| Dataset scope described in the thesis | 1,785 recordings, approximately 55 hours, and 40 performers |
| Instrument classes | Tar, Kamancheh, Santoor, Setar, and Ney |
| Dastgah classes | Shur, Segah, Mahur, Homayoun, Rastpanjgah, Nava, and Chahargah |
| Tools | Python, TensorFlow/Keras, librosa, NumPy, scikit-learn, Matplotlib, and Google Colab |

The dataset is credited to its original authors; it was used for the thesis rather than created as part of this project.

## Approach

The audio-processing pipeline uses 20-second segments sampled at 22,050 Hz. In the combined-feature configuration, each segment is represented by 30 MFCCs and their first and second derivatives, together with a 128-band log-Mel spectrogram. The corresponding preprocessing configuration uses an FFT window of 4,096 samples and a hop length of 2,048 samples.

The combined-feature architecture contains:

1. A residual Conv1D branch for MFCC-based features.
2. A residual Conv2D branch for log-Mel spectrograms.
3. Feature concatenation followed by a bidirectional recurrent encoder and decoder.
4. Separate softmax outputs for the five instruments and seven Dastgahs.

The experiments compare FFT window sizes, recurrent encoder/decoder combinations, joint-loss scaling, and later preprocessing and model refinements.

## Results reported in the thesis

| Task | Reported test accuracy |
| --- | ---: |
| Instrument recognition | 98.9% |
| Dastgah recognition | 94.07% |

These values are taken from the original thesis abstract. The saved notebook outputs include other experiment runs and revisions, with differing scores. They have not been reconciled into a newly reproduced benchmark. See the [reproduction notes](docs/reproduction_notes.md) before interpreting or comparing results.

## Explore the notebooks

| Folder | Notebooks | Purpose |
| --- | ---: | --- |
| [Process&Evaluation](notebooks/Process%26Evaluation/) | 3 | Feature extraction, label histograms, and evaluation reporting |
| [NFFT_DIFF](notebooks/NFFT_DIFF/) | 8 | Seven FFT-window experiments and a comparison plot notebook |
| [EN-DE_DIFF](notebooks/EN-DE_DIFF/) | 5 | Recurrent encoder/decoder comparisons, including a configuration without recurrent layers |
| [ALPHA_DIFF](notebooks/ALPHA_DIFF/) | 8 | Seven joint-loss scaling experiments and a comparison plot notebook |
| [Refinements](notebooks/Refinements/) | 7 | Later preprocessing, model, ablation, and evaluation revisions |

All 31 notebook files retain their original names and contents. A complete file index and suggested reading order are in the [notebook guide](docs/notebook_guide.md).

For the combined MFCC/Mel architecture, start by reading the [LSTM-encoder / GRU-decoder experiment](notebooks/EN-DE_DIFF/Conv1D-MFCCs_Conv2D-MEL_EN-LSTM_DE-GRU.ipynb). This is a useful source-code entry point; selecting a canonical final training notebook requires reconciling the later revisions with the thesis.

## Working with the project

The notebooks were developed for Google Colab and mount Google Drive. Read the [reproduction notes](docs/reproduction_notes.md) for their input files, path settings, and known source issues.

To prepare a local Python environment:

```bash
python -m venv .venv
```

Activate it on Windows PowerShell:

```powershell
.\.venv\Scripts\Activate.ps1
```

Or on macOS/Linux:

```bash
source .venv/bin/activate
```

Then install the dependency list:

```bash
python -m pip install -r requirements.txt
```

The dependency list is based on imports in the notebooks. The original package versions were not supplied, so it does not establish a tested, reproducible environment. The Google Drive mounting cells require Colab; running locally also requires replacing those cells and updating file paths. Execution additionally depends on the external data and the source corrections documented in the reproduction notes.

## Data and supporting materials

The source notebooks expect audio recordings, extracted feature pickles, and, for evaluation, saved models. None of these files were included with the notebook archive.

The thesis cites the dataset as:

> Baba Ali, B., Gorgan Mohammadi, A., and Faraji Dizaji, A. (2019). Nava: A Persian Traditional Music Database for the Dastgah and Instrument Recognition Tasks. Advanced Signal Processing, 3(2), 125–134.

This bibliographic entry follows the thesis reference list.

## Academic information

**Author:** [Amirhossein Sorour](https://github.com/amirhosseinsorour)  
**Supervisor:** Dr. Mohammad Mehdi Homayounpour  
**Institution:** Amirkabir University of Technology, Department of Computer Engineering  
**Degree:** BSc in Computer Engineering  
**Original thesis title:** Automatic Detection of Instrument and Scale (Dastgah) for Persian Traditional Music
