# Image-Handling-and-Pixel-Transformations-Using-OpenCV 

## AIM:
Write a Python program using OpenCV that performs the following tasks:

1) Read and Display an Image.  
2) Adjust the brightness of an image.  
3) Modify the image contrast.  
4) Generate a third image using bitwise operations.

## Software Required:
- Anaconda - Python 3.7
- Jupyter Notebook (for interactive development and execution)

## Algorithm:
### Step 1:
Load an image from your local directory and display it.

### Step 2:
Create a matrix of ones (with data type float64) to adjust brightness.

### Step 3:
Create brighter and darker images by adding and subtracting the matrix from the original image.  
Display the original, brighter, and darker images.

### Step 4:
Modify the image contrast by creating two higher contrast images using scaling factors of 1.1 and 1.2 (without overflow fix).  
Display the original, lower contrast, and higher contrast images.

### Step 5:
Split the image (boy.jpg) into B, G, R components and display the channels

## Program Developed By:
- **Name:** Sairam V 
- **Register Number:** 212225230237

  ### Ex. No. 01

#### 1. Read the image ('Eagle_in_Flight.jpg') using OpenCV imread() as a grayscale image.
```python
eagle_gray = cv2.imread("Eagle_in_Flight.jpg", cv2.IMREAD_GRAYSCALE)
assert eagle_gray is not None, "Eagle image not found"
print("Grayscale image loaded successfully")
```

#### 2. Print the image width, height & Channel.
```python
height, width = eagle_gray.shape
channels = 1
print(f"Width: {width} pixels\nHeight: {height} pixels\nChannels: {channels}")
```

#### 3. Display the image using matplotlib imshow().
```python
plt.figure(figsize=(9, 5))
plt.imshow(eagle_gray, cmap="gray", vmin=0, vmax=255)
plt.title("Eagle – Grayscale")
plt.axis("off")
plt.show()
```

#### 4. Save the image as a PNG file using OpenCV imwrite().
```python
saved = cv2.imwrite("eagle_grayscale.png", eagle_gray)
print("Saved eagle_grayscale.png:", saved)
```

#### 5. Read the saved image above as a color image using cv2.cvtColor().
```python
eagle_bgr = cv2.imread("eagle_grayscale.png", cv2.IMREAD_COLOR)
assert eagle_bgr is not None
eagle_from_png_rgb = cv2.cvtColor(eagle_bgr, cv2.COLOR_BGR2RGB)
print("Color image shape:", eagle_from_png_rgb.shape)
# For the following crop exercise, reload the original COLOR photograph.
eagle_original_bgr = cv2.imread("Eagle_in_Flight.jpg", cv2.IMREAD_COLOR)
eagle_rgb = cv2.cvtColor(eagle_original_bgr, cv2.COLOR_BGR2RGB)
```

#### 6. Display the Colour image using matplotlib imshow() & Print the image width, height & channel.
```python
plt.figure(figsize=(9, 5))
plt.imshow(eagle_rgb)
plt.title("Original Eagle – Color")
plt.axis("off")
plt.show()
h, w, c = eagle_rgb.shape
print(f"Width: {w}, Height: {h}, Channels: {c}")
```

#### 7. Crop the image to extract any specific (Eagle alone) object from the image.
```python
# Crop coordinates: rows 20:445 and columns 200:555.
# Change these values if you want a tighter crop.
eagle_crop = eagle_rgb[20:445, 200:555]
plt.figure(figsize=(7, 5))
plt.imshow(eagle_crop)
plt.title("Cropped Eagle")
plt.axis("off")
plt.show()
print("Cropped shape:", eagle_crop.shape)
```

#### 8. Resize the image up by a factor of 2x.
```python
eagle_resized = cv2.resize(eagle_crop, None, fx=2, fy=2, interpolation=cv2.INTER_CUBIC)
plt.figure(figsize=(7, 6))
plt.imshow(eagle_resized)
plt.title("Eagle – 2× Resize")
plt.axis("off")
plt.show()
print("Original crop:", eagle_crop.shape, "Resized:", eagle_resized.shape)
```

#### 9. Flip the cropped/resized image horizontally.
```python
eagle_flipped = cv2.flip(eagle_resized, 1)
plt.figure(figsize=(7, 6))
plt.imshow(eagle_flipped)
plt.title("Eagle – Horizontal Flip")
plt.axis("off")
plt.show()
```

#### 10. Read in the image ('Apollo-11-launch.jpg').
```python
apollo_bgr = cv2.imread("Apollo-11-launch.jpg", cv2.IMREAD_COLOR)
assert apollo_bgr is not None
apollo_rgb = cv2.cvtColor(apollo_bgr, cv2.COLOR_BGR2RGB)
print("Apollo image shape:", apollo_rgb.shape)
plt.figure(figsize=(10, 6))
plt.imshow(apollo_rgb)
plt.axis("off")
plt.show()
```

