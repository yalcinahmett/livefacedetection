# Live Face Detection Project
## I have benefited from this [article](https://www.datacamp.com/tutorial/face-detection-python-opencv).
## Let's go deep into codes.
> We are importing the OpenCV library.
```python
import cv2
```
> Now choosing an algorithm. In the article haarcascades algorithm used.
```python
face_classifier = cv2.CascadeClassifier(
    cv2.data.haarcascades + "haarcascade_frontalface_default.xml"
)
```
> It is for opening the default camera.
```python
video_capture = cv2.VideoCapture(0)
```
> We are initializing a function which can take video frames as input.
```python
def detect_bounding_box(vid):
    gray_image = cv2.cvtColor(vid, cv2.COLOR_BGR2GRAY)
    faces = face_classifier.detectMultiScale(gray_image, 1.1, 5, minSize=(40, 40))
    for (x, y, w, h) in faces:
        cv2.rectangle(vid, (x, y), (x + w, y + h), (0, 255, 0), 4)
    return faces
```
> We are checking whether the camera is working properly to finish the environment. If the user wants to quit can press 'q' to finish the environment manually.
```python
while True:

    result, video_frame = video_capture.read() 
    if result is False:
        break  

    faces = detect_bounding_box(
        video_frame
    )  

    cv2.imshow(
        "My Face Detection Project", video_frame
    )  

    if cv2.waitKey(1) & 0xFF == ord("q"):
        break
```
> After the loop has finished, we stop using camera and closing the app window.
```python
video_capture.release()
cv2.destroyAllWindows()
```
