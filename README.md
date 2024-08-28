# Dartboard Score Prediction

## Overview
This project focuses on creating a computer vision program that analyzes images of dartboards and calculates the score based on the position of darts. The project is divided into two tasks, each focusing on different aspects of the dartboard and scoring.

## Project Structure

### Task 1: Dart Detection and Position Estimation
The objective of Task 1 is to detect the number of darts and their positions on a classic dartboard with 9 concentric circles. The approach involves the following steps:

1. **Image Processing**:
   - Convert the dartboard image to Hue, Saturation, and Brightness (HSB) format.
   - Blur the image and split it into background and foreground.
   - Use `cv2.findContours` to find contours and filter them based on area.
   - Fit ellipses to the filtered contours representing the concentric circles.

2. **Bullseye Detection**:
   - Add the smallest ellipse (the bullseye) manually, based on empirical observations.

3. **Dart Detection**:
   - Load a pre-trained YOLOv8 model and fine-tune it with dart training images (annotations done with RoboFlow).
   - Detect the bounding boxes for darts using the trained model.

4. **Dart Position Estimation**:
   - Estimate the dart's position using the left edge of the bounding box and half its height.
   - Determine which concentric circle the dart falls into using `cv2.pointPolygonTest`.

5. **Output**:
   - Write the results for all darts in each image to `Radu_Madalin_407/Task1`.

### Task 2: Dartboard Score Calculation
Task 2 extends the functionality to calculate the score on a dartboard that includes double and triple rings, and the bullseye is divided into inner and outer sections.

1. **Image Processing**:
   - Similar to Task 1, but with additional steps to differentiate between single, double, and triple zones.
   - Masks are created for red, green, white, and black pixels to identify different dartboard regions.

2. **Ellipse Detection**:
   - Extract the ellipse that fits the whole dartboard using the black mask.
   - Use the red and green masks to extract the inner and outer bullseye ellipses, respectively.

3. **Dart Detection**:
   - As in Task 1, use YOLOv8 to detect darts.

4. **Score Calculation**:
   - Estimate the dart's tip position with corrections for darts that may be lodged obliquely.
   - Calculate the angle of the dart tip relative to the dartboard center and determine the sector.
   - Determine the score by checking if the dart is in the bullseye, double, or triple zones, and assign the score accordingly.

5. **Output**:
   - Write the results for all darts in each image to `Radu_Madalin_407/Task2`.

### Running the Project
To run the project:
1. Clone the repository:
    ```bash
    git clone https://github.com/madalin312/darts_scoring
    ```
2. Ensure that the notebook is located in the same folder as the training, validation, and auxiliary data to avoid any file path issues.
3. Run the Jupyter Notebook provided to execute the tasks and generate the results.

### Dependencies
The project relies on the following libraries:
- OpenCV
- YOLOv8
- TensorFlow
- RoboFlow

Ensure that these dependencies are installed in your environment. You can install the required packages using:
```bash
pip install -r requirements.txt
