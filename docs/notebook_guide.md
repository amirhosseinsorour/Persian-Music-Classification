# Notebook guide

All paths below are relative to `notebooks/`. The 31 original notebooks are preserved without renaming or editing their contents.

## Suggested reading order

1. Read `Process&Evaluation/Preprocess.ipynb` to understand the feature-extraction approach, alongside the source corrections in [reproduction notes](reproduction_notes.md).
2. Read `EN-DE_DIFF/Conv1D-MFCCs_Conv2D-MEL_EN-LSTM_DE-GRU.ipynb` for the combined MFCC/Mel model architecture and training workflow.
3. Compare the other encoder/decoder notebooks and the FFT-window experiments.
4. Examine the alpha experiments for joint-loss scaling at a fixed ratio of task weights.
5. Read the report notebooks for the evaluation workflow and `Refinements/` for later revisions.

This is a reading order. A fresh execution needs external data, compatible dependencies, path changes, and the source corrections described in the reproduction notes. The `Refinements` folder name alone does not establish which notebook is the final reproducible version.

## Complete inventory

### Feature extraction and evaluation
Original folder: `Process&Evaluation` · 3 notebooks.
| Notebook | Purpose |
| --- | --- |
| [Histogram_Test.ipynb](../notebooks/Process%26Evaluation/Histogram_Test.ipynb) | Inspect the distribution of class labels |
| [Preprocess.ipynb](../notebooks/Process%26Evaluation/Preprocess.ipynb) | Extract MFCC-based features and Mel spectrograms |
| [Report.ipynb](../notebooks/Process%26Evaluation/Report.ipynb) | Load a saved model and generate classification reports and confusion matrices |

### FFT-window experiments
Original folder: `NFFT_DIFF` · 8 notebooks.
| Notebook | Purpose |
| --- | --- |
| [Conv1D_MFCCs_1024.ipynb](../notebooks/NFFT_DIFF/Conv1D_MFCCs_1024.ipynb) | MFCC-based model with N_FFT = 1024 |
| [Conv1D_MFCCs_16384.ipynb](../notebooks/NFFT_DIFF/Conv1D_MFCCs_16384.ipynb) | MFCC-based model with N_FFT = 16384 |
| [Conv1D_MFCCs_2048.ipynb](../notebooks/NFFT_DIFF/Conv1D_MFCCs_2048.ipynb) | MFCC-based model with N_FFT = 2048 |
| [Conv1D_MFCCs_32768.ipynb](../notebooks/NFFT_DIFF/Conv1D_MFCCs_32768.ipynb) | MFCC-based model with N_FFT = 32768 |
| [Conv1D_MFCCs_4096.ipynb](../notebooks/NFFT_DIFF/Conv1D_MFCCs_4096.ipynb) | MFCC-based model with N_FFT = 4096 |
| [Conv1D_MFCCs_65536.ipynb](../notebooks/NFFT_DIFF/Conv1D_MFCCs_65536.ipynb) | MFCC-based model with N_FFT = 65536 |
| [Conv1D_MFCCs_8192.ipynb](../notebooks/NFFT_DIFF/Conv1D_MFCCs_8192.ipynb) | MFCC-based model with N_FFT = 8192 |
| [plot_fig.ipynb](../notebooks/NFFT_DIFF/plot_fig.ipynb) | Plot the FFT-window comparison |

### Encoder/decoder architecture experiments
Original folder: `EN-DE_DIFF` · 5 notebooks.
| Notebook | Purpose |
| --- | --- |
| [Conv1D-MFCCs_Conv2D-MEL_!RNN.ipynb](../notebooks/EN-DE_DIFF/Conv1D-MFCCs_Conv2D-MEL_%21RNN.ipynb) | Combined MFCC/Mel model without recurrent layers |
| [Conv1D-MFCCs_Conv2D-MEL_EN-GRU_DE-GRU.ipynb](../notebooks/EN-DE_DIFF/Conv1D-MFCCs_Conv2D-MEL_EN-GRU_DE-GRU.ipynb) | Combined MFCC/Mel model: GRU encoder / GRU decoder |
| [Conv1D-MFCCs_Conv2D-MEL_EN-GRU_DE-LSTM.ipynb](../notebooks/EN-DE_DIFF/Conv1D-MFCCs_Conv2D-MEL_EN-GRU_DE-LSTM.ipynb) | Combined MFCC/Mel model: GRU encoder / LSTM decoder |
| [Conv1D-MFCCs_Conv2D-MEL_EN-LSTM_DE-GRU.ipynb](../notebooks/EN-DE_DIFF/Conv1D-MFCCs_Conv2D-MEL_EN-LSTM_DE-GRU.ipynb) | Combined MFCC/Mel model: LSTM encoder / GRU decoder |
| [Conv1D-MFCCs_Conv2D-MEL_EN-LSTM_DE-LSTM.ipynb](../notebooks/EN-DE_DIFF/Conv1D-MFCCs_Conv2D-MEL_EN-LSTM_DE-LSTM.ipynb) | Combined MFCC/Mel model: LSTM encoder / LSTM decoder |

