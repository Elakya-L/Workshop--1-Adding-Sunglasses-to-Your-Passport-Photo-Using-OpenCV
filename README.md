# Workshop--1-Adding-Sunglasses-to-Your-Passport-Photo-Using-OpenCV-Completion-requirements
# Name: Elakya L
# Reg No: 212225230066
Sturdy Octo Disco is a fun project that adds sunglasses to photos using image processing.

Welcome to Sturdy Octo Disco, a fun and creative project designed to overlay sunglasses on individual passport photos! This repository demonstrates how to use image processing techniques to create a playful transformation, making ordinary photos look extraordinary. Whether you're a beginner exploring computer vision or just looking for a quirky project to try, this is for you!

## Features:
- Detects the face in an image.
- Places a stylish sunglass overlay perfectly on the face.
- Works seamlessly with individual passport-size photos.
- Customizable for different sunglasses styles or photo types.

## Technologies Used:
- Python
- OpenCV for image processing
- Numpy for array manipulations

## How to Use:
1. Clone this repository.
2. Add your passport-sized photo to the `images` folder.
3. Run the script to see your "cool" transformation!

## Applications:
- Learning basic image processing techniques.
- Adding flair to your photos for fun.
- Practicing computer vision workflows.

Feel free to fork, contribute, or customize this project for your creative needs!

## PROGRAM

### Step 1: Import Required Libraries
Import OpenCV, NumPy, and Matplotlib to perform image processing and display the results.

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt
```

### Step 2: Read and Display the Face Image
Load the original face image and display it using Matplotlib.

```python
faceImage = cv2.imread('3.jpeg')

plt.imshow(faceImage[:, :, ::-1])
plt.title("Face")
plt.axis('off')
plt.show()

print(faceImage.shape)
```

### Step 3: Read and Display the Sunglasses Image
Load the sunglasses image with its alpha channel to preserve transparency information.

```python
glassPNG = cv2.imread('sunglass.png', -1)

plt.imshow(glassPNG[:, :, :3][:, :, ::-1])
plt.title("Sunglasses")
plt.axis('off')
plt.show()
```

### Step 4: Resize the Sunglasses Image
Resize the sunglasses to fit the eye region of the face.

```python
glassPNG = cv2.resize(glassPNG, (190, 50))

print("Image Dimension =", glassPNG.shape)
```

### Step 5: Separate Color and Alpha Channels
Separate the color information and alpha channel from the sunglasses image.

```python
glassBGR = glassPNG[:, :, 0:3]
glassMask1 = glassPNG[:, :, 3]

plt.figure(figsize=[12, 6])

plt.subplot(121)
plt.imshow(glassBGR[:, :, ::-1])
plt.title("Sunglasses Color Channels")
plt.axis('off')

plt.subplot(122)
plt.imshow(glassMask1, cmap='gray')
plt.title("Sunglasses Alpha Channel")
plt.axis('off')

plt.show()
```

### Step 6: Place Sunglasses on the Face
Copy the face image and place the sunglasses over the selected eye region.

```python
# Make a copy
#faceWithGlassesNaive = resized_faceImage.copy()
faceWithGlassesNaive = faceImage.copy()

# Replace the eye region with the sunglass image
faceWithGlassesNaive[100:140,65:195]=glassBGR

plt.imshow(faceWithGlassesNaive[...,::-1])
```

### Step 7: Apply Masking to the Sunglasses
Use the alpha channel to create a mask, remove the corresponding background pixels, and combine the sunglasses with the eye region.

```python
glassMask = cv2.merge((glassMask1,glassMask1,glassMask1))

glassMask = np.uint8(glassMask/255)

faceWithGlassesArithmetic = faceImage.copy()

eyeROI= faceWithGlassesArithmetic[100:140,65:195]

maskedEye = cv2.multiply(eyeROI,(1-  glassMask ))

maskedGlass = cv2.multiply(glassBGR,glassMask)

eyeRoiFinal = cv2.add(maskedEye, maskedGlass)
plt.figure(figsize=[20,20])
plt.subplot(131);plt.imshow(maskedEye[...,::-1]);plt.title("Masked Eye Region")
plt.subplot(132);plt.imshow(maskedGlass[...,::-1]);plt.title("Masked Sunglass Region")
plt.subplot(133);plt.imshow(eyeRoiFinal[...,::-1]);plt.title("Augmented Eye and Sunglass")

```

### Step 8: Display the Final Image
Replace the selected eye region with the combined image and compare the original face with the final result.

```python
faceWithGlassesArithmetic[100:140,65:195]=eyeRoiFinal

plt.figure(figsize=[20,20]);
plt.subplot(121);plt.imshow(faceImage[:,:,::-1]); plt.title("Original Image");
plt.subplot(122);plt.imshow(faceWithGlassesArithmetic[:,:,::-1]);plt.title("With Sunglasses");
```

## OUTPUT

The following outputs are obtained:

1. Original face image displayed using OpenCV and Matplotlib.
   
<img width="464" height="187" alt="image" src="https://github.com/user-attachments/assets/838eb6f3-1fa6-4837-a485-d7fe49f731d2" />

2. Sunglasses image loaded and displayed.

<img width="266" height="281" alt="image" src="https://github.com/user-attachments/assets/1dca587d-52b5-49f5-84fd-115fe172162d" />

3. Color and alpha channels of the sunglasses displayed separately.

<img width="695" height="121" alt="image" src="https://github.com/user-attachments/assets/dd410136-7c4a-404d-87ed-26da0aae7cf1" />
  
4. Sunglasses placed over the eye region.

<img width="248" height="271" alt="image" src="https://github.com/user-attachments/assets/534dfc27-10ab-4df8-8bab-3f6910a4438b" />


5. Combined eye and sunglasses region obtained using masking and arithmetic operations.

<img width="687" height="89" alt="image" src="https://github.com/user-attachments/assets/0e7c4de4-8e73-40da-bdc1-8549f72588c2" />

6. Original and modified face images displayed side by side.

<img width="509" height="296" alt="image" src="https://github.com/user-attachments/assets/18c38210-1224-4d27-ac45-ac5135f5626b" />


## RESULT

Thus, sunglasses were added to a face image using Python, OpenCV, NumPy, and Matplotlib. The experiment demonstrated image loading, resizing, alpha-channel separation, masking, pixel arithmetic, and image blending to overlay sunglasses onto the eye region.
