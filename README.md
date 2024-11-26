# Cell Nuclei Segmentation with U-Net

This project implements a U-Net model in PyTorch to segment cell nuclei in microscopy images. The objective is to accurately identify and separate cell nuclei from the background, showcasing the U-Net architecture's robustness in biomedical image segmentation.

## Project Overview

The project involves:
- **Dataset**: 2000 microscopy images and their corresponding masks, each with dimensions of 128x128 pixels. Data was loaded from `.npz` files, normalized, and reshaped for model input.
- **Objective**: Train a U-Net model to produce binary segmentation masks for cell nuclei.

## Challenges and Resolutions

### Initial Challenges:
1. **High Loss Values**: The loss remained high during early training epochs.
   - **Resolution**: Reduced the learning rate to `0.001` and increased the number of training epochs to `300`.
2. **Zero Output Masks**: Predicted masks contained only zeros, leading to incorrect results.
   - **Resolution**: Proper normalization of images and masks, validation of model architecture, and adding a small value to the sigmoid output before thresholding resolved this issue.
3. **Incorrect Component Counts**: The `cv2.connectedComponents` function returned inaccurate counts due to improper mask thresholding.
   - **Resolution**: Ensured binary mask thresholding before counting components.

### Final Results:
- Segmented cell nuclei were clearly separated from the background in test images.
- Training loss decreased significantly by epoch 150, indicating successful training.
- Dynamic learning rate adjustments improved performance by reducing validation loss stagnation.

## Key Model Features

- **Architecture**: U-Net, tailored for biomedical image segmentation tasks.
- **Optimization**:
  - Lowered learning rate to `0.001`.
  - Increased training epochs to `300`.
  - Added small value to sigmoid output to stabilize binary mask predictions.
- **Component Counting**: Used OpenCV's `cv2.connectedComponents` for nuclei counting.

## Results and Insights

- **Performance**: The model effectively segmented cell nuclei in microscopy images.
- **Learning**: Lowering the learning rate and increasing training epochs were crucial for achieving convergence.
- **Conclusion**: This project demonstrates the U-Net architecture's effectiveness for biomedical image segmentation, offering a reliable method for accurate cell nuclei identification.

## Getting Started

1. **Dataset**: Ensure your dataset contains microscopy images and their corresponding masks in `.npz` format, resized to 128x128 pixels.
2. **Dependencies**:
   - Python 3.x
   - PyTorch
   - OpenCV
   - NumPy
3. **Training**:
   - Adjust the learning rate and number of epochs as needed.
   - Normalize images and masks before training.
4. **Inference**:
   - Use the trained model to generate binary segmentation masks.
   - Apply `cv2.connectedComponents` to count nuclei in the segmented masks.

## Future Work

- Experiment with different loss functions to further enhance segmentation accuracy.
- Explore data augmentation techniques to increase robustness.
- Fine-tune the architecture for higher-resolution microscopy images.

## Acknowledgments

This project highlights the capabilities of the U-Net architecture for biomedical applications and serves as a foundation for future segmentation tasks.
