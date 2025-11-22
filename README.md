# HindiNER

## Hindi Audio → Text → NER (XLM-RoBERTa) Pipeline

Turn Hindi audio into text and extract named entities using a pre-trained XLM-RoBERTa model.

## Overview
This repository contains a self-contained notebook that:
- Uses an existing transcription file (`final_transcription.txt`) or transcribes uploaded/provided audio
- Load the pre-trained XLM-RoBERTa model fine-tuned on the dataset.
- Runs NER and displays both token-level tags and structured entities

Core file:
- `Audio_to_NER.ipynb`: End-to-end pipeline (audio → text → NER)

## Features
- Audio upload or path-based transcription (fallback to `final_transcription.txt` if available)
- Hindi spell-check pass with lightweight common corrections
- XLM-RoBERTa-based NER with inline tagged output and a dataframe of entities
- Entity counts summary for quick inspection

## Requirements
- Python 3.8–3.11
- Jupyter Notebook or JupyterLab
- ffmpeg (required by `pydub` for audio processing)

Python packages (installed automatically in the notebook, but listed here):
- `pandas`, `numpy`, `scikit-learn`
- `pydub`, `faster-whisper`, `ipywidgets`

## Using the Notebook
1. Launch Jupyter and open `Audio_to_NER_Pipeline.ipynb`:
   ```bash
   jupyter notebook
   ```
2. Run the first cell to install/import dependencies.
3. Choose how to provide input text:
   - Upload an audio file (WAV/MP3), or
   - Enter a local audio path, or
   - Ensure `final_transcription.txt` exists (the notebook will use it as a fallback)
4. Click “Transcribe audio” to process input. If an audio file is provided or a path is valid, it will be transcribed with `faster-whisper` and optionally spell-checked.
5. Run the NER cell to see:
   - Token-level tags (first 200 tokens shown)
   - A dataframe of entities and label counts

The notebook also writes successful transcriptions to `final_transcription.txt` for reproducibility.

## Using an Existing Transcription
If you already have text, save it in UTF-8 as `final_transcription.txt` in the project root. The notebook will pick it up automatically when no audio is supplied.

## Notes on `faster-whisper`
- Model size can be adjusted in the notebook (default: `medium`). Smaller models are faster; larger models can be more accurate.
- If you have a GPU, `faster-whisper` will try to use it automatically.

## Troubleshooting
- "ffmpeg not found": Install ffmpeg and ensure `ffmpeg.exe` is on your PATH (Windows) or install via your package manager (macOS/Linux).
- No entities detected: Ensure you’re loading the correct XLM-RoBERTa model and that the input text is in Hindi; validate that tokens are being generated as expected.
- Empty transcription: Check audio quality and try adjusting silence split parameters in the notebook.
- Widgets don’t render: Enable `ipywidgets` and ensure the nbextension is enabled.

## Repository Structure (typical)
```
.
├─ Audio_to_NER_Pipeline.ipynb
├─ final_transcription.txt                   # (created after successful transcription; optional)
```

## Acknowledgements
- Transcription powered by `faster-whisper`
