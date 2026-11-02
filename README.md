# 🩺 Retinal AI – Diabetic Retinopathy Detection & Vessel Segmentation

### An AI-powered retinal image analysis system combining Deep Learning and Computer Vision to support the early detection and analysis of Diabetic Retinopathy.

<p align="center">
  <strong>ResNet-50 Classification | U-Net Segmentation | YOLO Lesion Detection</strong>
</p>

---

## 📌 Overview

Diabetic Retinopathy (DR) is a diabetes-related eye disease that can damage the blood vessels in the retina and potentially lead to vision loss if not detected early.

**Retinal AI** is a web-based AI application designed to analyse retinal fundus images using multiple deep-learning architectures.

The system integrates three independent AI models into a unified analysis platform:

* **ResNet-50:** Classifies retinal images into five diabetic retinopathy severity levels.
* **U-Net:** Segments retinal blood vessels and generates visual vessel maps.
* **YOLO:** Detects retinal lesions and identifies their locations within fundus images.

The application combines the outputs of these models to provide a comprehensive visual analysis, generate downloadable PDF reports and support email-based report delivery.

The objective is to explore how multiple deep-learning approaches can work together to support retinal image analysis and research in AI-assisted ophthalmology.

---

## ✨ Key Features

| Feature                | Description                                                                              |
| ---------------------- | ---------------------------------------------------------------------------------------- |
| 🧠 DR Classification   | Classifies retinal images into five severity categories using ResNet-50.                 |
| 🩸 Vessel Segmentation | Identifies retinal blood vessel structures using U-Net.                                  |
| 🔍 Lesion Detection    | Detects and localizes retinal lesions using YOLO.                                        |
| 📊 Confidence Analysis | Displays classification confidence and class probabilities.                              |
| 🖼️ Visual Results     | Generates segmentation masks, vessel overlays and annotated detection images.            |
| 📄 PDF Reports         | Generates downloadable retinal analysis reports.                                         |
| 📧 Email Integration   | Sends generated PDF reports through the Brevo email service.                             |
| 🌐 Web Interface       | Provides an interactive React-based interface for image upload and result visualization. |

---

## 🧠 Deep Learning Models

### 1. ResNet-50 – Diabetic Retinopathy Classification

ResNet-50 is a 50-layer deep convolutional neural network based on residual learning.

It is used to classify retinal fundus images into five diabetic retinopathy severity categories.

**Classification Categories:**

1. No Diabetic Retinopathy
2. Mild Diabetic Retinopathy
3. Moderate Diabetic Retinopathy
4. Severe Diabetic Retinopathy
5. Proliferative Diabetic Retinopathy

**Implementation Details:**

* Architecture: ResNet-50
* Framework: PyTorch
* Input size: 224 × 224
* Output: Predicted severity class
* Additional output: Class probabilities and prediction confidence

The backend applies image preprocessing, including CLAHE-based contrast enhancement and ImageNet normalization, before passing the image to the trained model.

### 2. U-Net – Retinal Blood Vessel Segmentation

U-Net is a convolutional neural network architecture commonly used for biomedical image segmentation.

In this project, U-Net identifies retinal blood vessel structures and generates a binary segmentation mask.

**Implementation Details:**

* Architecture: U-Net
* Framework: TensorFlow / Keras
* Patch size: 128 × 128
* Stride: 64 pixels
* Prediction threshold: 0.5
* Output: Binary vessel segmentation mask

The system processes retinal images using overlapping patches and reconstructs the predictions into a full-sized segmentation map.

It also generates a visual overlay highlighting the detected retinal vessels.

### 3. YOLO – Retinal Lesion Detection

YOLO (You Only Look Once) is an object detection architecture used to identify and localize objects within images.

In this project, YOLO is integrated to detect retinal lesions and visualize their locations.

**Implementation Details:**

* Architecture: YOLO
* Framework: Ultralytics
* Input image size: 640
* Confidence threshold: 0.25
* Output: Detected classes, confidence scores and bounding-box coordinates.

The backend also generates an annotated image displaying the detected regions.

---

## 🏗️ System Architecture

The application follows a frontend-backend architecture.

```text
              USER
                |
                |
                v
       React Web Application
                |
                |
          Upload Fundus Image
                |
                v
          FastAPI Backend
                |
       +--------+--------+
       |        |        |
       v        v        v
    ResNet-50  U-Net    YOLO
       |        |        |
       v        v        v
  DR Class.  Vessel    Lesion
             Mask      Detection
       |        |        |
       +--------+--------+
                |
                v
        Analysis Results
                |
       +--------+---------+
       |                  |
       v                  v
  PDF Report         Visual Results
       |
       v
  Brevo Email Service
```

---

## 🛠️ Technology Stack

### Frontend

* React.js
* JavaScript
* CSS3
* Vite
* jsPDF

### Backend

* Python
* FastAPI
* Uvicorn
* REST API

### Artificial Intelligence & Machine Learning

* PyTorch
* TensorFlow
* Keras
* Ultralytics YOLO
* OpenCV
* NumPy
* Torchvision

### Additional Technologies

* Git & GitHub
* Brevo Email API
* Python Dotenv

---

## 📂 Project Structure

