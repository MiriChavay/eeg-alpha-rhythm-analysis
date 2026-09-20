# EEG Alpha Rhythm: Eyes-Open vs. Eyes-Closed Analysis

A signal-processing exploration of the classic **alpha-blocking (Berger)
effect** in EEG - the well-documented jump in occipital alpha-band
(8-12 Hz) power when someone closes their eyes - using recordings from
3 participants (POz electrode, 1024 Hz, 40s per condition).

## Pipeline

1. **Load & visualize** the raw EO/EC signals for all three participants
2. **Band-pass filter** (2-40 Hz, Butterworth) to remove drift and
   high-frequency noise
3. **Spectral analysis**: FFT power spectrum, a smoothed version, and
   Welch's method (segment-averaged PSD) - then estimate each
   participant's **Individual Alpha Frequency (IAF)**, the peak in the
   7.5-12.5 Hz band, from all three estimates
4. **Time-frequency analysis** via spectrograms, to see how alpha power
   evolves over the recording rather than just its average shape
5. **Reconstruct the alpha-band component** of each signal by
   band-passing to +-1 Hz around each participant's estimated IAF and
   inverse-FFTing back to the time domain

See the notebook's "Key Findings" section at the end for the actual
numbers - alpha power is consistently higher eyes-closed than
eyes-open across all three participants, by roughly 2.4x to 15x,
which is exactly what the alpha-blocking effect predicts.

## Tools

`numpy`, `scipy.signal` (`butter`, `filtfilt`, `welch`, `spectrogram`),
`matplotlib`, `pandas`

## Running it

The three CSVs (`subject_504.csv`, `subject_519.csv`, `subject_524.csv`)
are included in this repo, so the notebook runs as-is - just run all
cells. Each CSV has two columns, `EC` (eyes closed) and `EO` (eyes
open).

## Data

The three participants' recordings are public data, included here for
reproducibility.

## Note

The original notebook loaded these files from Google Drive inside
Colab (`drive.mount(...)` + an absolute `/content/drive/...` path);
that's been replaced with a plain relative `pd.read_csv`-style load so
the notebook runs anywhere, Colab or not.
