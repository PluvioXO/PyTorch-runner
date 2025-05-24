# FIFO Model Marking & Sanitization Library (PyTorch)

## Project Overview
This project provides a FIFO (First-In-First-Out) organization system to distribute the computational marking (evaluation) of multiple PyTorch ML models, efficiently balancing compute load across available resources. It is designed to streamline large-scale model evaluation workflows, particularly in research or production environments where many models must be assessed in parallel or sequence.

Additionally, the library offers robust sanitization utilities tailored to both the file type (expecting all saved models as `.pt`) and the specific model architecture (e.g., Logistic Regression, Neural Networks, Transformers, etc.), ensuring safe and consistent model handling.

## Key Features
- **FIFO Queue System:** Distributes model evaluation tasks in a first-come, first-served manner.
- **PyTorch Native:** Built specifically for PyTorch models and workflows.
- **Model-Type-Aware Sanitization:** Cleans and validates models based on their architecture and file format.
- **Scalable:** Handles large numbers of models and distributes compute load efficiently.
- **Extensible:** Easily add support for new model types or sanitization routines.

## Use Cases
- **Academic Research:** Batch evaluation of student-submitted PyTorch models for automated grading.
- **Model Benchmarking:** Fairly compare multiple model architectures on the same dataset using a consistent evaluation pipeline.
- **Production Model Validation:** Sanitize and validate incoming models before deployment in a production environment.
- **Collaborative Projects:** Manage and evaluate models from multiple contributors in a shared queue.

## Installation
```bash
pip install fifo-model-marking  # Replace with actual package name if published
```
Or clone the repository:
```bash
git clone <repo-url>
cd <repo-directory>
pip install -r requirements.txt
```

## Usage Example
```python
from fifo_model_marking import FIFOModelQueue, sanitize_model

# Initialize the FIFO queue
eval_queue = FIFOModelQueue()

# Add models to the queue
eval_queue.enqueue('model1.mdf5')
eval_queue.enqueue('model2.mdf5')

# Process models in FIFO order
while not eval_queue.is_empty():
    model_path = eval_queue.dequeue()
    sanitized_model = sanitize_model(model_path)
    # Evaluate the sanitized model
    # ... (your evaluation code here)
```

## Supported Model Types
- Logistic Regression (PyTorch)
- Feedforward Neural Networks
- Convolutional Neural Networks (CNNs)
- Recurrent Neural Networks (RNNs)
- Transformers
- Custom PyTorch models (with extension)

## Sanitization Details
- **File Type Check:** Ensures models are saved in `.pt` format.
- **Architecture Validation:** Confirms the model matches expected PyTorch architecture.
- **Parameter Inspection:** Checks for NaNs, Infs, or other anomalies in model weights.
- **Security:** Removes or flags unsafe code or attributes in model files.

## Contribution Guidelines
Contributions are welcome! Please open an issue or submit a pull request. For major changes, discuss them in an issue first.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/YourFeature`)
3. Commit your changes (`git commit -am 'Add new feature'`)
4. Push to the branch (`git push origin feature/YourFeature`)
5. Open a pull request

## License
[MIT License](LICENSE)