#### 11. Add the following text to the dark area at the bottom of the image (centered on the image):
```python
apollo_annotated = apollo_bgr.copy()
caption = "Apollo 11 Saturn V Launch, July 16, 1969"
h, w = apollo_annotated.shape[:2]
font = cv2.FONT_HERSHEY_SIMPLEX
scale = min(0.9, w / 1100)
thickness = 2
(text_w, text_h), baseline = cv2.getTextSize(caption, font, scale, thickness)
x = max(0, (w - text_w) // 2)
y = h - 30
cv2.putText(apollo_annotated, caption, (x, y), font, scale, (255, 255, 255), thickness, cv2.LINE_AA)
plt.figure(figsize=(11, 6))
plt.imshow(cv2.cvtColor(apollo_annotated, cv2.COLOR_BGR2RGB))
plt.title("Apollo 11 – Caption Added")
plt.axis("off")
plt.show()
```

#### 12. Draw a magenta rectangle that encompasses the launch tower and the rocket.
```python
# Approximate bounds for the supplied 1280 × 720 image.
# OpenCV drawing uses BGR: magenta = (255, 0, 255).
cv2.rectangle(apollo_annotated, (480, 55), (705, 630), (255, 0, 255), 4)
print("Magenta rectangle drawn")
```

#### 13. Display the final annotated image.
```python
plt.figure(figsize=(12, 7))
plt.imshow(cv2.cvtColor(apollo_annotated, cv2.COLOR_BGR2RGB))
plt.title("Apollo 11 – Annotated Launch")
plt.axis("off")
plt.show()
cv2.imwrite("apollo_annotated.png", apollo_annotated)
```

#### 14. Read the image ('Boy.jpg').
```python
boy_bgr = cv2.imread("boy.jpg", cv2.IMREAD_COLOR)
assert boy_bgr is not None
boy_rgb = cv2.cvtColor(boy_bgr, cv2.COLOR_BGR2RGB)
print("Boy image shape:", boy_rgb.shape)
plt.figure(figsize=(8, 5))
plt.imshow(boy_rgb)
plt.axis("off")
plt.show()```

#### 15. Adjust the brightness of the image.
```python
brightness_matrix = np.full(boy_rgb.shape, 50, dtype=np.uint8)
print("Brightness change:", brightness_matrix[0, 0])
```

#### 16. Create brighter and darker images.
```python
boy_brighter = cv2.add(boy_rgb, brightness_matrix)
boy_darker = cv2.subtract(boy_rgb, brightness_matrix)
```

#### 17. Display the images (Original Image, Darker Image, Brighter Image).
```python
fig, ax = plt.subplots(1, 3, figsize=(14, 4))
for a, im, title in zip(ax, [boy_rgb, boy_darker, boy_brighter], ["Original", "Darker (−50)", "Brighter (+50)"]):
    a.imshow(im); a.set_title(title); a.axis("off")
plt.tight_layout(); plt.show()
```

#### 18. Modify the image contrast.
```python
# Alpha > 1 increases contrast; alpha < 1 reduces contrast.
# Beta shifts brightness so the scaling is around mid-gray (128).
def adjust_contrast(image, alpha):
    return np.clip((image.astype(np.float32) - 128) * alpha + 128, 0, 255).astype(np.uint8)

boy_lower_contrast = adjust_contrast(boy_rgb, 0.8)
boy_higher_contrast = adjust_contrast(boy_rgb, 1.2)
# Additional 1.1× result, as mentioned in the supplied exercise:
boy_contrast_1_1 = adjust_contrast(boy_rgb, 1.1)
```

#### 19. Display the images (Original, Lower Contrast, Higher Contrast).
```python
fig, ax = plt.subplots(1, 3, figsize=(14, 4))
for a, im, title in zip(ax, [boy_rgb, boy_lower_contrast, boy_higher_contrast], ["Original", "Lower contrast (0.8×)", "Higher contrast (1.2×)"]):
    a.imshow(im); a.set_title(title); a.axis("off")
plt.tight_layout(); plt.show()
```

#### 20. Split the image (boy.jpg) into the B,G,R components & Display the channels.
```python
b, g, r = cv2.split(boy_bgr)
fig, ax = plt.subplots(1, 3, figsize=(13, 4))
for a, channel, title in zip(ax, [b, g, r], ["Blue", "Green", "Red"]):
    a.imshow(channel, cmap="gray", vmin=0, vmax=255); a.set_title(title); a.axis("off")
plt.tight_layout(); plt.show()
```

#### 21. Merged the R, G, B , displays along with the original image
```python
merged_rgb = cv2.merge([r, g, b])
fig, ax = plt.subplots(1, 2, figsize=(11, 4))
for a, im, title in zip(ax, [boy_rgb, merged_rgb], ["Original RGB", "Merged RGB"]):
    a.imshow(im); a.set_title(title); a.axis("off")
plt.tight_layout(); plt.show()
print("Identical:", np.array_equal(boy_rgb, merged_rgb))
```

