# DIGITAL_IMAGE_PROCESSING_TECHNIQUES-WS1
# Sturdy-Octo-Disco-Adding-Sunglasses-for-a-Cool-New-Look

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
## PROGRAM:
### CODE FOR IMPORTING:
~~~
import cv2
import numpy as np
import matplotlib.pyplot as plt
~~~
### CODE:
~~~
# Load the Face Image
faceImage = cv2.imread(r"C:\Users\acer\Downloads\dip_ex-pareesh.jpeg")
plt.imshow(faceImage[:,:,::-1]);plt.title("Face")
~~~
## OUTPUT:
<img width="1107" height="700" alt="image" src="https://github.com/user-attachments/assets/a008edfa-c4cf-4b50-81a5-cf252e28b4ea" />


### CODE:
~~~
faceImage.shape
#resized_faceImage.shape
faceImage.shape
~~~
## OUTPUT:
<img width="643" height="142" alt="image" src="https://github.com/user-attachments/assets/204f23b6-cc4e-49f0-b2ec-61765cba4ee6" />
### CODE:
~~~
# Load the Sunglass image with Alpha channel
# (http://pluspng.com/sunglass-png-1104.html)
glassPNG = cv2.imread(r"C:\Users\acer\Downloads\sunglass-png-aviator-sunglass-png-clipart-3381.png",-1)
plt.imshow(glassPNG[:,:,::-1]);plt.title("glassPNG")
~~~
## OUTPUT:
<img width="930" height="512" alt="image" src="https://github.com/user-attachments/assets/42656078-57e8-427e-8d05-cc6fa0e0f46a" />


### CODE:
~~~
# Resize the image to fit over the eye region
glassPNG = cv2.resize(glassPNG,(360,100))
print("image Dimension ={}".format(glassPNG.shape))
~~~
## OUTPUT:
<img width="647" height="131" alt="image" src="https://github.com/user-attachments/assets/64909b97-14bc-4dcc-b29a-2b1b2bf70fd0" />

### CODE:
~~~
# Separate the Color and alpha channels
glassBGR = glassPNG[:,:,0:3]
glassMask1 = glassPNG[:,:,3]

----
# Display the images for clarity
plt.figure(figsize=[15,15])
plt.subplot(121);plt.imshow(glassBGR[:,:,::-1]);plt.title('Sunglass Color channels');
plt.subplot(122);plt.imshow(glassMask1,cmap='gray');plt.title('Sunglass Alpha channel');
~~~
## OUTPUT:
<img width="471" height="88" alt="image" src="https://github.com/user-attachments/assets/9b7197d3-bf7d-4fcb-a992-12d2ec738be4" />
<img width="1132" height="257" alt="image" src="https://github.com/user-attachments/assets/a291c45c-f7cd-411e-8539-fc543b141ae0" />


### CODE:
~~~
# Make a copy
#faceWithGlassesNaive = resized_faceImage.copy()
faceWithGlassesNaive = faceImage.copy()

# Replace the eye region with the sunglass image
faceWithGlassesNaive[825:925,110:470]=glassBGR

plt.imshow(faceWithGlassesNaive[...,::-1])
~~~
## OUTPUT:
<img width="766" height="527" alt="image" src="https://github.com/user-attachments/assets/13401ef8-3fe0-4651-8ff8-6b460e388d0d" />


### CODE:
~~~
# Make the dimensions of the mask same as the input image.
# Since Face Image is a 3-channel image, we create a 3 channel image for the mask
glassMask = cv2.merge((glassMask1,glassMask1,glassMask1))

# Make the values [0,1] since we are using arithmetic operations
glassMask = np.uint8(glassMask/255)

# Make a copy
faceWithGlassesArithmetic = faceImage.copy()

# Get the eye region from the face image
eyeROI= faceWithGlassesArithmetic[825:925,110:470]

# Use the mask to create the masked eye region
maskedEye = cv2.multiply(eyeROI,(1-  glassMask ))

# Use the mask to create the masked sunglass region
maskedGlass = cv2.multiply(glassBGR,glassMask)

# Combine the Sunglass in the Eye Region to get the augmented image
eyeRoiFinal = cv2.add(maskedEye, maskedGlass)

# Display the intermediate results
plt.figure(figsize=[20,20])
plt.subplot(131);plt.imshow(maskedEye[...,::-1]);plt.title("Masked Eye Region")
plt.subplot(132);plt.imshow(maskedGlass[...,::-1]);plt.title("Masked Sunglass Region")
plt.subplot(133);plt.imshow(eyeRoiFinal[...,::-1]);plt.title("Augmented Eye and Sunglass")
~~~
## OUTPUT:
<img width="1146" height="683" alt="image" src="https://github.com/user-attachments/assets/20b9469b-9643-46a8-9f15-5aa22c2a8688" />

### CODE:
~~~
# Replace the eye ROI with the output from the previous section
faceWithGlassesArithmetic[825:925,110:470]=eyeRoiFinal

# Display the final result
plt.figure(figsize=[20,20]);
plt.subplot(121);plt.imshow(faceImage[:,:,::-1]); plt.title("Original Image");
plt.subplot(122);plt.imshow(faceWithGlassesArithmetic[:,:,::-1]);plt.title("With Sunglasses");
~~~
## OUTPUT:
<img width="1108" height="492" alt="image" src="https://github.com/user-attachments/assets/9fde2ba2-64e6-45f6-b1da-68c23a36567b" />


## Applications:
- Learning basic image processing techniques.
- Adding flair to your photos for fun.
- Practicing computer vision workflows.

Feel free to fork, contribute, or customize this project for your creative needs!
