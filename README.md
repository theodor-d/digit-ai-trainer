# Digit AI Trainer

A web-based handwritten digit recognition trainer built with Python, Flask, NumPy, and Pillow.

This project allows users to create their own digit dataset, train a neural network directly in the browser, monitor training progress in real time, and test predictions using either drawn digits or uploaded images.

## Features

- Draw digits on a built-in canvas
- Label and save training examples
- Upload handwritten digit images for training
- Train a neural network from scratch or continue training
- Real-time training metrics and loss/accuracy graphs
- Validation split with early stopping
- Automatic data augmentation
- Confusion matrix visualization
- Dataset import/export support
- Persistent model and dataset storage
- Top-3 prediction confidence scores

## Technologies Used

- Python
- Flask
- NumPy
- Pillow (PIL)
- HTML
- CSS
- JavaScript

## Neural Network Architecture

Input Layer:
- 784 neurons (28×28 pixels)

Hidden Layers:
- 128 neurons
- 64 neurons

Output Layer:
- 10 neurons (digits 0-9)

Additional training techniques:

- Leaky ReLU activation
- Softmax output
- Adam optimizer
- Dropout regularization
- Data augmentation
- Validation split
- Early stopping

## Dataset Management

The application includes built-in dataset tools:

- Add samples through drawing
- Upload image files
- Delete individual samples
- Clear entire dataset
- Export dataset as JSON
- Import dataset from JSON

The dataset and trained model are automatically saved locally using:

```text
ai_state_advanced.pkl
```

## Installation

### 1. Clone the repository

```bash
git clone https://github.com/yourusername/digit-ai-trainer.git
cd digit-ai-trainer
```

### 2. Install dependencies

```bash
pip install flask numpy pillow
```

### 3. Run the application

```bash
python app.py
```

### 4. Open in browser

```text
http://127.0.0.1:5000
```

## Usage

### Teaching the AI

1. Draw a digit on the canvas.
2. Enter the correct label (0-9).
3. Click **Save Drawing**.

Alternatively:

1. Upload handwritten digit images.
2. Assign a label.
3. Save them to the dataset.

### Training

Choose one of:

- **Train From Scratch**
- **Train Further**

The application will display:

- Training accuracy
- Validation accuracy
- Training loss
- Validation loss
- Gradient magnitude
- Dataset statistics

### Prediction

Draw a digit or upload an image and click:

```text
MAKE AI GUESS
```

The model returns:

- Top predicted digit
- Top 3 confidence scores
- Probability distribution for all digits

## Project Structure

```text
.
├── app.py
├── ai_state_advanced.pkl
├── README.md
```

## API Endpoints

| Endpoint | Method | Description |
|-----------|----------|-------------|
| `/` | GET | Main application |
| `/stats` | GET | Dataset statistics |
| `/teach` | POST | Save drawn sample |
| `/guess` | POST | Predict drawn sample |
| `/train_stream` | POST | Train model with live updates |
| `/teach_upload` | POST | Upload training images |
| `/guess_upload` | POST | Predict uploaded image |
| `/delete_sample` | POST | Delete dataset sample |
| `/clear_dataset` | POST | Remove all samples |
| `/export_dataset` | GET | Export dataset |
| `/import_dataset` | POST | Import dataset |

## Training Pipeline

1. Data collection
2. Image preprocessing
3. Digit centering and normalization
4. Data augmentation
5. Train/validation split
6. Neural network training
7. Early stopping evaluation
8. Model persistence

## Future Improvements

- Support for letters and symbols
- Convolutional neural network (CNN) architecture
- Multiple saved models
- Training history persistence
- GPU acceleration
- Dark mode interface

## License

MIT License

## Disclaimer

This project is designed for educational purposes and experimentation with machine learning concepts. It is not intended to compete with production-grade OCR systems such as MNIST-trained deep learning models.
