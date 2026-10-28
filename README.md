# Capsule-Endoscopy-Polyp-Detection
# Polyp Detection and Bench-Top Magnetic Positioning for a Wireless Capsule Endoscopy Proof of Concept

## 1. Project Overview

This project explores polyp detection in gastrointestinal endoscopy images using YOLOv8 and image-enhancement techniques. It also investigates temporal filtering to reduce inconsistent frame-by-frame predictions in endoscopic video.

The project includes experiments E0–E5, progressing from baseline detection to enhanced image processing and temporal analysis using a Hidden Markov Model (HMM).

The perception pipeline runs on a laptop. An ESP32-CAM provides the video stream over Wi-Fi, and Python with OpenCV processes the stream and performs inference using the trained YOLO model.

A separate Arduino UNO-controlled servo arm carries an external magnet for bench-top positioning experiments. The detector and the magnetic positioning arm are not integrated into a closed-loop autonomous control system.

**This is a proof-of-concept project, not a clinically validated medical diagnostic system.**

---

## 2. Objectives

- Establish a baseline YOLOv8n model for polyp detection.
- Evaluate image-enhancement techniques for endoscopic images.
- Investigate the effects of fractional-derivative and Haar Discrete Wavelet Transform (DWT) enhancement.
- Apply temporal filtering to reduce frame-to-frame prediction instability.
- Compare detection results across experiments E0–E5.
- Explore a separate bench-top magnetic positioning setup.

---

## 3. Experiments

| Experiment | Description |
|---|---|
| E0 | Baseline YOLOv8n polyp detection. |
| E1 | Image enhancement using a Sakaguchi-type approach. |
| E2 | E1 enhancement with an additional fractional-derivative operation. |
| E3 | Enhanced image processing incorporating Haar DWT detail enhancement. |
| E4 | Temporal filtering using a Hidden Markov Model (HMM) based on E3 predictions. |

Refer to the notebook for the actual implementation, experiment parameters, and evaluation procedures.

---

## 4. Dataset

The project uses a YOLO-format version of the Kvasir-SEG dataset.

The dataset is divided into:

| Split | Number of images |
|---|---:|
| Training | 700 |
| Validation | 150 |
| Testing | 150 |
| **Total** | **1,000** |

The dataset directory must retain the structure and filenames expected by the notebook.

### Expected dataset location

The notebook uses Google Drive as its storage location. The expected dataset root is:

`/content/drive/MyDrive/Capsule_Perception/Kvasir-SEG.yolov8_split/`

The directory must contain the training, validation, and test splits:

```text
Kvasir-SEG.yolov8_split/
├── train/
├── val/
└── test/
```

**Important**: Keep the folder names unchanged because the notebook uses predefined file paths. The dataset version downloaded from Roboflow may have a different split or directory structure, so verify it before running the notebook. Do not change the notebook code.

The contents of each split must match the format expected by the notebook and the YOLO data configuration, including the relevant images and annotation files.

### Dataset source

The original Kvasir-SEG dataset is available from the official dataset website:

https://universe.roboflow.com/teste-mhypc/kvasir-seg-gouny

Use the dataset version and YOLO-format conversion corresponding to the project. Check the dataset's terms before redistributing its files.

---

## 5. Required Google Drive Folder Structure

The notebook uses paths under the `Capsule_Perception` directory. The directory names and file paths are important because the code references them directly.

The following structure represents the project layout relevant to the current experiments:

```text
My Drive/
└── Capsule_Perception/
    ├── Kvasir-SEG.yolov8_split/
    │   ├── train/
    │   ├── val/
    │   └── test/
    │
    └── experiments/
        └── Professor_Fresh_Run/
            ├── training_runs/
            │   └── E3_Sakaguchi_Fractional_DWT/
            │       └── weights/
            │           └── best.pt
            │
            └── E4_Final_HMM/
                ├── Videos/
                │   ├── 512722d1-05f9-4454-a343-7aba1fb462c2.avi
                │   └── df1aa095-0cab-4433-97fe-00d456f33615.avi
                │
                ├── raw_video_predictions/
                │   └── df1aa095-0cab-4433-97fe-00d456f33615_predictions.csv
                │
                └── hmm_video_predictions/
                    └── df1aa095-0cab-4433-97fe-00d456f33615_e4_hmm.csv
```

