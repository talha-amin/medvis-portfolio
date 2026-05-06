# Task 5 — Morphological Operations

## Overview

This task applies four morphological operations to medical PNG images using two different kernel shapes. The goal is to understand how each operation affects different types of anatomical structures.

---

## Operations

| Operation | What it does | How |
|---|---|---|
| Erosion | Shrinks white regions | Removes edge pixels of white areas |
| Dilation | Expands white regions | Adds pixels at edges of white areas |
| Opening | Removes small white dots | Erosion → then Dilation |
| Closing | Fills small black holes | Dilation → then Erosion |

## Kernel Shapes Used

```python
# Rectangular — affects all directions equally including corners
kernel_rect = cv.getStructuringElement(cv.MORPH_RECT, (5, 5))

# Elliptical — rounded shape, gentler on diagonals, smoother results
kernel_ellipse = cv.getStructuringElement(cv.MORPH_ELLIPSE, (5, 5))
```

---

## Key Code

```python
import cv2 as cv

img = cv.imread('dataset2/lung.png', cv.IMREAD_GRAYSCALE)
kernel = cv.getStructuringElement(cv.MORPH_RECT, (5, 5))

erosion  = cv.erode(img, kernel, iterations=1)
dilation = cv.dilate(img, kernel, iterations=1)
opening  = cv.morphologyEx(img, cv.MORPH_OPEN,  kernel)
closing  = cv.morphologyEx(img, cv.MORPH_CLOSE, kernel)
```

---

## Observations Per Image

**Lumbar Bones** — Erosion widens gaps between vertebrae and breaks thin connections. Dilation merges vertebrae together. Opening removes small bone fragments. Closing fills small gaps inside bone regions.

**Blood Vessels** — Erosion removes thinnest vessels, only thick ones survive. Dilation thickens all vessels and merges nearby ones. Opening simplifies the vascular network. Closing bridges small gaps between close vessels.

**Brain Tumor** — Erosion shrinks the white brain region. Dilation expands it and fills dark holes. Closing most useful — fills internal dark gaps cleanly.

**Lung** — Closing shows the most dramatic effect — small black holes (airways) inside the lungs get filled, producing clean solid lung shapes. Opening removes small white speckles.

## Rectangular vs Elliptical

The rectangular kernel is more aggressive — it affects corners too. The elliptical kernel produces smoother results that better match the natural curved shapes of anatomical structures.

---

## How to Run

1. Open `exercise2_task5.ipynb` in [Google Colab](https://colab.research.google.com)
2. Upload the 4 PNG files into a folder called `dataset2/`
3. Run all cells top to bottom
