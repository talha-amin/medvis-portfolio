# Medical Visualization — University Coursework Portfolio

This repository documents my practical coursework in **Medical Visualization**, completed as part of my university studies. The tasks cover foundational skills in medical image processing using Python, including reading DICOM data, 3D volume visualization, image filtering, and segmentation.

---

## 🛠️ Technologies Used

- Python 3
- [pydicom](https://pydicom.github.io/) — reading DICOM medical image files
- [NumPy](https://numpy.org/) — array and matrix operations
- [SciPy (ndimage)](https://docs.scipy.org/doc/scipy/reference/ndimage.html) — image filtering and processing
- [Matplotlib](https://matplotlib.org/) — visualization and plotting
- Google Colab — development environment

---

## 📁 Repository Structure

```
medvis-portfolio/
│
├── exercise1/
│   ├── exercise1_solution.ipynb   ← DICOM reading + 3D volume slicing
│   └── README.md
│
├── exercise2/
│   ├── task3/
│   │   ├── exercise2_task3.ipynb  ← Image filtering (Median & Gaussian)
│   │   └── README.md
│   └── README.md
│
└── README.md  ← You are here
```

---

## 📚 Exercises Overview

### Exercise 1 — Reading and Visualizing DICOM Data
- Reading DICOM files using `pydicom`
- Extracting imaging parameters (modality, resolution, pixel values)
- Loading a 3D MRI volume from multiple slices
- Visualizing axial, sagittal, and coronal slices
- Understanding and correcting the **anisotropy problem** using interpolation

### Exercise 2 — Image Processing
- Applying **salt & pepper noise** to a medical image
- Comparing **Median filter** vs **Gaussian filter** for noise reduction
- Understanding when each filter is appropriate in a medical context
- Segmentation using thresholding and connected component analysis

---

## ⚠️ Note on Data

DICOM datasets used in these exercises are **not included** in this repository as they contain medical imaging data. The notebooks use a brain MRI dataset (dataset1) provided as part of the course. To run the notebooks, upload your own DICOM dataset to Google Colab and adjust the file paths accordingly.

---

## 🎯 Key Concepts Learned

- Medical imaging modalities (CT, MRI, X-Ray, PET, Ultrasound)
- DICOM file format and metadata structure
- Hounsfield Units (CT gray value standardization)
- Voxel anisotropy in 3D medical volumes
- Image histogram and windowing
- Noise types and appropriate filter selection
- Image segmentation principles

---

*Coursework completed as part of Medical Visualization, [Your University Name]*
