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

![code](https://user-images.githubusercontent.com/87376487/128454815-8961d283-ee11-4415-ab92-2eafcbd16210.png)

STEP 2: Loading Images and Converting to RGB.

![code2](https://user-images.githubusercontent.com/87376487/128454967-bdb13579-f7b7-49d3-9f08-7b8d81ce35bc.png)

![Elon Musk](https://user-images.githubusercontent.com/87376487/128454046-cdfd8839-782d-428c-b8d5-28e7b8867e26.jpg)

STEP 3: Find Faces Locations and Encodings

In this step we will use the true functionality of the face recognition library. First we will find the faces in our images . This is done using HOG (Histogram of Oriented Gradients) at the backend. Once we have the face they are warped to remove unwanted rotations. Then the image is feed to a pretrained neural network that out puts 128 measurements that are unique to that particular face. The parts that the model measures is not known as this is what the model learns by itself when it was trained. Lucky for us all this is done is just 2 lines of code. Once we have the face locations and the encodings we can draw rectangles around our faces.

![code3](https://user-images.githubusercontent.com/87376487/128455106-e78f7efd-70e5-4e3e-beeb-ef2a40594bd6.png)

![testing](https://user-images.githubusercontent.com/87376487/128454581-1edb011d-468d-45ae-ad21-35c1d88ccdf3.png)





