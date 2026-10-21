# Augmented-Reality: ArUco poster overlay

Detects an ArUco marker in a room photo and warps a poster image onto it with a perspective transform (OpenCV).
Coursework project; a 10-page report is included (`Augumented_Reality.pdf`).

## Algorithm
1. Load the room image and the poster image (`cv2.imread`).
2. Detect the ArUco marker (`DICT_7X7_250`) and take its four corner points. Only the first detected marker is used.
3. Compute the poster's central rectangle (width/6 x height/4) as the source quadrilateral.
   This only avoids distortion if the poster has a 3:2 aspect ratio.
4. Compute the homography (`cv2.getPerspectiveTransform`) and warp the poster (`cv2.warpPerspective`).
5. Mask out the target region in the room image (`np.zeros_like`, `cv2.fillPoly`) and merge with `cv2.bitwise_and` / `cv2.bitwise_or`.

## Run
```bash
pip install opencv-python numpy   # the aruco API used needs a recent OpenCV (4.7 or newer)
python augmented_reality.py
```
Expected inputs (not included in this repository): `aruco_images/room50.jpg` (room photo with an ArUco marker) and `aruco_images/poster.jpg`.
The result is written to `aug_images/new_img1.jpg`.

## Status and limitations
- Demonstrated on a few classroom images; no quantitative evaluation. Alignment errors came from poor marker detection, perspective distortion and lighting (see report).
- Sample input images are not included, so the script cannot run from a clean clone yet.
