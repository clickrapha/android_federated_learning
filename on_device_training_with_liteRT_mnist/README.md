# On-Device Training with LiteRT (TensorFlow Lite)

This repository demonstrates how to build and convert a TensorFlow model that supports **on-device training** using LiteRT (formerly TensorFlow Lite).

By enabling training directly on edge devices, this workflow allows for:

* **Personalization:** Adapt models to individual user data without cloud processing.
* **Privacy:** Keep sensitive data local to the device.
* **Efficiency:** Reduce latency and bandwidth usage by minimizing server dependence.

## 🛠️ Requirements

The following environment was used for this execution. While other versions may be compatible, these are recommended for reproducibility.

**Python Version:** `3.9`

**Dependencies:**

```txt
protobuf==3.20.3
matplotlib==3.9.4
numpy==1.23.5
tensorflow==2.8.0

```

To install the dependencies, you can run:

```bash
pip install tensorflow==2.8.0 numpy==1.23.5 matplotlib==3.9.4 protobuf==3.20.3

```

## 🚀 Usage

1. **Define and Convert:**
Run the jypyter notebook script to train the base model and convert it.

2. **Output:**
The execution will generate a model file ready for deployment on Android  edge devices.

## 🔗 References

* [On-Device Training with LiteRT (Google AI Edge)](https://ai.google.dev/edge/litert/conversion/tensorflow/build/ondevice_training) – Official documentation and tutorial.
