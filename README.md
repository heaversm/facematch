# Webcam Face Match

[Demo](https://webcam-facematch.netlify.app/)

## Instructions

You can compare faces with the select dropdowns provided.

To compare a face with a webcam image, click Start Camera - allow access to the camera via the browser dialog, and bring your face as close as possible to the camera, looking straight ahead, before clicking the Take Photo button.

## Description

This prototype uses a subset of functionality from [face-api](https://github.com/justadudewhohacks/face-api.js#interface-face-detection), trained on this [BBT Dataset](https://github.com/Daniel595/Jetson_nano_face_recognition/tree/master/faces/train/datasets/bbt) combined with [webcam-easy](https://github.com/bensonruan/webcam-easy) to take a photo of you via the webcam, and compare it to a list of faces to determine similarity.

The prototype was built to test basic feasibility of asserting one's own identity for use in self-attested verifiable credentials via a web interface.

## Machine Learning

Underneath the hood, face-api.js is using:

**Library**: TensorflowJS

**Architecture**: Resnet-34

**Neural Network**: Convolutional Neural Network

**Models**:

- faceLandmark68Net
- faceLandmark68TinyNet
- faceRecognitionNet
- ssdMobilenetv1
- tinyFaceDetector
- tinyYolo

**Methods**

- `computeFaceDescriptor(input)`
- `euclideanDistance(descriptor1,descriptor2)`
- `LabeledFaceDescriptors(className,descriptors)`
- `FaceMatcher(labeledFaceDescriptors)`

**Process**:

The webcam image is drawn to canvas every frame. When you take a photo, the canvas image is run through MobileNetV1's Single Shot Detection to identify the face in the frame.

Facial Landmarks are detected and used for alignment (faceLandmark68TinyNet), and a facial description is built. 

The Face Descriptor is a feature vector with 128 values - basically a huge array of embeddings (numbers) used to calculate the Euclidean Distance between the webcam photo and the chosen comparison photo from the dropdown, leveraging faceRecognitionNet.



