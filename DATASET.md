# Dataset Information

## Kvasir-SEG Polyp Detection Dataset

This project uses the Kvasir-SEG dataset, originally designed for polyp segmentation and subsequently converted to YOLO object detection format for this project's experiments.

### Dataset Source

**Roboflow Universe:**  
https://universe.roboflow.com/teste-mhypc/kvasir-seg-gouny

### Dataset Preparation

The original segmentation annotations were converted into bounding-box annotations suitable for YOLOv8 object detection.

The dataset used in the experiments contains 1,000 images, split as follows:

| Dataset Split | Number of Images |
|---|---:|
| Training | 700 |
| Validation | 150 |
| Testing | 150 |
| **Total** | **1,000** |

### Required Directory Structure

The Colab notebook expects the converted dataset at:

`/content/drive/MyDrive/Capsule_Perception/Kvasir-SEG.yolov8_split/`

Expected structure:

```text
Capsule_Perception/
└── Kvasir-SEG.yolov8_split/
    ├── data.yaml
    ├── train/
    ├── val/
    └── test/
```

The dataset must contain the image files and corresponding YOLO object detection annotations required by the notebook.

### Setup Instructions

1. Visit the Roboflow Universe dataset page.
2. Download the appropriate dataset version.
3. Obtain or recreate the converted YOLO object detection dataset used in the experiments.
4. Ensure that the dataset contains the same images, annotations, and train-validation-test split as the original experiments.
5. Place the dataset in the directory specified above in Google Drive.

**Important:** Downloading the original segmentation dataset may not reproduce the converted object detection dataset or the exact experimental split. For reproducibility, use the same converted annotations and dataset version as the experiments.

### Licensing and Attribution

Please review the dataset's licensing, attribution, and redistribution requirements on the source page before using or sharing the data.
