# NutritionCalculate-ComputerVision

## Overview

**NutritionCalculate-ComputerVision** adalah sebuah aplikasi mobile berbasis Computer Vision yang dirancang untuk membantu pengguna menghitung bobot makanan yang ada di piring mereka. Pengguna hanya perlu memfoto piring yang berisi makanan, dan aplikasi akan mengenali jenis-jenis lauk-pauk yang ada di piring serta menghitung bobot masing-masing makanan secara otomatis. 

Aplikasi ini sangat berguna bagi mereka yang ingin memantau asupan nutrisi, menjaga pola makan, atau menghitung jumlah kalori dengan akurat.

## Features

- **Food Recognition**: Menggunakan teknologi Computer Vision untuk mengenali berbagai jenis makanan pada piring pengguna.
- **Weight Estimation**: Menghitung bobot masing-masing makanan berdasarkan analisis gambar.
- **Nutritional Information**: Memberikan perkiraan jumlah kalori dan informasi nutrisi untuk setiap jenis makanan.
- **User-Friendly Interface**: Antarmuka sederhana yang memungkinkan pengguna untuk dengan mudah mengambil foto dan mendapatkan hasil cepat.

## How It Works

1. **Take a Photo**: Pengguna mengambil foto piring yang berisi makanan menggunakan kamera ponsel.
2. **Food Identification**: Algoritma Computer Vision menganalisis gambar untuk mengenali berbagai jenis lauk-pauk yang ada di piring.
3. **Weight Calculation**: Berdasarkan pengenalan visual dan model machine learning, aplikasi memperkirakan bobot makanan.
4. **Nutritional Analysis**: Aplikasi memberikan data nutrisi seperti jumlah kalori dan komposisi makronutrien untuk setiap makanan yang terdeteksi.

## Technology Stack

- **Mobile Framework**: React Native / Flutter (untuk pengembangan aplikasi mobile)
- **Computer Vision**: OpenCV, TensorFlow, atau PyTorch (untuk pengenalan makanan)
- **Backend**: Node.js dengan API Restful untuk komunikasi data antara aplikasi dan server
- **Database**: MongoDB / PostgreSQL untuk menyimpan data nutrisi dan hasil analisis
- **Machine Learning Models**: Pre-trained models untuk deteksi makanan dan perkiraan berat

## Steps and Components

Untuk membuat aplikasi seperti yang kamu rencanakan, ada beberapa teknologi dan metode dari computer vision yang dapat digunakan. Berikut adalah langkah-langkah dan komponen yang bisa membantu dalam pengembangan aplikasi tersebut:

### Object Detection untuk Mengenali Lauk-Pauk:
- Kamu dapat menggunakan model object detection untuk mengenali berbagai jenis makanan pada piring. Framework yang bisa digunakan antara lain TensorFlow, PyTorch, atau Google ML Kit untuk mobile.
- Model seperti **YOLO (You Only Look Once)** atau **Faster R-CNN** dapat dilatih untuk mendeteksi dan mengklasifikasikan berbagai lauk-pauk seperti ayam, ikan, sayur, dan lainnya.

### Image Segmentation untuk Memisahkan Objek:
- Dengan **image segmentation**, kamu dapat memisahkan setiap makanan pada piring secara lebih tepat. Model seperti **Mask R-CNN** bisa digunakan untuk memisahkan tiap objek sehingga dapat menghitung ukuran atau luas dari makanan secara lebih akurat.

### Estimasi Bobot Berat:
- Setelah objek makanan dikenali, kamu bisa mengkombinasikan estimasi ukuran atau volume dari makanan tersebut dengan **database nutrisi** yang mencakup informasi tentang berat per volume jenis makanan.
- Sebagai contoh, untuk memperkirakan berat nasi, volume nasi di gambar bisa dikalkulasi dan dikalikan dengan densitas atau berat rata-rata per unit volume.
- Menggunakan teknik **depth estimation** juga bisa membantu untuk memperkirakan volume makanan berdasarkan ukurannya dalam gambar 2D.

