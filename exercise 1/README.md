# Exercise 1 — Reading and Visualizing DICOM Data

## Overview

This exercise introduces the basics of reading and displaying medical image data in Python. It covers the DICOM file format, extracting imaging metadata, loading 3D volumes, and understanding the anisotropy problem in medical imaging.

---

## Tasks Covered

### Task 4 — Read DICOM Data
Read a DICOM slice using `dcmread()` and extract the following parameters:

| Parameter | Value |
|---|---|
| Imaging Modality | MR (Magnetic Resonance Imaging) |
| Slice Thickness (z) | 5.0 mm |
| Pixel Spacing | 0.859375 × 0.859375 mm |
| Grid Size | 256 × 256 pixels |
| Smallest Image Pixel Value | 0 |
| Largest Image Pixel Value | 884 |

**Key code:**
```python
from pydicom import dcmread

dcm_slice = dcmread('dataset1/brain_001.dcm')

print(f'Imaging Modality:           {dcm_slice.Modality}')
print(f'Slice Thickness (z):        {dcm_slice.SliceThickness} mm')
print(f'Pixel Spacing (x, y):       {dcm_slice.PixelSpacing[0]} x {dcm_slice.PixelSpacing[1]} mm')
print(f'Grid Size (Rows x Cols):    {dcm_slice.Rows} x {dcm_slice.Columns} pixels')
print(f'Smallest Image Pixel Value: {dcm_slice.SmallestImagePixelValue}')
print(f'Largest Image Pixel Value:  {dcm_slice.LargestImagePixelValue}')
```

---

### Task 5 — Visualization of 3D Medical Image Data (Theory)

The dataset has shape **[256, 256, 20]**:
- x (coronal): 256 pixels @ 0.859 mm
- y (sagittal): 256 pixels @ 0.859 mm
- z (axial): 20 slices @ 5.0 mm

**The Anisotropy Problem:**
Voxels are not cubic — they are ~5.82× larger in z than in x/y. This causes sagittal and coronal slices to appear squashed/stretched.

**Solution:** Isotropic resampling using `ndimage.zoom()` with a zoom factor of `5.0 / 0.859 ≈ 5.82` in the z-direction, producing uniform 0.859 × 0.859 × 0.859 mm voxels.

**Key code:**
```python
import os
import numpy as np
from scipy import ndimage
from pydicom import dcmread
import matplotlib.pyplot as plt

# Load full 3D volume
def read_dcm_volume(name):
    volume_img = []
    for file in sorted(os.listdir(name)):
        if file.endswith('.dcm'):
            dcm_slice = dcmread(os.path.join(name, file))
            volume_img.append(dcm_slice.pixel_array)
    return np.transpose(np.array(volume_img), (1, 2, 0))

dcm_volume = read_dcm_volume('dataset1')

# Extract slices (anisotropic)
axial_slice    = dcm_volume[:, :, 10]   # z fixed
sagittal_slice = dcm_volume[:, 128, :]  # y fixed
coronal_slice  = dcm_volume[128, :, :]  # x fixed

# Fix anisotropy
zoom_factor_z = 5.0 / 0.859375
dcm_volume_resampled = ndimage.zoom(dcm_volume, (1, 1, zoom_factor_z))
```

---

## Concepts Learned

- DICOM file structure and metadata fields
- How to load a 3D volume from individual slice files
- Axial, sagittal, and coronal slice orientations
- What voxel anisotropy is and how to correct it with interpolation
- Using `matplotlib` subplots to compare multiple images

---

## How to Run

1. Open `exercise1_solution.ipynb` in [Google Colab](https://colab.research.google.com)
2. Upload your DICOM dataset into a folder called `dataset1/`
3. Run all cells top to bottom
