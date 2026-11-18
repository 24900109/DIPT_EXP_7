#  Lane Detection

##  Aim

To implement a basic lane detection pipeline using OpenCV by completing missing code segments at specified locations.

---

## Learning Objective

* Understand each stage of image processing
* Learn how to build a complete computer vision pipeline
* Practice writing code in guided sections

**Important Instruction:**
👉 Write code **ONLY in places marked as `# Your Code Here`**
👉 Do NOT modify any other part of the code

---

##  Software Used

* Anaconda – Python 3.7
* Jupyter Notebook / VS Code
* OpenCV (cv2)
* NumPy
* Matplotlib

---

##  Algorithm & Explanation

---
##  Developed By

* **Name:** KIRUTHIKA N
* **Register No:** 212224230127

###  Step 1: Import Libraries

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt
```

---

###  Step 2: Read the Image

```python
image = cv2.imread("tulip.jpg")

if image is None:
    raise FileNotFoundError("Could not load 'lan_img1.jpg'. Check the file path.")
image_rgb = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)

```

---

###  Step 3: Convert to Grayscale

```python
gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

```

---

###  Step 4: Display Images

```python
plt.figure(figsize=(10,5))
plt.figure(figsize=(10,5))

plt.figure(figsize=(10, 5))

plt.subplot(1, 2, 1)
plt.imshow(image_rgb)
plt.title("Original Image")
plt.axis("off")

plt.subplot(1, 2, 2)
plt.imshow(gray, cmap="gray")
plt.title("Grayscale Image")
plt.axis("off")

plt.tight_layout()
plt.show()

```
<img width="1267" height="445" alt="1" src="https://github.com/user-attachments/assets/418262b1-435f-4b48-a566-967cd145ceda" />

---

###  Step 5: Thresholding

```python


threshold = 
threshold = 150
_, thresh = cv2.threshold(gray, threshold, 255, cv2.THRESH_BINARY)

plt.figure(figsize=(6, 6))
plt.imshow(thresh, cmap="gray")
plt.title("Thresholded Image")
plt.axis("off")
plt.show()

```
<img width="607" height="386" alt="2" src="https://github.com/user-attachments/assets/65281b29-6dee-4fc7-92d7-7dd55ee0c0c6" />

---

###  Step 6: Region of Interest (ROI)

```python

height, width = thresh.shape

roi_vertices = np.array([[
    (int(0.1 * width), height),
    (int(0.45 * width), int(0.6 * height)),
    (int(0.55 * width), int(0.6 * height)),
    (int(0.9 * width), height)
]], dtype=np.int32)

mask = np.zeros_like(thresh)
cv2.fillPoly(mask, roi_vertices, 255)
roi_masked = cv2.bitwise_and(thresh, mask)

plt.figure(figsize=(6, 6))
plt.imshow(roi_masked, cmap="gray")
plt.title("ROI Masked Image")
plt.axis("off")
plt.show()
```
<img width="622" height="388" alt="3" src="https://github.com/user-attachments/assets/8f327624-4e32-43ff-9756-5cde5a044470" />


### Step 7: Edge Detection (Canny)

```python


edges = cv2.Canny(roi_masked, 50, 150)
plt.figure(figsize=(6, 6))
plt.imshow(edges, cmap="gray")
plt.title("Edge Detected Image")
plt.axis("off")
plt.show()

```
<img width="627" height="387" alt="4" src="https://github.com/user-attachments/assets/5357ddb9-6b2a-45c9-b37e-80f818a6bf6b" />

---

###  Step 8: Gaussian Blur

```python


smoothed = cv2.GaussianBlur(edges, (5, 5), 0)
plt.figure(figsize=(6, 6))
plt.imshow(smoothed, cmap="gray")
plt.title("Smoothed (Blurred) Edge Image")
plt.axis("off")
plt.show()

```
<img width="622" height="387" alt="5" src="https://github.com/user-attachments/assets/a1abb5f4-08d3-456c-83d9-e6f295ecabb9" />

---

###  Step 9: Hough Transform

```python
lines = cv2.HoughLinesP(
    smoothed,
    rho=2,
    theta=np.pi / 180,
    threshold=50,
    minLineLength=40,
    maxLineGap=100
)

line_image = np.zeros_like(image)
if lines is not None:
    for line in lines:
        x1, y1, x2, y2 = line[0]
        cv2.line(line_image, (x1, y1), (x2, y2), (255, 0, 0), 5)

line_image_rgb = cv2.cvtColor(line_image, cv2.COLOR_BGR2RGB)

plt.figure(figsize=(6, 6))
plt.imshow(line_image_rgb)
plt.title("Detected Lines")
plt.axis("off")
plt.show()

```
<img width="622" height="390" alt="6" src="https://github.com/user-attachments/assets/8a7fe9d5-b18c-492b-9543-069b8985d1f1" />

---

### Step 10: Lane Detection Logic

```
final_output = cv2.addWeighted(image, 0.8, line_image, 1.0, 0.0)
final_output_rgb = cv2.cvtColor(final_output, cv2.COLOR_BGR2RGB)
plt.figure(figsize=(6, 6))
plt.imshow(final_output_rgb)
plt.title("Final Lane Detection Output")
plt.axis("off")
plt.show()
```

<img width="610" height="391" alt="7" src="https://github.com/user-attachments/assets/05a04230-84a9-47b5-94d6-1720850aaea0" />

---


## Result

Thus, the lane detection pipeline is successfully implemented by completing the missing code sections. The system detects and highlights lane lines effectively.

---