### Preprocessing & Training Data:
- Untuk meningkatkan akurasi deteksi lauk-pauk, kamu akan memerlukan dataset makanan yang cukup besar untuk melatih model. Kamu bisa menggunakan dataset makanan yang sudah ada, atau mengumpulkan data dari berbagai gambar makanan di internet dan kemudian melabelinya secara manual.
- Setelah itu, model object detection dan segmentation bisa dilatih dengan data yang telah disediakan.

### Framework untuk Mobile:
- Untuk membuat aplikasi berbasis ponsel, kamu bisa menggunakan **TensorFlow Lite** atau **Google ML Kit** untuk menjalankan model computer vision di perangkat mobile. Ini memungkinkan kamu untuk membuat aplikasi dengan deteksi makanan secara real-time di ponsel.

### Kalibrasi Kamera untuk Berat yang Akurat:
- Menghitung bobot atau berat makanan juga memerlukan penyesuaian kamera, karena gambar 2D tidak bisa langsung memberikan informasi tentang volume atau berat tanpa referensi.
- Kamu bisa menggunakan referensi ukuran seperti **coin calibration** atau **fiducial markers** pada piring untuk memperkirakan skala objek.


## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/username/NutritionCalculate-ComputerVision.git


<br>
<br>

# Plan A
# Rice Weight Estimation using Object Detection + Weight Mapping

This project utilizes object detection techniques (YOLOv5 or SSD) to detect rice in a plate from an image and predict its weight. The model detects the rice as an object, calculates the bounding box area, and maps it to the weight using a regression model.

## Table of Contents
- [Introduction](#introduction)
- [Technology Stack](#technology-stack)
- [Project Structure](#project-structure)
- [Installation](#installation)
- [Dataset](#dataset)
- [Training the Object Detection Model](#training-the-object-detection-model)
- [Weight Mapping with Regression](#weight-mapping-with-regression)
- [Running the Model](#running-the-model)
- [Results](#results)
- [Contributing](#contributing)
- [License](#license)

## Introduction
This project aims to estimate the weight of rice on a plate using computer vision. We use YOLOv5 (You Only Look Once) or SSD (Single Shot Detector) for object detection to localize the rice and then apply a regression model to map the bounding box size to the actual weight of rice in grams.

This solution is designed to work on any device with a standard camera, making it a flexible and accessible approach for users without the need for specialized sensors (such as depth cameras).

## Technology Stack
The project uses the following technologies:
- **YOLOv5** for object detection, implemented with PyTorch.
- **TensorFlow** or **SSD** as an alternative object detection model.
- **Scikit-learn** for regression mapping from bounding box size to weight.
- **OpenCV** for image processing and bounding box measurements.

## Dataset
You need a dataset of rice images with labeled bounding boxes and corresponding weights. Each image should have a label file that defines the bounding box coordinates for the rice and the true weight in grams.

- You can create your own dataset by capturing images of rice in different quantities on plates.
- Use tools like **LabelImg** or **Roboflow** to annotate the images with bounding boxes around the rice.

The dataset structure should look like this:
![image](https://github.com/user-attachments/assets/18ad84ee-7679-4363-b3c5-736b6c1454ed)


## Training the Object Detection Model
Once the dataset is ready, you can train the YOLOv5 or SSD model to detect rice.

1. **Train YOLOv5**:
    ```bash
    python yolov5/train.py --img 640 --batch 16 --epochs 50 --data data.yaml --weights yolov5s.pt
    ```

2. **Train SSD**:
    Follow the TensorFlow Object Detection API instructions for training SSD models.

## Weight Mapping with Regression
Once the object detection model is trained and can accurately detect rice, we use regression to estimate the weight based on the bounding box size.

1. Extract bounding box size from detected images.
2. Train a regression model (e.g., Linear Regression, Random Forest) to map bounding box size to actual weight.

