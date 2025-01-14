Here's a more detailed README.md specifically for your code:

# TFLite Circuit Breaker Detector Metadata Writer

A Python application for adding metadata to a TensorFlow Lite model specifically designed for circuit breaker detection. The application provides two different approaches for metadata addition, allowing flexibility in how model information is specified.

## Description

This tool adds essential metadata to TFLite models, including:
- Input/output tensor specifications
- Normalization parameters
- Model information
- Label mappings
- Color space information

## Prerequisites

```bash
pip install tflite-support==0.4.4
```

## Project Structure

```
├── metadata_writer.py          # Main script
├── breaker_detector.tflite     # Your input TFLite model
├── labels.txt                  # Generated labels file
└── breaker_detector_with_metadata.tflite  # Output model with metadata
```

## Implementation Methods

### 1. Detailed Metadata Addition (add_metadata_to_tflite)
This method provides fine-grained control over metadata specifications:
- Detailed model information
- Custom input tensor specifications
- Custom output tensor specifications
- Specific normalization parameters ([0.0], [255.0])

```python
add_metadata_to_tflite(
    model_path="breaker_detector.tflite",
    label_file="labels.txt",
    output_path="breaker_detector_with_metadata.tflite"
)
```

### 2. Simplified Inference-Optimized Method (add_metadata_to_tflite2)
This method uses standardized parameters for inference:
- Simplified metadata addition
- Standard normalization parameters ([127.5, 127.5, 127.5])
- Automatic tensor configuration

```python
add_metadata_to_tflite2(
    model_path="breaker_detector.tflite",
    label_file="labels.txt",
    output_path="breaker_detector_with_metadata.tflite"
)
```

## Model Specifications

### Input Requirements
- Image Size: 224 x 224 pixels
- Channels: 3 (RGB)
- Pixel Value Range: [0, 1]

### Output Format
- Bounding boxes in [x, y, width, height] format

## Usage

1. Place your TFLite model in the project directory as `breaker_detector.tflite`

2. Run the script:
```bash
python metadata_writer.py
```

The script will:
- Generate a labels.txt file with "circuit_breaker" class
- Add metadata to your model using the inference-optimized method
- Save the new model as `breaker_detector_with_metadata.tflite`

## Normalization Parameters

### Method 1 (Detailed)
- Mean: [0.0]
- Standard Deviation: [255.0]

### Method 2 (Inference-Optimized)
- Mean: [127.5, 127.5, 127.5]
- Standard Deviation: [127.5, 127.5, 127.5]

## Metadata Information

The detailed method includes:
- Model Name: "Circuit Breaker Detector"
- Version: "v1"
- Description: "Detects circuit breakers in images and returns their bounding boxes"
- License: "Apache License. Version 2.0"

## Error Handling

Common issues to watch for:
- File path errors: Ensure model and label files are in the correct location
- Tensor type mismatches: Verify model input/output specifications
- Normalization parameter format: Must be lists, not single values

## Dependencies

- tflite-support==0.4.4
- TensorFlow Lite