```text
Diabetic-Retinopathy-Detection-Vessel-Segmentation/
│
├── backend/
│   └── app.py
│
├── models/
│   ├── resnet_dr_best.pth
│   ├── best_retinal_unet.keras
│   └── best.pt
│
├── public/
│
├── src/
│   ├── App.jsx
│   ├── App.css
│   └── ...
│
├── runs/
│   └── detect/
│       └── predict/
│
├── index.html
├── package.json
├── package-lock.json
├── vite.config.js
├── eslint.config.js
└── README.md
```

---

## ⚙️ Installation & Setup

Follow these steps to run the project locally.

### Prerequisites

Make sure you have installed:

* Node.js and npm
* Python 3.10 or a compatible Python version
* Git

You will also need the trained model weight files.

### 1. Clone the Repository

```bash
git clone https://github.com/MeSachinSNair/Diabetic-Retinopathy-Detection-Vessel-Segmentation.git
```

Navigate into the project directory:

```bash
cd Diabetic-Retinopathy-Detection-Vessel-Segmentation
```

### 2. Set Up the Backend

Navigate to the backend directory:

```bash
cd backend
```

Create a Python virtual environment:

```bash
python -m venv venv
```

Activate the environment on Windows:

```bash
venv\Scripts\activate
```

Install the required Python packages:

```bash
pip install fastapi uvicorn python-multipart python-dotenv requests numpy opencv-python torch torchvision tensorflow ultralytics
```

### 3. Configure Environment Variables

Create a `.env` file inside the `backend` directory.

Add your Brevo credentials:

```env
BREVO_API_KEY=your_brevo_api_key
BREVO_SENDER_EMAIL=your_verified_sender_email
BREVO_SENDER_NAME=Retinal AI
```

These credentials are required for the email report functionality.

Never commit your actual API keys or secret credentials to GitHub.

### 4. Verify Model Files

Ensure the following trained model files are available inside the root `models/` directory:

```text
models/
├── resnet_dr_best.pth
├── best_retinal_unet.keras
└── best.pt
```

The backend requires these files to initialize the three AI models.

### 5. Start the Backend Server

From the `backend` directory, run:

```bash
uvicorn app:app --reload
```

The backend should be accessible at:

```text
http://127.0.0.1:8000
```

FastAPI interactive API documentation:

```text
http://127.0.0.1:8000/docs
```

### 6. Set Up the Frontend

Open a second terminal and navigate to the root project directory.

Install frontend dependencies:

```bash
npm install
```

Start the development server:

```bash
npm run dev
```

The frontend will be available at:

```text
http://localhost:5173
```

---

## 🔌 API Endpoints

The backend provides the following API endpoints:

| Method | Endpoint          | Function                            |
| ------ | ----------------- | ----------------------------------- |
| GET    | `/`               | Backend health check                |
| POST   | `/predict/resnet` | Diabetic Retinopathy classification |
| POST   | `/predict/unet`   | Retinal vessel segmentation         |
| POST   | `/predict/yolo`   | Retinal lesion detection            |
| POST   | `/report/email`   | Email PDF analysis report           |

Interactive API testing is available through FastAPI Swagger UI at `/docs`.

---

## 📊 Analysis Workflow

1. Open the Retinal AI web application.
2. Upload a retinal fundus image.
3. Submit the image for analysis.
4. The frontend sends the image to the FastAPI backend.
5. The three deep-learning models process the image.
6. The application displays:

   * Diabetic Retinopathy classification.
   * Classification confidence and class probabilities.
   * Retinal blood vessel segmentation.
   * Segmentation mask and vessel overlay.
   * Detected retinal lesions and their confidence scores.
7. Generate a PDF analysis report.
8. Optionally send the report through the integrated email service.

---

## 🔬 Project Objective

The project explores the integration of multiple deep-learning architectures for retinal image analysis.

Instead of depending on a single model, the system combines classification, semantic segmentation and object detection to provide different perspectives on retinal abnormalities.

This approach demonstrates the potential of combining computer vision techniques in AI-assisted ophthalmic research.

---

## 👥 Team & Contributions

This project was developed collaboratively as a group project.

**Individual Contribution:**

Sachin S. Nair – ResNet-50-based Diabetic Retinopathy Classification component.

The project also involved collaborative development and integration of the frontend, backend and other deep-learning components.

**Team Members:**

SACHIN S NAIR
SYED MUHAMMED
KARTHIK B PILLAI

---

## ⚠️ Medical Disclaimer

Retinal AI is an academic and research-oriented prototype.

The predictions and visualizations generated by this application are intended for educational and research purposes only.

This system is not a certified medical device and must not be used as a substitute for professional medical diagnosis, clinical evaluation or treatment.

Always consult a qualified ophthalmologist or eye-care professional for medical interpretation.

---

## 🚀 Future Improvements

* Improve model accuracy and generalization.
* Evaluate performance using standard retinal image datasets.
* Add quantitative segmentation metrics such as Dice Score and IoU.
* Add object detection evaluation metrics such as mAP.
* Optimize inference speed.
* Introduce additional retinal disease classification models.
* Deploy the application to a cloud platform.
* Improve security and patient-data privacy controls.

---

## 🤝 Acknowledgements

We acknowledge the contributions of all team members involved in developing this project and the open-source communities behind the deep-learning frameworks and technologies used.

---

<p align="center">
  <strong>Retinal AI – Exploring the potential of Artificial Intelligence in retinal image analysis.</strong>
</p>
