# AWS Face Mask Detection

A Python implementation that uses AWS Rekognition to detect and visualize face mask usage in images. The script draws color-coded bounding boxes to indicate proper mask usage, improper mask usage, and absence of masks.

## Prerequisites

- Python 3.8.8
- AWS Account with Rekognition access
- AWS Access Key and Secret Key
- boto3 library
- Pillow (PIL) library

## Installation

```bash
pip install boto3
pip install Pillow
```

## Required Libraries
```python
import boto3
import io
from PIL import Image, ImageDraw, ExifTags, ImageColor
```

## Configuration

Set up your AWS credentials:
```python
aws_accesskey = "Your Access Key"
aws_secretaccess = "Your Secret Access Key"
myregion = "your-region"
```

## Features

### Face Mask Detection
The main function `detect_FaceMask` analyzes images for face mask usage:

```python
def detect_FaceMask(aws_access, aws_secret, aws_region, photo, confidence):
    """
    Detects face masks in an image and visualizes results.
    
    Args:
        aws_access: AWS access key
        aws_secret: AWS secret key
        aws_region: AWS region name
        photo: Path to image file
        confidence: Confidence threshold for detections
        
    Output:
        Displays image with color-coded bounding boxes
    """
```

### Visualization Colors
- 🟢 Green: Properly worn face mask
- 🔴 Red: No face mask detected
- 🟡 Yellow: Low confidence detection or improperly worn mask

## Usage

```python
# Example usage
detect_FaceMask(
    aws_accesskey,
    aws_secretaccess,
    "us-west-2",
    "path/to/image.jpg",
    90  # confidence threshold
)
```

## How It Works

1. Image Processing:
   - Opens and processes image using PIL
   - Converts image to binary format
   - Prepares drawing context for visualization

2. AWS Rekognition:
   - Sends image to AWS Rekognition service
   - Analyzes for protective equipment (face masks)
   - Returns detection results with confidence scores

3. Visualization:
   - Draws bounding boxes around detected faces
   - Color codes based on mask presence and proper usage
   - Handles low confidence detections with warning indicators

## Bounding Box Logic

1. Face Mask Present:
   ```python
   if ppe_item['Type'] == 'FACE_COVER':
       # Green box for proper mask usage
       # Red box if mask doesn't cover properly
   ```

2. No Face Mask:
   ```python
   if found_mask == False:
       # Red box around entire person
   ```

3. Low Confidence:
   ```python
   if ppe_item['CoversBodyPart']['Confidence'] < confidence:
       # Yellow warning box
   ```

## Error Handling

The implementation handles:
- Image loading errors
- AWS service errors
- Invalid confidence values
- Image format issues
