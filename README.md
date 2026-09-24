# AI Hazard Recognition and Dynamic Safety-Zone Monitoring

Multi-camera perception and spatial reasoning for monitoring industrial safety zones as equipment and surrounding conditions change in real time.

This repository is part of a CIVS industrial-safety research effort. The codebase is forked from the shared project repository; **my primary contribution is the multi-camera spatial reasoning logic used to convert detections from four camera views into dynamically updated safety boundaries.**

## Research problem

Static safety polygons are easy to define, but they do not represent an active industrial environment well when equipment moves and the safe operating region changes with it.

The project therefore asks a more useful question than object detection alone:

> How can detections from multiple viewpoints be transformed into an updated spatial model of the safe and unsafe regions of the environment?

The resulting system combines perception, tracking, editable zones, and rule-based spatial reasoning to support proactive hazard monitoring.

## System overview

The application combines:

- **YOLOv8** for real-time object detection;
- **DeepSORT** for object tracking;
- **multi-polygon zone monitoring** for spatial safety constraints;
- **FastAPI** services for model inference, event handling, and APIs;
- a **React** interface for live visualization and zone control.

## My contribution

My work focused on the spatial reasoning layer that sits between raw detections and the final safety-zone decision.

The reasoning engine:

- receives detections from **four camera perspectives**;
- identifies the relevant blocker/equipment positions in each view;
- uses the outermost detected positions to update the active safety boundary;
- translates multi-view perception into a rule-based spatial representation that can change as the environment changes.

This is the component described in the associated AISTech 2026 work on dynamic safety-zone reconfiguration.

## Why the multi-camera setting matters

No single view reliably captures the entire operating region. Occlusion, perspective, and equipment motion can make a fixed or single-camera boundary misleading.

Using multiple views allows the system to reason over complementary observations and update the monitored region based on the current equipment configuration rather than a permanently fixed polygon.

## Repository structure

The project contains a full-stack hazard-recognition application:

```text
reactapp/
├── backend/      # FastAPI + ML inference / tracking / zone logic
├── frontend/     # React visualization and controls
└── README.md
```

## Running the application

### Backend

```bash
cd reactapp/backend
python -m venv .venv
source .venv/bin/activate       # Linux/macOS
# .\.venv\Scripts\activate      # Windows
pip install -r requirements.txt
uvicorn main:app --reload
```

### Frontend

```bash
cd reactapp/frontend
npm install
npm start
```

The frontend runs on `http://localhost:3000` and communicates with the FastAPI backend.

## Notes

- Model weights are not committed to the repository.
- Logs, uploaded media, and generated snapshots should remain excluded from version control.
- This repository reflects a collaborative research codebase. The contribution statement above is included to distinguish my work from the shared project infrastructure.

## Affiliation

Developed through the **Center for Innovation Through Visualization and Simulation (CIVS), Purdue University Northwest** as part of industrial safety research.
