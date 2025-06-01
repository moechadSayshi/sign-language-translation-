# sign language translation using open cv and tensorflow

## project overview

This repository contains a final-year machine learning project that implements real-time sign language recognition using OpenCV for image capture and processing, and a TensorFlow model exported from Google’s Teachable Machine for gesture classification. It allows users to collect custom hand‐sign images, train a model via Teachable Machine, and perform live inference to translate hand signs into text labels.

## features

* **real-time hand detection and cropping**
  Uses `cvzone.HandTrackingModule.HandDetector` to locate a single hand in the webcam feed, crop it with a fixed padding (`offset = 20`), and place it on a blank (white) background of size 300 × 300 pixels, preserving the sign’s aspect ratio.

* **custom dataset collection**
  The `datacollection.py` script captures and saves hand‐sign images to a specified folder (e.g., `data/<label>`). Pressing the `s` key saves the current cropped‐and‐resized frame with a timestamped filename.

* **tensorflow-based classification (Teachable Machine)**
  A model exported from Google’s Teachable Machine (`model/keras_model.h5`) and its accompanying `labels.txt` file are loaded by the `cvzone.ClassificationModule.Classifier`. During inference, the model predicts the most likely sign class and displays the predicted label overlayed on the webcam feed.

* **simple, modular architecture**

  * `datacollection.py`: Collect and store images for each sign class.
  * `test1.py`: Load the Teachable Machine–exported model & labels, then run live inference on webcam input.

## project structure

```
.
├── data/
│   └── <label_1>/
│       ├── Image_<timestamp>.jpg
│       └── ...
│   └── <label_2>/
│       └── ...
├── model/
│   ├── keras_model.h5
│   └── labels.txt
├── datacollection.py
├── test1.py
└── README.md
```

## prerequisites

* **python 3.7+**
* **opencv-python** (`cv2`)
* **cvzone** (version ≥ 1.5.0)
* **tensorflow** (≥ 2.x)
* **numpy** (≥ 1.19)
* **mediapipe**
* a working webcam (USB or built‐in)

Install dependencies:

```bash
pip install opencv-python cvzone tensorflow numpy mediapipe
```

## data collection workflow

1. **create a folder for each sign label**
2. **set `folder` path** in `datacollection.py` for the target label
3. **run script** with `python datacollection.py` and press `s` to save images
4. **repeat for each class**

## model training (google teachable machine)

1. Visit [Teachable Machine](https://teachablemachine.withgoogle.com/)
2. Create an **Image Project → Standard Image Model**
3. Upload your collected images for each class
4. Click **Train Model**
5. After training, click **Export Model → TensorFlow (Keras)**
6. Download and extract the `.zip` containing:

   * `keras_model.h5`
   * `labels.txt`
7. Place both files into the `model/` directory of your project

## running the real-time inference demo

1. Ensure `model/keras_model.h5` and `model/labels.txt` exist
2. Install dependencies (see above)
3. Run:

```bash
python test1.py
```

4. The webcam feed will show hand detection and predicted sign labels

## dependencies

```text
opencv-python
cvzone
tensorflow
numpy
mediapipe
```

## notes & tips

* Collect 200–300 images per sign class for best performance
* Good lighting and centered hands improve detection accuracy
* If you update labels, regenerate `labels.txt` via Teachable Machine

## acknowledgements

* Google Teachable Machine
* cvzone (by HGLab)
* MediaPipe
* TensorFlow/Keras

## license

This project is released under the MIT License. Add a LICENSE file if needed.
