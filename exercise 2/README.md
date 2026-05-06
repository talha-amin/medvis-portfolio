# Exercise 2 — Image Processing

## Overview

This exercise covers fundamental image processing techniques applied to medical images. It includes noise reduction using filters, image segmentation, and morphological operations.

---

## Tasks

| Task | Topic | Status |
|---|---|---|
| Task 3 | Image Preprocessing — Smoothing (Median & Gaussian filters) | ✅ Complete |
| Task 4 | Image Segmentation (Thresholding + Connected Component Analysis) | ✅ Complete |
| Task 5 | Morphological Operations (Erosion, Dilation, Opening, Closing) | ✅ Complete |

---

## Key Concepts

**Median Filter**
- Replaces each pixel with the median value of its neighborhood
- Best for salt & pepper noise — completely ignores extreme outliers
- Risk: can erase thin structures (e.g. blood vessels) narrower than the kernel size

**Gaussian Filter**
- Replaces each pixel with a weighted average of its neighborhood
- Best for general/random scanner noise
- Safer for thin structures but cannot fully remove extreme outliers

**Thresholding**
- Segments image by labeling pixels above/below an intensity threshold
- Simple but limited — different tissues with similar intensities get merged

**Connected Component Analysis (CCA)**
- Labels connected groups of pixels after segmentation
- Used to filter out small noise regions and keep only the target structure

**Morphological Operations**
- Erosion: shrinks bright regions (removes small noise)
- Dilation: expands bright regions (fills small gaps)
- Opening: erosion then dilation (removes small objects)
- Closing: dilation then erosion (fills small holes)
