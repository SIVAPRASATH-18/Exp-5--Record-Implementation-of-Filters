# Exp-5--Record-Implementation-of-Filters

## Aim

To write a Python program using OpenCV to apply different smoothing filters (Averaging, Weighted Averaging, Gaussian, Median) and sharpening filters (Laplacian Kernel and Laplacian Operator) for image enhancement, and display each result separately along with the original image for comparison.

---

## The program performs the following operations:

- Read and display an input image  
- Apply Averaging filter  
- Apply Weighted Averaging filter  
- Apply Gaussian filter  
- Apply Median filter  
- Apply Laplacian sharpening using kernel  
- Apply Laplacian operator  
- Display all outputs for comparison  

---

##  Software Used

- Anaconda – Python 3.7  
- Jupyter Notebook / VS Code  
- OpenCV (cv2)  
- NumPy  
- Matplotlib  

---

##  Algorithm

### Step 1:
Import the required libraries: OpenCV, NumPy, and Matplotlib.

### Step 2:
Read the input image (e.g., `image.jpg`).

### Step 3:
Convert the image from BGR to RGB format for display.

### Step 4:
Apply Averaging Filter using `cv2.blur()`.

### Step 5:
Apply Weighted Averaging Filter using a custom kernel with `cv2.filter2D()`.

### Step 6:
Apply Gaussian Filter using `cv2.GaussianBlur()`.

### Step 7:
Apply Median Filter using `cv2.medianBlur()`.

### Step 8:
Apply Laplacian Sharpening using Kernel with `cv2.filter2D()`.

### Step 9:
Convert image to grayscale and apply Laplacian Operator using `cv2.Laplacian()`.

### Step 10:
Display all filtered images using a grid layout for comparison.

---

## Program

```py

import cv2
import numpy as np
import matplotlib.pyplot as plt

# Step 1: Read image
img = cv2.imread("car.jpg")

if img is None:
    raise FileNotFoundError("Please check that image.jpg exists.")

# Step 2: Convert BGR to RGB
rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)

# Step 3: Averaging Filter - stronger blur
averaging = cv2.blur(rgb, (15, 15))

# Step 4: Weighted Averaging Filter
kernel = np.array([
    [1, 1, 2, 1, 1],
    [1, 2, 4, 2, 1],
    [2, 4, 8, 4, 2],
    [1, 2, 4, 2, 1],
    [1, 1, 2, 1, 1]
], dtype=np.float32)

kernel = kernel / kernel.sum()
weighted = cv2.filter2D(rgb, -1, kernel)

# Step 5: Gaussian Filter - stronger smoothing
gaussian = cv2.GaussianBlur(rgb, (21, 21), 5)

# Step 6: Median Filter
median = cv2.medianBlur(rgb, 9)

# Step 7: Laplacian Sharpening
sharp_kernel = np.array([
    [0, -1, 0],
    [-1, 5, -1],
    [0, -1, 0]
], dtype=np.float32)

sharpened = cv2.filter2D(rgb, -1, sharp_kernel)

# Step 8: Grayscale conversion
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

# Step 9: Laplacian Operator
lap = cv2.Laplacian(gray, cv2.CV_64F, ksize=3)
laplacian = cv2.convertScaleAbs(lap)

# Normalize Laplacian for better edge visibility
laplacian = cv2.normalize(
    laplacian, None, 0, 255, cv2.NORM_MINMAX
)

# Step 10: Display results
images = [
    (rgb, "Original Image"),
    (averaging, "Averaging Filter (15x15)"),
    (weighted, "Weighted Averaging"),
    (gaussian, "Gaussian Filter"),
    (median, "Median Filter (9x9)"),
    (sharpened, "Laplacian Sharpening"),
    (gray, "Grayscale Image"),
    (laplacian, "Laplacian Edge Detection")
]

plt.figure(figsize=(16, 9))

for i, (image, title) in enumerate(images):
    plt.subplot(2, 4, i + 1)

    if image.ndim == 2:
        plt.imshow(image, cmap="gray", vmin=0, vmax=255)
    else:
        plt.imshow(image)

    plt.title(title)
    plt.axis("off")

plt.tight_layout()
plt.show()


```

##  Developed By

- **Name:** SIVAPRASATH B 
- **Register No:** 212225230268

---

##  Output


<img width="1305" height="493" alt="image" src="https://github.com/user-attachments/assets/0385deeb-e14b-46eb-b61c-c9efe89c66c8" />



### Smoothing Filters

- Averaging filter produces blurred image  
- Weighted averaging provides smoother result with less distortion  
- Gaussian filter preserves edges better while reducing noise  
- Median filter removes salt-and-pepper noise effectively  

###  Sharpening Filters

- Laplacian kernel enhances edges and fine details  
- Laplacian operator detects edges clearly in grayscale  

---

##  Result

Thus, smoothing filters and sharpening filters are successfully implemented using OpenCV.

The smoothing filters reduce noise and improve image quality, while sharpening filters enhance edges and details for better feature extraction.
