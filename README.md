# Multimodal Crime Report Analyzer

This project is a team-built multimodal crime analysis system for assignment work across audio, document, image, text, video, and final integration stages. Each modality lives in its own folder so it can be developed, tested, and documented independently.

## Assignment Folder Mapping

The assignment brief asks for folders like `/audio`, `/pdf`, `/images`, `/video`, `/text`, and `/integration`.

This repository uses slightly more descriptive names, but they map directly:

- `audio_analysis/` = assignment `/audio`
- `document_analysis/` = assignment `/pdf`
- `image_analysis/` = assignment `/images`
- `video_analysis/` = assignment `/video`
- `text_analysis/` = assignment `/text`
- `integration/` = assignment `/integration`

## Current Modules

- `audio_analysis/` processes emergency-call audio and writes structured CSV output
- `document_analysis/` extracts structured incident details from PDF reports
- `image_analysis/` analyzes scene images and writes structured detection CSV output
- `text_analysis/` analyzes crime-related text records and writes structured CSV outputs
- `video_analysis/` analyzes surveillance-style clips and generates an event log
- `integration/` merges the available modality outputs into one assignment-ready incident report and dashboard

## Repository Structure

```text
MultimodalCrimeReportAnalyzer/
├── README.md
├── audio_analysis/
├── document_analysis/
│   ├── README.md
│   ├── data/
│   ├── output/
│   ├── requirements.txt
│   └── src/
├── image_analysis/
│   ├── README.md
│   ├── data/
│   ├── output/
│   ├── requirements.txt
│   └── src/
├── integration/
│   ├── app.py
│   ├── README.md
│   ├── data/
│   ├── output/
│   ├── requirements.txt
│   └── src/
├── text_analysis/
│   ├── README.md
│   ├── data/
│   ├── output/
│   ├── requirements.txt
│   ├── requirements-full.txt
│   └── src/
├── video_analysis/
│   ├── README.md
│   ├── data/
│   ├── frames/
│   ├── output/
│   ├── requirements.txt
│   └── src/
└── yolov8n.pt
```

## Module Guides

Each implemented module has its own README with setup and run instructions:

- [Audio Analysis](audio_analysis/README.md)
- [Document Analysis](document_analysis/README.md)
- [Image Analysis](image_analysis/README.md)
- [Text Analysis](text_analysis/README.md)
- [Video Analysis](video_analysis/README.md)
- [Integration](integration/README.md)

## Quick Start

Choose the module you want to run, move into that folder, create a virtual environment, install dependencies, and follow that module's README.

Examples:

Audio analysis:

```bash
cd audio_analysis
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
python3 src/audio_analyzer.py --data data --output output/audio_output.csv --max 10 --summary
```

Document analysis:

```bash
cd document_analysis
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
python -m spacy download en_core_web_sm
python3 src/document_analysis.py data/LESO2.pdf -o output/incident_extract.csv -v
```

Text analysis:

```bash
cd text_analysis
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
python3 src/text_analysis.py --input "data/CrimeReport (1).txt" --no-transformers
```

Image analysis:

```bash
cd image_analysis
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
python3 src/main.py --mode infer --config app.config.yaml --max-images 150
```

Video analysis:

```bash
cd video_analysis
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
python3 src/motion_detection.py
```

Integration:

```bash
cd integration
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
python3 src/integrate_reports.py
streamlit run app.py
```

The integration module uses a manual mapping file at `integration/data/incident_map.csv`
to link `Call_ID`, `Report_ID`, `Image_ID`, `Clip_ID`, and `Text_ID` to a shared
`Incident_ID`.

## Outputs

Current outputs produced by the implemented modules:

- `audio_analysis/output/audio_output.csv`
- `document_analysis/output/incident_extract.csv`
- `image_analysis/output/image_analyst_output.csv`
- `text_analysis/output/text_output.csv`
- `video_analysis/output/video_event_log.csv`
- `integration/output/final_integrated_incident_report.csv`

## Notes

- `video_analysis/` uses the `yolov8n.pt` model file already present in the project root.
- `document_analysis/` may require Tesseract OCR for scanned PDFs.
- `text_analysis/` can run in a lightweight rule-based mode with `--no-transformers`.
- `integration/` includes a Streamlit dashboard at `integration/app.py`.
