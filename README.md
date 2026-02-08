# Forced Alignment using Montreal Forced Aligner MFA
Forced alignment using Montreal Forced Aligner (MFA) to align audio with transcripts at word and phoneme level, including OOV handling and TextGrid outputs.

# Forced Alignment using Montreal Forced Aligner (MFA)

## Objective
To perform forced alignment between speech audio and its corresponding text
transcription using Montreal Forced Aligner (MFA) and generate word-level and
phoneme-level boundaries.

## Tools Used
- Montreal Forced Aligner (v3.3.4)
- Praat
- Windows 10
- Miniconda

## Dataset
The dataset consists of speech audio files (.wav) and corresponding transcript
files (.txt). Each transcript contains the spoken content of the audio.

## Installation
```bash
conda create -n mfa python=3.9
conda activate mfa
mamba install -c conda-forge montreal-forced-aligner
````
## Download models
```bash
mfa model download acoustic english_us_arpa
mfa model download dictionary english_us_arpa
```
## Run Alignment
```bash
mfa align data english_us_arpa english_us_arpa output
```
## Output

TextGrid files are generated in the output folder containing:
Word boundaries
Phoneme boundaries
These can be visualized using Praat software.

