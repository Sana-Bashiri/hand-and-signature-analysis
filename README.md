# Hand and Signature Analysis with Computer Vision


Two academic projects collected in `Github-Yolov11`: custom hand detection, hand-landmark visualization, and exploratory signature-region detection.

**Model note:** The code uses **YOLOv8n**, alongside MediaPipe and OpenCV.

## Contents

| Location | Contents |
| --- | --- |
| [English report](Report/Project_Report.pdf) | Academic methodology, recorded results, figures, limitations |
| [Report source](Report/Project_Report.tex) | Editable LaTeX version |
| [Code](Code) | Three unchanged notebooks with descriptive filenames |
| [Readme.tex](Readme.tex) | Detailed project guide, required inputs, dependencies, and execution notes |

## Notebooks

| Notebook | Original name | Purpose |
| --- | --- | --- |
| [Hand YOLO training](Code/hand_detection_yolov8_training.ipynb) | `ravesh2.ipynb` | Dataset split, two independent 30-epoch YOLOv8n training runs, and video inference |
| [Hand landmarks](Code/hand_landmark_detection_mediapipe.ipynb) | `Untitled2.ipynb` | MediaPipe hand landmarks on an image and a video |
| [Signature exploration](Code/signature_detection_contours_yolov8.ipynb) | `signatureproject.ipynb` | CLAHE, Otsu thresholding, contour filtering, a pretrained YOLO branch, and TensorBoard |

Only notebook filenames changed. Contents, outputs, metadata, and comments are preserved byte for byte. The [SHA-256 manifest](Code/Notebook_Provenance.json) records each mapping.

## Recorded observations

- **Hand YOLO:** 10 training images and 3 validation images. The saved video run has no detections across 174 frames at confidence 0.30. Best-checkpoint mAP@0.50 is 0.995, but printed precision is only 0.00333; the report discusses the limits of these small-set validation numbers.
- **MediaPipe:** Image and video processing are implemented. The original report describes success, while the supplied notebook retains missing-package errors.
- **Signature:** Saved YOLO output has zero boxes; an embedded TensorBoard scalar records zero contour candidates. The YOLO fallback is the pretrained `book` class, so it is not a trained signature detector. Cached image and scalar timestamps differ.

## Running the original workflows

Use Google Colab or a compatible IPython notebook environment. Provide inputs before running cells in order. See [Readme.tex](Readme.tex) for full details.

| Notebook | Required inputs | Main dependencies |
| --- | --- | --- |
| Hand YOLO | `/content/hands_dataset.zip`; `hand_video.mp4` in the working directory | Ultralytics, OpenCV, scikit-learn, IPython |
| Hand landmarks | `/content/hand.jpg`; `/content/videohand.mp4` | MediaPipe exposing `mp.solutions.hands`, OpenCV, Matplotlib; Colab for download |
| Signature | `/content/signa.jpg` | Ultralytics, OpenCV, NumPy, PyTorch, TensorBoard |

The dataset archive, original inputs, trained weights, generated hand videos, and standalone TensorBoard event files were not supplied. The report includes a signature image recovered from notebook metadata and a validation chart reconstructed from saved logs. No new training or inference was performed.

The hand dataset-preparation cell moves paired `.jpg`/`.txt` files; use a fresh archive when repeating preparation. Its glob excludes `.jpeg`. The MediaPipe setup cell does not install MediaPipe. Exact historical environments are documented in the report; they are not a tested dependency lockfile.

## Documents

The finished report uses black text and tables on white pages, with color confined to figures. To compile the editable report source, run LaTeX from `Report/` so the figure paths resolve. 
