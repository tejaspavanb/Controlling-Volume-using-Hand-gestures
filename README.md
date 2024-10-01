Thank you for sharing the code. Here's an improved version of the **Read Me** page to reflect this specific code example for **"Controlling Volume Using Hand Gestures"**.

---

# **Controlling Volume Using Hand Gestures**

## **Overview**

This project demonstrates how to control your computer's system volume using hand gestures detected via a webcam. It uses **OpenCV** and **MediaPipe** to track hand landmarks and **PyCaw** for volume control. The distance between the thumb and index finger is used to set the volume level, and the percentage of volume is displayed on the screen.

## **Features**

- **Real-time Hand Gesture Recognition**: Detects hand movements and adjusts system volume based on finger gestures.
- **Volume Indicator**: Shows a visual bar representing the volume level.
- **Simple Hand Landmarks**: Uses the thumb and index finger to adjust the volume, with circles and lines drawn to indicate their positions.
  
## **Technologies Used**

- **OpenCV**: For capturing webcam input and rendering video frames.
- **MediaPipe**: For detecting and tracking hand landmarks in real-time.
- **PyCaw**: For controlling the system volume on Windows.
- **Python**: Programming language used for the logic.

## **Requirements**

- Python 3.x
- OpenCV (`cv2`)
- MediaPipe
- PyCaw
- NumPy
- comtypes (for PyCaw)

To install the required dependencies, run the following command:

```bash
pip install opencv-python mediapipe pycaw numpy comtypes
```

## **Installation Instructions**

1. Clone the repository:
   
   ```bash
   git clone https://github.com/tejaspavanb/Controlling-Volume-using-Hand-gestures.git
   cd Controlling-Volume-using-Hand-gestures
   ```

2. Install the necessary Python libraries:
   
   ```bash
   pip install -r requirements.txt
   ```

3. Run the program:
   
   ```bash
   python volume_control.py
   ```

## **How It Works**

1. **Webcam Capture**: The webcam captures the video stream using `cv2.VideoCapture()`.
   
2. **Hand Detection**: Using **MediaPipe**, hand landmarks are detected, focusing on the thumb and index finger.
   
3. **Gesture Recognition**: The distance between the thumb and index finger is used to adjust the volume. The closer the fingers are, the lower the volume, and vice versa.

4. **Volume Control**: The distance is mapped to a volume range using `np.interp()`. PyCaw is used to set the system volume programmatically.

5. **Visual Feedback**: Circles are drawn around the thumb and index finger, and a line is drawn between them. A volume bar and percentage are displayed on the screen to give real-time feedback.

## **Usage Instructions**

1. Run the Python script after installation.
2. Make sure your hand is visible in the camera feed.
3. Perform the following gesture:
   - **Thumb and Index Finger**: Move your thumb and index finger closer together or further apart to adjust the volume. The volume level will adjust accordingly in real-time.
4. Press the **spacebar** to stop the program.

## **Code Explanation**

- **Hand Detection**: The script uses **MediaPipe Hands** for detecting the position of 21 hand landmarks. 
   ```python
   mpHands = mp.solutions.hands
   hands = mpHands.Hands()
   mpDraw = mp.solutions.drawing_utils
   ```
   
- **Volume Control**: The volume is controlled by **PyCaw**, which accesses the system's audio interface.
   ```python
   devices = AudioUtilities.GetSpeakers()
   interface = devices.Activate(IAudioEndpointVolume._iid_, CLSCTX_ALL, None)
   volume = cast(interface, POINTER(IAudioEndpointVolume))
   volMin, volMax = volume.GetVolumeRange()[:2]
   ```

- **Gesture Logic**: The distance between the thumb and index finger is calculated using the Euclidean distance formula:
   ```python
   length = hypot(x2 - x1, y2 - y1)
   ```

- **Volume Mapping**: The hand gesture range is mapped to the system volume range using `np.interp()`, allowing smooth control:
   ```python
   vol = np.interp(length, [30, 350], [volMin, volMax])
   ```

- **Volume Bar and Percentage Display**: A visual bar is drawn to indicate the volume level, and a percentage is displayed on the screen:
   ```python
   cv2.rectangle(img, (50, int(volbar)), (85, 400), (0, 0, 255), cv2.FILLED)
   cv2.putText(img, f"{int(volper)}%", (10, 40), cv2.FONT_ITALIC, 1, (0, 255, 98), 3)
   ```

## **Customization**

- You can change the gesture-to-volume mapping by adjusting the thresholds in the code. 
- You can modify the visual elements, such as the color or size of the drawn circles and lines, by updating the parameters in the `cv2.circle()` and `cv2.line()` functions.

## **Known Issues**

- Accuracy may decrease in poor lighting conditions or if the hand is not properly visible to the camera.
- Background noise (other objects or patterns) can interfere with hand detection.

## **Contributing**

Feel free to fork the repository, improve the code, and submit a pull request. Suggestions and feedback are welcome!

## **License**

This project is licensed under the MIT License.

---

This should provide a comprehensive **Read Me** for users interested in running and understanding the project!