#### 22. Split the image into the H, S, V components & Display the channels.
```python
hsv_img = cv2.cvtColor(boy_bgr, cv2.COLOR_BGR2HSV)
hue, saturation, value = cv2.split(hsv_img)
fig, ax = plt.subplots(1, 3, figsize=(13, 4))
for a, ch, title in zip(ax, [hue, saturation, value], ["Hue (0–179)", "Saturation (0–255)", "Value (0–255)"]):
    a.imshow(ch, cmap="gray"); a.set_title(title); a.axis("off")
plt.tight_layout(); plt.show()
```
#### 23. Merged the H, S, V, displays along with original image.
```python
merged_hsv = cv2.merge([hue, saturation, value])
restored_bgr = cv2.cvtColor(merged_hsv, cv2.COLOR_HSV2BGR)
restored_rgb = cv2.cvtColor(restored_bgr, cv2.COLOR_BGR2RGB)
fig, ax = plt.subplots(1, 2, figsize=(11, 4))
for a, im, title in zip(ax, [boy_rgb, restored_rgb], ["Original RGB", "Restored from HSV"]):
    a.imshow(im); a.set_title(title); a.axis("off")
plt.tight_layout(); plt.show()
print("Max rounding difference:", np.abs(boy_rgb.astype(int) - restored_rgb.astype(int)).max())
```

## Output:
- **i)** Read and Display an Image.  
- **ii)** Adjust Image Brightness.  
- **iii)** Modify Image Contrast.  
- **iv)** Generate Third Image Using Bitwise Operations.
<img width="660" height="218" alt="image" src="https://github.com/user-attachments/assets/415bcb43-48b7-4d52-8e2c-e635ba0b08d5" />
<img width="703" height="257" alt="image" src="https://github.com/user-attachments/assets/5e9165d0-b46f-4ba9-89c4-60cf6fdf71b1" />
<img width="680" height="644" alt="image" src="https://github.com/user-attachments/assets/8780982b-6af9-4a0c-b4bb-cc032f7a09b3" />

<img width="783" height="202" alt="image" src="https://github.com/user-attachments/assets/f714079e-d7ba-4650-b5f9-c409e84f03cc" />
<img width="756" height="272" alt="image" src="https://github.com/user-attachments/assets/356169f7-148f-4035-aadf-5e87eafc2ca1" />
<img width="828" height="647" alt="image" src="https://github.com/user-attachments/assets/5b4b8e94-37ba-4fdb-abeb-d47f9d937513" />
<img width="816" height="663" alt="image" src="https://github.com/user-attachments/assets/a577eac1-b389-4eb6-9316-a6c5ee1da9af" />
<img width="830" height="688" alt="image" src="https://github.com/user-attachments/assets/6a15ea19-d1ec-4546-8d93-fc16b0dbd0b6" />
<img width="800" height="642" alt="image" src="https://github.com/user-attachments/assets/8c426c69-b1be-41bc-93c1-a54744cdd5b8" />
<img width="827" height="666" alt="image" src="https://github.com/user-attachments/assets/78b69e4c-372e-4747-a2dd-7f02add5215e" />
<img width="843" height="658" alt="image" src="https://github.com/user-attachments/assets/b1580fd5-6f9e-4366-b6b9-288757887054" />
<img width="733" height="675" alt="image" src="https://github.com/user-attachments/assets/4591ec4d-2ae7-4c0b-9c32-7d48fa711e64" />
<img width="1246" height="678" alt="image" src="https://github.com/user-attachments/assets/34d8ef07-7b22-447a-bf2a-041d47d907c2" />
<img width="724" height="493" alt="image" src="https://github.com/user-attachments/assets/22b4a832-b8ca-41fe-b9dc-29c5bfcd2bd6" />
<img width="723" height="267" alt="image" src="https://github.com/user-attachments/assets/0df8258c-1f91-4973-9212-85b99e401ae3" />
<img width="693" height="384" alt="image" src="https://github.com/user-attachments/assets/fa9989f8-8560-421e-9923-8797e66e595b" />
<img width="713" height="398" alt="image" src="https://github.com/user-attachments/assets/f59c2ef6-d483-42f0-ad39-bf156889e767" />
<img width="706" height="497" alt="image" src="https://github.com/user-attachments/assets/1416e196-d4ec-4fc6-88d3-97e72b1ff246" />
<img width="718" height="433" alt="image" src="https://github.com/user-attachments/assets/e1bb2283-6551-4227-92f0-65c07aab3f51" />
<img width="713" height="558" alt="image" src="https://github.com/user-attachments/assets/a00d433a-36b3-4160-893e-460354c14fe6" />

## Result:
Thus, the images were read, displayed, brightness and contrast adjustments were made, and bitwise operations were performed successfully using the Python program.

