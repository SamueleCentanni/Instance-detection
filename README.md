# 📚 Book Instance Detection

![OpenCV](https://img.shields.io/badge/OpenCV-5C3EE8?style=for-the-badge&logo=opencv&logoColor=white)
![Python](https://img.shields.io/badge/Python-3.8%2B-blue?style=for-the-badge&logo=python&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=for-the-badge&logo=jupyter&logoColor=white)

Implementation of a Computer Vision system for **Product Recognition**, specifically designed to identify books on shelves using **traditional computer vision techniques** (no Deep Learning).

Developed for the **Image Processing and Computer Vision** course (Module 1) at the **University of Bologna**.

**Authors:**
* **Samuele Centanni**
* **Mattia Lodi**
* **Tomaž Cotič**

---

## 📖 Project Overview

The objective of this assignment is to develop a pipeline that, given a reference image for a specific book (Model), can identify and localize all its instances within a cluttered image of a shelf (Scene).

### The Challenge
Unlike generic object detection, this is an **Instance-level** detection task. The system must:
1.  Match specific book covers despite occlusion, rotation, and lighting changes.
2.  Be robust to clutter (many other books on the shelf).
3.  Use **only** traditional feature extraction and matching techniques.

---

## 🎯 Task Requirements

For each product (book) found in the scene, the system outputs:
* **Count:** Number of instances found.
* **Dimensions:** Area in pixels of the bounding box.
* **Position:** The 4 corners of the bounding box $(x, y)$.
* **Visualization:** An overlay of the bounding boxes on the scene image.

---

## 📂 Dataset Structure

The project relies on a custom dataset organized as follows:

* **`dataset/models/`**: Contains reference images of the books to be detected (e.g., `model_0.png`, `model_1.png`). These are flat, scanned-like images of covers.
* **`dataset/scenes/`**: Contains various photos of shelves where the books are placed in different positions and angles (e.g., `scene_0.jpg`).

---

## 🛠 Methodology

The solution is implemented using **OpenCV** and follows a standard feature-matching pipeline:

1.  **Feature Extraction:** Detecting keypoints and computing descriptors (SIFT) for both the *Model* and the *Scene*.
2.  **Feature Matching:** Finding correspondences between model features and scene features (e.g., using FLANN or BFMatcher).
3.  **Filtering:** Removing outliers / incorrect matches (e.g., Lowe's Ratio Test).
4.  **Localization:** Using **Homography** (RANSAC) to project the corners of the model onto the scene to draw the bounding box.
5.  **Clustering (Optional):** Techniques to separate multiple instances of the same book in one scene.

---
