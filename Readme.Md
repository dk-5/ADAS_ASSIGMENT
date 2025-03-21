Advanced Driver Assistance System (ADAS)

This repository demonstrates an ADAS system that leverages object detection, sensor fusion, and collision avoidance to improve vehicle safety. The system processes data from cameras and LIDAR to identify potential hazards and make informed decisions for collision prevention.

Table of Contents

Data Processing

Sensor Fusion Techniques

Camera and LIDAR Integration

Collision Avoidance Algorithm

References

Data Processing

Data Acquisition

Images are loaded from the KITTI dataset, processing the first 1000 images to simulate a continuous data stream.

Pre-processing

Each image is processed as follows:

Read via OpenCV.

Converted from BGR (OpenCV default) to RGB, as required by the YOLOv5 model.

Inference

The YOLOv5 model performs object detection, generating bounding boxes, confidence scores, and class indices.

Storing Results

Detection results are stored in a dictionary and saved as a JSON file.

Processed images with overlayed bounding boxes and labels are saved for further analysis.

Sensor Fusion Techniques

Calibration-Based Projection

KITTI calibration files are used to extract the P2 matrix for projecting 3D LIDAR points into the 2D camera space.

Correlation via Center Matching

Simulated radar points are projected into the image plane and matched with bounding box centers using Euclidean distance.

Detections are fused if they fall within a threshold distance (e.g., 50 pixels).

The fused center is calculated as the average of the detection center and the projected radar point.

Feature Refinement

The code extracts contours from each detection's ROI to refine the object’s shape for better accuracy.

Camera and LIDAR Integration

Synchronization via Calibration

Calibration matrices ensure both LIDAR points and camera detections share a unified coordinate system.

Matching Detections to Radar Data

Bounding box centers from the camera are matched to projected radar points based on proximity.

Fused Data Structure

Each correlated detection includes:

Original camera detection bounding box.

Corresponding radar object (with its 3D centroid).

Projected radar point on the image.

Fused center calculated from the average of the camera and radar points.

Collision Avoidance Algorithm

Obstruction Identification

The system identifies potential hazards based on object classes like "person," "car," "truck," etc.

Decision Making

If a fused object matches obstruction criteria, the system triggers a collision risk warning.

Actions include automated braking, lane change avoidance, or adaptive cruise control (ACC).

Results Visualization

Red Bounding Boxes: Original camera detections.

Green Circles: Radar-projected points.

Yellow Markers: Fused detection centers.

Warning text overlays indicate potential collision risks.

References

Data Source

KITTI Dataset: http://www.cvlibs.net/datasets/kitti/

Object Detection Model

YOLOv5 by Ultralytics: https://github.com/ultralytics/yolov5

Sensor Fusion Techniques

KITTI Calibration Documentation: http://www.cvlibs.net/datasets/kitti/setup.php

Libraries and Frameworks

PyTorch: https://pytorch.org/

OpenCV: https://opencv.org/

NumPy: https://numpy.org/

Collision Avoidance Techniques

Path Planning Algorithms (e.g., RRT, A)**: https://github.com/AtsushiSakai/PythonRobotics

Obstacle Detection Research Papers: Search on IEEE Xplore or arXiv for cutting-edge techniques.

