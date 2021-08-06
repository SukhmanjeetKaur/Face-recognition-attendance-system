# Face-recognition-attendance-system

Understanding the problem
Although many face recognition algorithms have been developed over the years, their speed and accuracy balance has not been quiet optimal . But some recent advancements have shown promise. A good example is Facebook, where they are able to tag you and your friends with just a few images of training and with accuracy as high as 98%. So how does this work . Today we will try to replicate similar results using a face recognition library developed by Adam Geitgey. Lets look at the 4 problems he explained in his article.

Face recognition is a series of several problems:

First, look at a picture and find all the faces in it
Second, focus on each face and be able to understand that even if a face is turned in a weird direction or in bad lighting, it is still the same person.
Third, be able to pick out unique features of the face that you can use to tell it apart from other people— like how big the eyes are, how long the face is, etc.
Finally, compare the unique features of that face to all the people you already know to determine the person’s name.

FACE RECOGNITION 

STEP 1: Import the relevant libraries 

cmake, dlib, numpy, face-recognition, opencv-python

import cv2
import face_recognition
import numpy as np 

STEP 2: Loading Images and Converting to RGB.

imgElon = face_recognition.load_image_file('ImagesBasic/Elon Musk.jpg')
imgElon = cv2.cvtColor(imgElon,cv2.COLOR_BGR2RGB)
imgTest = face_recognition.load_image_file('ImagesBasic/Elon Test.jpg')
imgTest = cv2.cvtColor(imgTest,cv2.COLOR_BGR2RGB)

![Elon Musk](https://user-images.githubusercontent.com/87376487/128454046-cdfd8839-782d-428c-b8d5-28e7b8867e26.jpg)
Elon Musk 

STEP 3: Find Faces Locations and Encodings

In this step we will use the true functionality of the face recognition library. First we will find the faces in our images . This is done using HOG (Histogram of Oriented Gradients) at the backend. Once we have the face they are warped to remove unwanted rotations. Then the image is feed to a pretrained neural network that out puts 128 measurements that are unique to that particular face. The parts that the model measures is not known as this is what the model learns by itself when it was trained. Lucky for us all this is done is just 2 lines of code. Once we have the face locations and the encodings we can draw rectangles around our faces.

faceLoc = face_recognition.face_locations(imgElon)[0]
encodeElon = face_recognition.face_encodings(imgElon)[0]
cv2.rectangle(imgElon,(faceLoc[3],faceLoc[0]),(faceLoc[1],faceLoc[2]),(255,0,255),2) # top, right, bottom, left
 
faceLocTest = face_recognition.face_locations(imgTest)[0]
encodeTest = face_recognition.face_encodings(imgTest)[0]
cv2.rectangle(imgTest,(faceLocTest[3],faceLocTest[0]),(faceLocTest[1],faceLocTest[2]),(255,0,255),2)

![testing](https://user-images.githubusercontent.com/87376487/128454581-1edb011d-468d-45ae-ad21-35c1d88ccdf3.png)