The tree above lists the known paths and files used by the project. Other folders and generated files may be created by the notebook during training, evaluation, or visualization.

### 5.1 Dataset directory

```text
Capsule_Perception/
└── Kvasir-SEG.yolov8_split/
    ├── train/
    ├── val/
    └── test/
```

This directory contains the dataset splits required by the notebook.

Keep the directory name exactly as shown:

`Kvasir-SEG.yolov8_split`

### 5.2 E3 trained model

The E3 model weights are expected at:

```text
Capsule_Perception/
└── experiments/
    └── Professor_Fresh_Run/
        └── training_runs/
            └── E3_Sakaguchi_Fractional_DWT/
                └── weights/
                    └── best.pt
```

Full Colab path:

```text
/content/drive/MyDrive/Capsule_Perception/experiments/Professor_Fresh_Run/training_runs/E3_Sakaguchi_Fractional_DWT/weights/best.pt
```

The `best.pt` file contains the trained YOLO model weights used by downstream evaluation or video-processing steps that reference this path.

If the notebook loads these weights directly, the file must be available at the expected location before running the relevant cell.

### 5.3 E4 input videos

The original videos are stored in:

```text
Capsule_Perception/
└── experiments/
    └── Professor_Fresh_Run/
        └── E4_Final_HMM/
            └── Videos/
```

The known video filenames are:

- `512722d1-05f9-4454-a343-7aba1fb462c2.avi`
- `df1aa095-0cab-4433-97fe-00d456f33615.avi`

Preserve the filenames if the notebook references them directly.

### 5.4 Raw E3 video predictions

The raw prediction CSV is located at:

```text
Capsule_Perception/
└── experiments/
    └── Professor_Fresh_Run/
        └── E4_Final_HMM/
            └── raw_video_predictions/
                └── df1aa095-0cab-4433-97fe-00d456f33615_predictions.csv
```

Full path:

```text
/content/drive/MyDrive/Capsule_Perception/experiments/Professor_Fresh_Run/E4_Final_HMM/raw_video_predictions/df1aa095-0cab-4433-97fe-00d456f33615_predictions.csv
```

This file contains frame-level prediction data from the E3 video-processing stage.

### 5.5 E4 HMM predictions

The HMM output CSV is located at:

```text
Capsule_Perception/
└── experiments/
    └── Professor_Fresh_Run/
        └── E4_Final_HMM/
            └── hmm_video_predictions/
                └── df1aa095-0cab-4433-97fe-00d456f33615_e4_hmm.csv
```

Full path:

```text
/content/drive/MyDrive/Capsule_Perception/experiments/Professor_Fresh_Run/E4_Final_HMM/hmm_video_predictions/df1aa095-0cab-4433-97fe-00d456f33615_e4_hmm.csv
```

The known columns include:

- `video`
- `frame`
- `timestamp_seconds`
- `detected`
- `max_confidence`
- `num_detections`
- `boxes_xyxy`
- `e3_detected_at_hmm_threshold`
- `e4_hmm_state`
- `e4_polyp_probability`

These fields support analysis of raw detections and temporally filtered states.

**Note:** The CSVs and model weights above are existing project artifacts. If a notebook cell loads them rather than generating them, they must be present before that cell runs. Do not assume that running the notebook will recreate missing files automatically.

---

## 6. Repository Contents

A suggested GitHub repository layout is:

```text
polyp-detection-capsule-endoscopy/
├── README.md
├── requirements.txt
├── polyp_detection_experiments.ipynb
└── .gitignore
```

Use the actual notebook filename in your repository.

The repository contains:

- **README.md** — project overview, setup instructions, folder structure, and limitations.
- **requirements.txt** — Python dependencies used by the notebook.
- **polyp_detection_experiments.ipynb** — the Colab notebook containing the experiments.
- **.gitignore** — excludes local environment files, caches, and large generated artifacts that should not be committed.

The notebook is designed to use Google Drive paths. The folder tree in this README documents the required Drive layout; it does not mean that the corresponding files are automatically included in the GitHub repository.

