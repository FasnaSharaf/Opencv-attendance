# FACE RECOGNITION ATTENDANCE SYSTEM
## TABLE OF CONTENTS
* [ABSTRACT](#abstract)
* [METHODOLOGY](#methodology)
* [FACE RECOGNITION - STEP BY STEP](#face-recognition---step-by-step)
* [RESULT](#result)

## ABSTRACT
We are living in a world where everything is automated and linked online. The internet of things, image processing, and machine learning are evolving day by day. Many systems have been completely changed due to this evolution to achieve more accurate results. The attendance system is a typical example of this transition, starting from the traditional signature on a paper sheet to face recognition. This project proposes a method of developing a comprehensive embedded class attendance system using facial recognition with showing whether the face of the person is the student for that specified class or not. This can be achieved by choosing one machine learning algorithm, feeding in data, and getting the result. It is implemented using python and OpenCV and we use computer/laptop camera for the input image of the students or a normal outer camera can also be used which has to be connected to the system. Once a person is identified through the encodings obtained from the image, their attendance (with time) is automatically added in the excel sheet.

## METHODOLOGY
The main task in this project is to make computers identify faces from the series of images we have already uploaded. But face recognition is really a series of several related problems:<br>
•	First, look at a picture and find all the faces in it<br>
•	Second, focus on each face and be able to understand that even if a face is turned in a weird direction or in bad lighting, it is still the same person.<br>
•	Third, be able to pick out unique features of the face that you can use to tell it apart from other people— like how big the eyes are, how long the face is, etc.<br>
•	Finally, compare the unique features of that face to all the people you already know to determine the person’s name.<br>
As a human, our brain is wired to do all of this automatically and instantly. But, computers are not capable of this kind of high-level generalization, so we have to teach them how to do each step in this process separately. We need to build a pipeline where we solve each step of face recognition separately and pass the result of the current step to the next step. 

## FACE RECOGNITION - STEP BY STEP

### Step 1: Finding all the Faces
The first step in our pipeline after uploading images is face detection.  We’ll break up the image into small squares of 16x16 pixels each. In each square, we’ll count up how many gradients point in each major direction (how many point up, point up-right, point right, etc…). Then we’ll replace that square in the image with the arrow directions that were the strongest. The end result is we turn the original image into a very simple representation that captures the basic structure of a face in a simple way. To find faces in this HOG image, all we have to do is find the part of our image that looks the most similar to a known HOG pattern that was extracted from a bunch of other training faces:

![image](https://github.com/FasnaSharaf/Opencv-attendance/assets/83363902/35e45334-f201-4b8e-875f-74227d56c93b)
<br>Therefore using this technique we can now easily locate a face.
### Step 2: Posing and Projecting Faces
Now we have isolated the faces in our image. But now we have to deal with the problem that faces turned different directions look totally different to a computer. To do this, we are going to use an algorithm called face landmark estimation. The basic idea is we will come up with 68 specific points (called landmarks) that exist on every face — the top of the chin, the outside edge of each eye, the inner edge of each eyebrow, etc. Then we will train a machine learning algorithm to be able to find these 68 specific points on any face:
![image](https://github.com/FasnaSharaf/Opencv-attendance/assets/83363902/cfd7e23a-8f6c-4293-9ca8-0daadeeafcf3)
<br>Now that we know were the eyes and mouth are, we’ll simply rotate, scale and shear the image so that the eyes and mouth are centered as best as possible.

### Step 3: Encoding Faces
We need a way to extract a few basic measurements from each face. Then we could measure our unknown face the same way and find the known face with the closest measurements. For example, we might measure the size of each ear, the spacing between the eyes, the length of the nose, etc. The solution is to train a Deep Convolutional Neural Network. 
<br>But instead of training the network to recognize pictures objects like we did last time, we are going to train it to generate 128 measurements for each face. We call the 128 measurements of each face an embedding. All we need to do ourselves is to run our face images through their pre-trained network to get the 128 measurements for each face.

### Step 4: Finding the person’s name from the encoding
This last step is actually the easiest step in the whole process. All we have to do is find the person in our database of known people who has the closest measurements to our test image. Then we would add those names in an excel sheet with the entry time.

## RESULT
For this project we made use of  these libraries:-
•	cmake<br>
•	dlib<br>
•	face_recognition<br>
•	numpy<br>
•	opencv-python<br>

First we created a sample project named ”basics.py” where we uploaded a sample image and we tested another image of the same person to test whether the computer can find a match or not. The result shown by it is:

![image](https://github.com/FasnaSharaf/Opencv-attendance/assets/83363902/0d6aee19-7da5-43e0-8efc-8f42afa0ef5e)
![image](https://github.com/FasnaSharaf/Opencv-attendance/assets/83363902/7168dd6d-32da-40b6-b858-83e3d40c0a70)
<br>First image is the sample image we uploaded and the second image is the image we used to test if the computer can predict a match or not. It is able to locate faces and it found a match in these two images. It gave 0.44 as the prediction value. Lower the value, higher is the match.

<br>Secondly, we created the real project of Facial attendance recognition system under the label “attendance-project.py” where we uploaded a series of images of different persons under images folder. Another image of a person (test image) included in the list was used to test if it could identify or not. 
We used for loop to retrieve each element of the list of images to test against the test image. If it finds a match, the name of the person and the time when the  match is made is recorded in an excel sheet.
![image](https://github.com/FasnaSharaf/Opencv-attendance/assets/83363902/ca9dedac-eb49-46a4-9a36-fa01d90ebcab)

