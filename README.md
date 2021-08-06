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

STEP 4: Compare Faces and Find Distance

Once we have the encodings for both faces, then we can compare these 128 measurements of these two faces to find similarities. To compare the package uses one of the most common machine Learning methods linear SVM classifier. We can use the compare_faces function to find if the faces match. This function returns True or False. Similarly we can use the face_distance function to find how likely is the faces match in terms of numbers. This is helpul particularly when there are multiple faces to detect from.

![CODE4](https://user-images.githubusercontent.com/87376487/128455357-8fa5fbce-bc52-4e35-894b-cb578d40dff0.png)

If we run this with the test image we get the value True, indicating that the face found is of Elon Musk. The is distance between the faces is 0.35. The lower the distance the better the match.

![ELONTEST](https://user-images.githubusercontent.com/87376487/128455475-e56038b5-4690-44a3-adc4-65645f8eb68f.png)

Let try it with another testing image. This time we will test it with an image of Bill Gates. As we can see the result is False and the distance is much higher than before indicating a bad match.

![bill gates](https://user-images.githubusercontent.com/87376487/128455679-bd782075-4a3b-4230-ad51-c22878c9f092.png)

ATTENDANCE PROJECT

Now using the methods we have seen above, we will develop an attendance system where the user is automatically logged when they are detected in the camera. We will store the name along with the time when they appeared.


Importing Images

As we have imported before we can use the same face_recognition.load_image_file() function to import our images. But when we have multiple images, importing them individually can become messy. Therefore we will write a script to import all images in a given folder at once. For this we will need the os library so we will import that first. We will store all the images in one list and their names in another.

![CODE 5](https://user-images.githubusercontent.com/87376487/128456167-66eacf2a-eaef-4a79-86d6-94155dff0e5c.png)

Compute Encodings

Now that we have a list of images we can iterate through those and create a corresponding encoded list for known faces. To do this we will create a function. As earlier we will first convert it into RGB and then find its encoding using the face_encodings() function. Then we will append each encoding to our list.

The While loop

The while loop is created to run the webcam. But before the while loop we have to create a video capture object so that we can grab frames from the webcam.

cap = cv2.VideoCapture(0)

Webcam Image

First we will read the image from the webcam and then resize it to quarter the size. This is done to increase the speed of the system. Even though the image being used is 1/4 th of the original, we will still use the original size while displaying. Next we will convert it to RGB.

Webcam Encodings

Once we have the webcam frame we will find all the faces in our image. The face_locations function is used for this purpose. Later we will find the face_encodings as well.

Find Matches

Now we can match the current face encodings to our known faces encoding list to find the matches. We will also compute the distance. This is done to find the best match in case more than one face is detected at a time.

Marking Attendance

Lastly we are going to add the automated attendance code. We will start by writing a function that requires only one input which is the name of the user. First we open our Attendance file which is in csv format. Then we read all the lines and iterate through each line using a for loop. Next we can split using comma ‘,’. This will allow us to get the first element which is the name of the user. If the user in the camera already has an entry in the file then nothing will happen. On the other hand if the user is new then the name of the user along with the current time stamp will be stored. We can use the datetime class in the date time package to get the current time.

![ATTENDANCE](https://user-images.githubusercontent.com/87376487/128456437-63f687ca-a6b6-48c6-8738-1b309d4ff78b.png)

Comma Separated Values Storied in Attendance File

Completed Successfully! Thank You! 











