# TensorFlow Lite Example: On-Device Model Personalization

This repository is a clone of the official [TensorFlow Lite Model Personalization Example](https://github.com/tensorflow/examples/tree/master/lite/examples/model_personalization).

It illustrates how to personalize a TFLite model on-device without sending any data to a server. This approach builds on existing TFLite functionality to ensure data privacy and low latency, and it can be adapted for various tasks and models.

## 🔗 References

* **Principal Reference:** [TensorFlow Lite Model Personalization Example (Official)](https://github.com/tensorflow/examples/tree/master/lite/examples/model_personalization)
* **Documentation:** [On-Device Training with LiteRT](https://ai.google.dev/edge/litert/conversion/tensorflow/build/ondevice_training)

---

## 🛠️ Requirements & Environment

The following environment was used for the execution of this project. While the code may be compatible with other versions, these are recommended for reproducibility.

* **Python Version:** `3.9`
* **Android Studio** (for the mobile application)
* **Physical Android Device** (with camera)

### Python Dependencies
To match the environment used in this repository, install the following specific versions:

```
tensorflow==2.8.0
numpy==1.23.5
matplotlib==3.9.4
protobuf==3.20.3

```

You can install them via pip:

```bash
pip install tensorflow==2.8.0 numpy==1.23.5 matplotlib==3.9.4 protobuf==3.20.3

```

---

## 🚀 Quickstart

### 1. Prepare the TFLite Model

The python scripts for model generation are located in the `transfer_learning` directory.

```bash
cd transfer_learning

# Create and activate a virtual environment (Recommended)
python3.9 -m venv env
source env/bin/activate

# Install dependencies
pip install -r requirements.txt
# OR manually install the specific versions listed above if requirements.txt differs

# Generate the model flatbuffer file `model.tflite`
python generate_training_model.py

# Return to root and copy the model to the Android assets folder
cd ..
cp transfer_learning/model.tflite android/app/src/main/assets/model/model.tflite

```

### 2. Install and Run the Android Application

You can build and run the application using Android Studio or the command line.

**Option A: Android Studio**

1. Open Android Studio.
2. Import the project by pointing to the top-level `build.gradle` file in the `android` folder.
3. Connect your Android device.
4. Click the **Run** button.

**Option B: Command Line (Linux)**
Switch to the `android` folder and build using the Gradle wrapper:

```bash
cd android
./gradlew build

```

Install the APK to your connected device:

```bash
adb install ./app/build/outputs/apk/debug/app-debug.apk

```

---

## 📱 How to Use the App

<p align="center">
<img src="app_screenshot.png" alt="app_screenshot" width="350"/>
</p>

1. **Capture Data:** The buttons at the bottom correspond to classes the app will learn. Press a button to take a photo and associate it with that class.
2. **Collect Samples:** Take at least **10 images per class** (vary the background and orientation) for better results.
3. **Train:** Once enough samples are collected, the "Train" button will become active. Press it and wait for the loss to decrease.
4. **Inference:** Press "Pause" and switch to inference mode (top-right). Point the camera at objects to see real-time predictions.

---

## 📂 Project Structure

* **`transfer_learning/`**: Python CLI for defining and generating the personalizable model.
* **`android/transfer_api/`**: A simplified Android library for handling the on-device training logic.
* **`android/app/`**: The demo application that implements the UI and uses the transfer API.

### Customizing the Model

You can modify the model architecture in `transfer_learning/generate_training_model.py`. The system uses two distinct parts:

1. **Base Model:** (Fixed weights) Typically a pre-trained feature extractor (e.g., `MobileNetV2`).
2. **Head Model:** (Trainable weights) The layers trained on-device (e.g., Dense + Softmax).

*Note: The optimizer is currently set to `Adam` with `learning_rate=0.001`.*