---

## 7. Running the Notebook in Google Colab

### Step 1: Open the notebook

Open the uploaded notebook in Google Colab.

### Step 2: Mount Google Drive

Run the notebook's existing Google Drive mounting cell.

### Step 3: Recreate the directory structure

Inside Google Drive, create the required directories under:

```text
My Drive/Capsule_Perception/
```

Use the directory tree in Section 5 as the reference.

### Step 4: Place the dataset

Place the YOLO-format dataset inside:

```text
My Drive/Capsule_Perception/Kvasir-SEG.yolov8_split/
```

Ensure that the expected training, validation, and test folders are present.

### Step 5: Place existing model and experiment artifacts

If the notebook loads existing E3 weights, videos, or prediction CSVs, upload them to the exact locations described in Section 5.

Do not change the filenames or directory names expected by the code.

### Step 6: Install dependencies

Install the Python dependencies required by the notebook. See `requirements.txt` and the notebook's installation cells.

The Colab runtime may already contain some packages. Package versions should be consistent with the environment in which the notebook was tested.

### Step 7: Run the notebook in order

Execute the notebook cells sequentially, starting from the setup cells.

Some experiments depend on outputs produced by earlier experiments. Running cells out of order or omitting required artifacts may cause path or file-not-found errors.

### Important reproducibility note

This notebook uses paths tied to a particular Google Drive layout. To run it without modifying the code, reproduce that layout and supply all required pre-existing artifacts.

A successful run also depends on the availability of the dataset, trained weights, input videos, and any intermediate CSV files required by the relevant cells.

---

## 8. Evaluation

The notebook includes model evaluation and comparisons across the implemented experiments.

One recorded E3 test evaluation reported:

| Metric | Value |
|---|---:|
| Precision | 0.905 |
| Recall | 0.914 |
| mAP@50 | 0.936 |
| mAP@50–95 | 0.723 |
| Test images | 150 |

These values describe the recorded E3 evaluation, not a guarantee of performance on new datasets, live video, or clinical data. They should be reported with the associated experiment configuration and evaluation conditions.

Use the notebook outputs as the source of truth for the final results of E0–E5.

---

## 9. Hardware and System Scope

### Vision pipeline

- ESP32-CAM for video acquisition.
- Wi-Fi video streaming.
- Laptop for video processing.
- Python and OpenCV for video handling.
- YOLOv8n for polyp detection.

### Bench-top magnetic positioning setup

- Arduino UNO.
- Servo motors arranged as a three-joint arm.
- External magnet attached to the arm.

The magnetic positioning setup is a separate proof-of-concept component. The YOLO detection output is not connected to an autonomous closed-loop controller for the arm.

---

## 10. Limitations

- The project uses a limited dataset of 1,000 images.
- Performance on unseen endoscopic datasets may differ.
- Video-based temporal filtering does not establish clinical reliability.
- HMM outputs depend on the input predictions and selected model parameters.
- The bench-top magnetic positioning setup is not integrated with the vision pipeline.
- No claim of clinical validation, medical diagnosis, or patient-ready deployment is made.
- The repository may not contain the complete dataset, model weights, or generated video artifacts because these files can be large.

---

## 11. Data and Artifact Management

Large files such as datasets, trained weights, videos, and prediction outputs can make Git repositories difficult to clone and maintain.

Before uploading these files:

1. Check the dataset's redistribution terms.
2. Avoid committing files that you do not have permission to redistribute.
3. Keep a record of the exact model weights and dataset version used.
4. If large artifacts are not included in GitHub, document where authorized users can obtain them.
5. Make sure any external download or storage instructions preserve the directory structure expected by the notebook.

**Important:** A README folder tree documents the expected paths but does not provide the missing files. Users must obtain or generate those artifacts separately.

---

## 12. Disclaimer

This project is intended for academic research and proof-of-concept experimentation. It is not intended for clinical diagnosis, treatment decisions, or direct use on patients.

---

## 13. Acknowledgment

The project uses the Kvasir-SEG dataset for polyp detection research. Please refer to the dataset's official documentation and cite the dataset appropriately when using it in academic work.

Official dataset page: https://datasets.simula.no/kvasir-seg/
