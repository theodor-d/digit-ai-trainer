# Digit AI Trainer

A browser-based handwritten digit recognition app — draw digits, train your own neural network, and watch it learn in real time. Built from scratch using Python, Flask, NumPy, and Pillow (no ML frameworks).

## Features

* **Custom Dataset** — Draw or upload digits (0–9), label them, and manage your dataset with JSON import/export
* **Pure NumPy Neural Network** — Full MLP trained with backprop + Adam, no PyTorch/TensorFlow
* **Real-Time Training Graph** — Live accuracy, loss, and gradient norm plotted per epoch
* **Data Augmentation** — Rotation, scaling, elastic distortion, noise, and morphological filters
* **Early Stopping** — Auto-halts when validation loss stagnates to prevent overfitting
* **Confusion Matrix** — Per-class accuracy breakdown after training
* **Persistent Storage** — Dataset and weights auto-saved as .pkl between sessions

## Quick Start


git clone [https://github.com/theodor-d/digit-ai-trainer.git](https://github.com/theodor-d/digit-ai-trainer.git)
cd digit-ai-trainer
pip install flask numpy pillow
python ai_paint.py

Open http://127.0.0.1:5000 in your browser.
How to Use

    Teach — Draw a digit on the canvas, enter the label (0–9), click Save Drawing. Repeat for multiple digits. Aim for 10–20 samples per class.

    Train — Click Train From Scratch (reset + train) or Train Further (continue from current weights). Watch live metrics on the graph.

    Predict — Draw a new digit and click Make AI Guess to see top-3 predictions with confidence scores.

How It Works
Neural Network Architecture

Input (784) → Hidden 1 (128) → Hidden 2 (64) → Output (10)

Weights initialized with He initialization (W ~ N(0, sqrt(2/fan_in))) to keep gradient variance stable across layers.
Activations

    Hidden layers: Leaky ReLU — f(z) = z if z > 0, else 0.01z
    Prevents dead neurons by allowing a small gradient for negative inputs.

    Output layer: Softmax — converts raw scores into a probability distribution over 10 digit classes.

Loss Function

Categorical Cross-Entropy:

    L = -1/N · Σ y_true · log(P + 1e-9)

A small epsilon (1e-9) is added to avoid log(0). A loss of ~2.3 means the model is no better than random guessing (log(10) for 10 classes). Below 0.3 indicates good convergence.
Backpropagation & Gradients

The output gradient is simply (P - y_true) / N — the prediction error. This is backpropagated layer by layer using the chain rule.

Gradient Norm (plotted in orange on the graph) measures the total update magnitude across all parameters:

    ‖∇‖ = sqrt( Σ ‖∂L/∂W_i‖² )

High norm → large updates (early training). Near zero → converged or stuck.
Adam Optimizer

Adaptive learning rate per parameter using running estimates of gradient mean and variance:

m_t = 0.9·m + 0.1·g          (1st moment)
v_t = 0.999·v + 0.001·g²     (2nd moment)
θ  -= lr · m̂ / (√v̂ + 1e-8)

Learning rate: 0.001. Adam handles noisy gradients well, making it ideal for small or unbalanced datasets.
Regularization

    Dropout (keep=0.9): Randomly zeros 10% of activations each batch during training (inverted dropout). Forces the model not to rely on any single neuron.

    Early Stopping (patience=18): Training halts if validation loss doesn't improve by 1e-4 for 18 consecutive epochs.

Data Augmentation

Each sample is augmented ×2 per epoch, tripling the effective dataset size:
Technique	Probability
Random rotation (±12°)	100%
Random scaling (88–110%)	100%
Random translation (±2px)	100%
Elastic distortion	45%
Stroke dilation (MaxFilter)	35%
Stroke erosion (MinFilter)	20%
Gaussian noise σ=0.025	100%

After augmentation, each image is re-centered using the pixel bounding box to match MNIST-style preprocessing.
Live Training Graph
Metric	Color	Line
Train Accuracy	🟢 Green	Solid
Val Accuracy	🔵 Blue	Dashed
Train Loss	🔴 Red	Solid
Val Loss	🟣 Purple	Dashed
Gradient Norm	🟠 Orange	Solid

Healthy training: both losses decrease, accuracy rises, val and train metrics stay close. If val loss rises while train loss falls → overfitting (collect more data).
Project Structure

digit-ai-trainer/
├── ai_paint.py              # All-in-one: neural network, training loop, Flask API, and UI
├── ai_state_advanced.pkl    # Auto-saved dataset + model weights (created on first run)
└── README.md

Background

Built as self-exploration during my KMITL NextGen AI Camp #3 2026 from the ground up — implementing every component (forward pass, backprop, Adam, augmentation) using only NumPy.
