# Digit AI Trainer

A web-based handwritten digit recognition trainer that allows users to build custom datasets, train a neural network directly in the browser, and test predictions. 

**Tech Stack:** Python, Flask, NumPy, Pillow, HTML/CSS/JS

## Features & Architecture

* **Custom Datasets:** Draw or upload handwritten digits, label them, and manage your dataset (supports JSON import/export).
* **Browser-Based Training:** Train a custom Multi-Layer Perceptron (784-128-64-10) with real-time metrics, data augmentation, and early stopping.
* **Live Predictions:** Test the model via drawn or uploaded images, complete with top-3 confidence scores and a confusion matrix.
* **Persistent Storage:** Automatically saves your dataset and model states locally.

## Quick Start

### 1. Clone and enter the repository
```bash
git clone [https://github.com/yourusername/digit-ai-trainer.git](https://github.com/yourusername/digit-ai-trainer.git)
cd digit-ai-trainer

2. Install dependencies
Bash

pip install flask numpy pillow

3. Run the application
Bash

python app.py

4. Open your browser

Navigate to http://127.0.0.1:5000
Usage Guide

    Teach: Draw or upload a digit on the canvas, enter the correct label (0-9), and click Save.

    Train: Once you have enough samples, click Train From Scratch or Train Further to update the neural network.

    Predict: Draw or upload a new, unseen digit and click Make AI Guess to see the prediction results.

License: MIT License
Developed as part of ML self-exploration from the KMITL NextGen AI Camp #3.
