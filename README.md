# WBC_detection
A YOLOv11-based object detection system for identifying white blood cells in microscopic images to assist automated medical analysis.

*WBC Detection:* Utilizes a custom-trained YOLOv11 nano model to accurately identify WBCs in microscopic images.
WBC Classification: Classifies WBCs into Lymphocytes (LYM), Neutrophils (NEU), and Monocytes (MON) based on their detected diameters.

*Streamlit Web Interface:* Provides an interactive web application for uploading images, visualizing detections, and viewing diagnostic reports.

*Dynamic Calibration:* Allows users to adjust calibration parameters (µm/px ratio, diameter thresholds) directly within the Streamlit app for fine-tuning classification.

*Deployment:* Designed to run efficiently in a Google Colab environment with a secure cloudflared tunnel for public access.

# Setup and Usage
1. Open in Google Colab
This notebook is intended to be run in Google Colab. Open the .ipynb file in Colab.

2. Mount Google Drive
Ensure your Google Drive is mounted to save model weights and access dataset files. This is typically done automatically or can be manually executed using the provided cell:

## 📦 Data Loading

```python
from google.colab import drive
drive.mount('/content/drive', force_remount=True)
```
3. Install Dependencies
The project requires ultralytics, streamlit, opencv-python, pillow, and matplotlib. These will be installed by the provided cells in the notebook.

4. Prepare Dataset and Train Model
Follow the steps in the notebook to:

Download and extract the BCCD (Blood Cell Count and Detection) dataset.
Convert XML annotations to YOLO format.
Split the dataset into training and validation sets.
Train the YOLOv11 nano model using the prepared dataset.

5. Run the Streamlit Application
Once the model is trained, the notebook includes cells to:
Generate the app.py Streamlit application code.

6. Access the Web Interface
Click on the generated public URL (e.g., https://xxxx.trycloudflare.com).
Upload a blood smear image using the sidebar Upload Blood Smear Image button.
Observe the automated microscopic detection and diagnostic report.
Adjust Calibration Ratio, LYM/NEU Threshold, NEU/MON Threshold, and Confidence Threshold in the sidebar to refine the classification.
Install cloudflared (or localtunnel).
Start the Streamlit app in the background and create a public tunnel link.

Model Performance
The trained YOLOv11 nano model achieved the following validation metrics:

mAP50: 0.995
mAP50-95: 0.827
These metrics indicate strong performance in detecting and localizing WBCs, with high precision across various Intersection over Union (IoU) thresholds.

# Directory Structure

```
/content/drive/MyDrive/wbc_yolo/
├── exports/                   # Saved model training results (best.pt, last.pt, etc.)
│   ├── wbc_detection_model/
│   └── wbc_detection_model-2/ # Latest model training run
├── JPEGImages/                # Original images for training
├── BCCD_Dataset-master.zip    # Raw dataset zip file
└── wbc_data.yaml              # YOLO dataset configuration

/content/
├── WBC_Dataset/               # Processed dataset for YOLO training
│   ├── images/
│   │   ├── train/
│   │   └── val/
│   └── labels/
│       ├── train/
│       └── val/
├── app.py                     # Streamlit application code
└── cloudflared                # Cloudflare Tunnel executable
```