### Joint-loss scaling experiments
Original folder: `ALPHA_DIFF` · 8 notebooks.
| Notebook | Purpose |
| --- | --- |
| [Conv1D-MFCCs_Conv2D-MEL_EN-LSTM_DE-GRU_ALPHA0.1.ipynb](../notebooks/ALPHA_DIFF/Conv1D-MFCCs_Conv2D-MEL_EN-LSTM_DE-GRU_ALPHA0.1.ipynb) | Joint-loss scale alpha = 0.1 (task-weight ratio fixed at 4.7:1) |
| [Conv1D-MFCCs_Conv2D-MEL_EN-LSTM_DE-GRU_ALPHA0.3.ipynb](../notebooks/ALPHA_DIFF/Conv1D-MFCCs_Conv2D-MEL_EN-LSTM_DE-GRU_ALPHA0.3.ipynb) | Joint-loss scale alpha = 0.3 (task-weight ratio fixed at 4.7:1) |
| [Conv1D-MFCCs_Conv2D-MEL_EN-LSTM_DE-GRU_ALPHA0.5.ipynb](../notebooks/ALPHA_DIFF/Conv1D-MFCCs_Conv2D-MEL_EN-LSTM_DE-GRU_ALPHA0.5.ipynb) | Joint-loss scale alpha = 0.5 (task-weight ratio fixed at 4.7:1) |
| [Conv1D-MFCCs_Conv2D-MEL_EN-LSTM_DE-GRU_ALPHA0.8.ipynb](../notebooks/ALPHA_DIFF/Conv1D-MFCCs_Conv2D-MEL_EN-LSTM_DE-GRU_ALPHA0.8.ipynb) | Joint-loss scale alpha = 0.8 (task-weight ratio fixed at 4.7:1) |
| [Conv1D-MFCCs_Conv2D-MEL_EN-LSTM_DE-GRU_ALPHA1.ipynb](../notebooks/ALPHA_DIFF/Conv1D-MFCCs_Conv2D-MEL_EN-LSTM_DE-GRU_ALPHA1.ipynb) | Joint-loss scale alpha = 1 (task-weight ratio fixed at 4.7:1) |
| [Conv1D-MFCCs_Conv2D-MEL_EN-LSTM_DE-GRU_ALPHA2.ipynb](../notebooks/ALPHA_DIFF/Conv1D-MFCCs_Conv2D-MEL_EN-LSTM_DE-GRU_ALPHA2.ipynb) | Joint-loss scale alpha = 2 (task-weight ratio fixed at 4.7:1) |
| [Conv1D-MFCCs_Conv2D-MEL_EN-LSTM_DE-GRU_ALPHA3.ipynb](../notebooks/ALPHA_DIFF/Conv1D-MFCCs_Conv2D-MEL_EN-LSTM_DE-GRU_ALPHA3.ipynb) | Joint-loss scale alpha = 3 (task-weight ratio fixed at 4.7:1) |
| [plot.ipynb](../notebooks/ALPHA_DIFF/plot.ipynb) | Plot the saved comparison series |

### Later preprocessing and model revisions
Original folder: `Refinements` · 7 notebooks.
| Notebook | Purpose |
| --- | --- |
| [Ref -- Conv1D-MFCCs_Conv2D-MEL_EN-LSTM_DE-GRU.ipynb](../notebooks/Refinements/Ref%20--%20Conv1D-MFCCs_Conv2D-MEL_EN-LSTM_DE-GRU.ipynb) | Combined MFCC/Mel model revision; data-loader changes are incomplete |
| [Ref -- Conv1D_MFCCs_4096 - !AutoEncoder.ipynb](../notebooks/Refinements/Ref%20--%20Conv1D_MFCCs_4096%20-%20%21AutoEncoder.ipynb) | MFCC model variant without the encoder/decoder structure |
| [Ref -- Conv1D_MFCCs_4096 - !DeltaMFCC.ipynb](../notebooks/Refinements/Ref%20--%20Conv1D_MFCCs_4096%20-%20%21DeltaMFCC.ipynb) | MFCC model variant without delta-MFCC features |
| [Ref -- Conv1D_MFCCs_4096.ipynb](../notebooks/Refinements/Ref%20--%20Conv1D_MFCCs_4096.ipynb) | MFCC-based model revision |
| [Ref -- Histogram_Test.ipynb](../notebooks/Refinements/Ref%20--%20Histogram_Test.ipynb) | Inspect the distribution of class labels |
| [Ref -- Preprocess.ipynb](../notebooks/Refinements/Ref%20--%20Preprocess.ipynb) | Extract MFCC-based features and Mel spectrograms using track split lists |
| [Ref -- Report.ipynb](../notebooks/Refinements/Ref%20--%20Report.ipynb) | Load a saved model and generate classification reports and confusion matrices |

## Naming conventions

`NFFT` refers to the FFT window size. `MFCCs` refers to Mel-frequency cepstral coefficients. `MEL` refers to Mel-spectrogram features. `EN` and `DE` identify encoder and decoder choices. A leading `!` in an original filename denotes an ablation or removed component.
