# Driver Fatigue Detection Project

## What's included

- `Driver_Fatigue_Detection.ipynb`: end-to-end notebook for four-class image classification, custom CNN vs. frozen MobileNetV2, independent eye/mouth binary models, confusion matrices and precision/recall, three-stage fusion, session progression, and brightness stress checks.
- `requirements.txt`: Python dependencies.

## Dataset found in the supplied ZIP

The supplied archive contains 2,900 JPG images under `train/Closed`, `train/Open`, `train/no_yawn`, and `train/yawn` (725–726 images per class). It does not contain separate validation/test directories, a dataset citation, license, or subject/session IDs. The notebook creates a reproducible stratified 70/15/15 image-level split. If person/video IDs can be recovered, replace it with group-based splitting to reduce leakage. Confirm the source and license before redistribution or publication.

## Run

1. Install Python 3.10+ and the requirements. A GPU is helpful but not required.
2. Put the original ZIP next to the notebook (the notebook checks the uploaded archive names) or set `ZIP_PATH` to the correct file.
3. Open the notebook and run all cells. First MobileNetV2 run may need internet access to fetch ImageNet weights.
4. Metrics, saved models, model comparison, and progression CSV are created in `artifacts/`.
5. For meaningful progression, put actual time-ordered frames in `session_frames/`; adjust `FRAMES_PER_MINUTE` to match capture rate. Without these, the notebook uses a shuffled synthetic example and labels it as such.

## Labels and fusion

- `Closed` / `Open`: eye state.
- `yawn` / `no_yawn`: mouth state.
- Rule-based mapping: `Open` or `no_yawn` → Alert (0); `yawn` → Mild Fatigue (1); `Closed` → Severe Fatigue (2).

The supplied ZIP combines eye and mouth categories as four labels. The notebook derives two separate binary tasks from those labels and also trains four-class models.

## Safety and evaluation

This is an educational prototype, not a validated driver-monitoring or medical/safety system. Image-level held-out metrics do not establish performance on unseen drivers, cameras, or road conditions. Do not use the prototype to decide whether a person is safe to drive.
