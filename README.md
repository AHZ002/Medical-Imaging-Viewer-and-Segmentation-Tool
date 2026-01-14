# Medical Image Viewer & Segmentation Tool

A Python-based medical imaging application that provides comprehensive visualization and segmentation capabilities for DICOM and NIfTI medical images. The tool features an intuitive GUI for image manipulation and integrates MedSAM for automated medical image segmentation.

## Features

### Image Viewing & Manipulation
- **Multi-format Support**: Load and visualize DICOM (.dcm) and NIfTI (.nii, .nii.gz) medical images
- **Multi-slice Navigation**: Browse through 3D medical image volumes with an interactive slice slider
- **Image Transformations**:
  - Contrast adjustment with real-time preview
  - 90-degree rotation
  - Vertical flip
  - Zoom functionality (1x to 3x magnification)
- **Export Capability**: Save processed images as PNG or JPEG

### Segmentation Pipeline
- Integrated MedSAM (Medical Segment Anything Model) for automated segmentation
- Achieved **mean IoU of 0.8283** on MMOTU dataset
- Efficient processing pipeline for medical image analysis

## Installation

### Prerequisites
- Python 3.8 or higher
- pip package manager

### Required Dependencies

```bash
pip install numpy
pip install pydicom
pip install nibabel
pip install PyQt5
pip install scikit-image
pip install opencv-python
pip install torch torchvision  # For MedSAM segmentation
```

Or install all dependencies at once:

```bash
pip install numpy pydicom nibabel PyQt5 scikit-image opencv-python torch torchvision
```

## Usage

### Running the Application

```bash
python main.py
```

### Loading Images

1. Click **"Load DICOM/NIfTI Image"** button
2. Select a medical image file (.dcm, .nii, or .nii.gz)
3. For DICOM series, the application will automatically load all slices in the same directory

### Navigation & Manipulation

- **Slice Navigation**: Use the horizontal slider to navigate through different slices in 3D volumes
- **Contrast Adjustment**: Drag the contrast slider (1-300%) to enhance image visibility
- **Rotation**: Click "Rotate 90°" to rotate the image clockwise
- **Flip**: Click "Flip Vertically" to flip the image along the vertical axis
- **Zoom**: Adjust the zoom slider (100-300%) to magnify the region of interest

### Saving Images

1. Click **"Save Image"** button
2. Choose desired format (PNG or JPEG)
3. Specify filename and location

## Project Structure

```
.
├── main.py                 # Application entry point
├── gui.py                  # Main GUI implementation
├── image_loader.py         # DICOM/NIfTI image loading utilities
├── image_processor.py      # Image processing functions
├── medSAM__2_.ipynb       # MedSAM segmentation notebook
└── README.md              # Project documentation
```

## Architecture

### Components

**main.py**: Application launcher that initializes the PyQt5 application and main window.

**gui.py**: Contains the `MedicalImageViewer` class implementing the graphical interface with:
- Image display canvas
- Control buttons and sliders
- Event handlers for user interactions
- Multi-slice volume management

**image_loader.py**: Handles loading of medical images:
- DICOM single-frame and multi-frame support
- Automatic DICOM series detection and stacking
- NIfTI volume loading with dimension handling

**image_processor.py**: Image manipulation functions:
- Contrast enhancement
- Rotation and flipping
- Intelligent zoom with center cropping and bicubic interpolation

**medSAM__2_.ipynb**: Jupyter notebook implementing the MedSAM segmentation pipeline.

## Performance

The segmentation pipeline demonstrates strong performance on medical imaging datasets:

- **Dataset**: MMOTU (Multi-Modal Organ Tumor) dataset
- **Mean IoU**: 0.8283
- **Model**: MedSAM (Medical Segment Anything Model)

## Technical Details

### Supported Image Formats

- **DICOM**: Single-frame and multi-frame DICOM files with automatic series detection
- **NIfTI**: 2D, 3D, and 4D volumes (.nii and .nii.gz compressed format)

### Image Processing Pipeline

1. Load image using pydicom or nibabel
2. Convert to float32 numpy array
3. Apply user-requested transformations
4. Normalize to 0-255 range for display
5. Render using PyQt5 QImage/QPixmap

### Zoom Implementation

The zoom feature uses a sophisticated approach:
- Center-crop to desired zoom level
- Bicubic interpolation (cv2.INTER_CUBIC) for quality preservation
- Maintains original image dimensions for consistent display

## Limitations

- Single-channel (grayscale) image display
- DICOM series assumes files are in the same directory
- Zoom range limited to 1x-3x to prevent quality degradation

## Future Enhancements

- [ ] Multi-window layout for comparison viewing
- [ ] Additional segmentation model integration
- [ ] DICOM metadata viewer
- [ ] Annotation tools for manual segmentation
- [ ] Batch processing capabilities
- [ ] 3D volume rendering

## Contributing

Contributions are welcome! Please feel free to submit issues or pull requests.

## License

This project is available for educational and research purposes.

## Acknowledgments

- MedSAM model for medical image segmentation
- PyQt5 for the graphical interface
- pydicom and nibabel libraries for medical image I/O
- MMOTU dataset for validation

## Contact

For questions or feedback, please open an issue in the repository.

---

**Note**: Ensure you have appropriate permissions and comply with relevant regulations (HIPAA, GDPR, etc.) when working with medical imaging data.
