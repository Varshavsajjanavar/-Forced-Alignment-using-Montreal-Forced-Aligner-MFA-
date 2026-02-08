# Forced Alignment using Montreal Forced Aligner (MFA)

## Objective
To perform forced alignment between speech audio and text transcripts using Montreal Forced Aligner (MFA), and analyze word and phoneme boundaries.

## What is Forced Alignment?
Forced alignment is the process of aligning a known transcript with an audio recording to obtain time boundaries for words and phonemes.

## Dataset
The dataset contains:
- `wav/` – audio files
- `transcripts/` – corresponding text files

Each audio file has one transcript.

## Environment Setup

```bash
conda create -n mfa python=3.9
conda activate mfa
conda install -c conda-forge montreal-forced-aligner
```
## Download Models

```bash
mfa model download acoustic english_us_arpa
mfa model download dictionary english_us_arpa
```
## Corpus Preparation
All .wav and .txt files are placed in a single folder called corpus/.

Validate corpus:
```bash
mfa validate corpus english_us_arpa
```
## First Alignment
```bash
mfa align corpus english_us_arpa english_us_arpa aligned --clean --verbose
```
This generates TextGrid files in the aligned/ folder.

## OOV Handling

Some words were not found in the dictionary (Out-Of-Vocabulary).

OOV list generated:
```bash
oovs_found_english_us_arpa.txt
```
Generate pronunciations using G2P:
```bash
mfa models download g2p english_us_arpa
mfa g2p oovs_found_english_us_arpa.txt english_us_arpa generated.dict
```
Merge with original dictionary:
```bash
type english_us_arpa.dict generated.dict > english_us_arpa_fixed.dict
```
## Final Alignment (After OOV Fix):
```bash
mfa align corpus english_us_arpa_fixed.dict english_us_arpa aligned_fixed --clean --verbose
```
## Output

- aligned/ → initial alignment.

- aligned_fixed/ → improved alignment after OOV handling.

## Visualization

 The generated TextGrid files were opened in Praat to inspect:

- Word boundaries

- Phoneme boundaries

## Observations

- Initial alignment skipped OOV words.

- After G2P-based dictionary expansion, all words were aligned.

- Phoneme boundaries closely matched speech.

- Minor timing offsets observed for fast speech segments.

## Tools Used

- Montreal Forced Aligner v3.3.4.

- Praat for visualization.

- Conda environment.
## Screenshots

### OOV Words Detected
![OOV Count](screenshots/oov_count.png)

### OOV List
![OOV Found](screenshots/oov_found.png)

### Generated Dictionary
![Generated Dictionary](screenshots/generated.dict.png)

### TextGrid Visualization in Praat
![Praat Alignment](screenshots/utterances.png)

