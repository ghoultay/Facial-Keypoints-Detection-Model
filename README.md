# Face Image Keypoint Detection

This project involves detecting facial keypoints using a deep learning model based on the EfficientNet B5 architecture. The model was trained on the **WFLW dataset** and optimized for accurate keypoint prediction without freezing any layers.

## Final Pipeline

### Augmentations
To improve generalization, the following augmentations were applied:
- **HorizontalFlip**
- **Rotate**
- **Resize**
- **ShiftScaleRotate**
- **RandomBrightnessContrast**
- **OneOf**: Gaussian, CLAHE, ImageCompression, RandomGamma, Blur, Posterize

### Model
- **Backbone**: EfficientNetB5 with pretrained weights
- **Dataset**: WFLW

### Criterion
- **Loss Function**: WingLoss

### Optimizer
- **AdamW** optimizer for better performance in weight decay.

### Scheduler and Warmup
- **Scheduler**: StepLR for learning rate decay.
- **Warmup**: LinearWarmup for smoothing the initial learning phase.

## Observations

1. The [paper](https://arxiv.org/pdf/2101.10808) explores using heatmaps for keypoint detection, such as employing the Hourglass architecture. This could potentially be explored further, but due to time constraints, it was not implemented in this project.

2. **Model Limitations**:
   - The model struggles with faces wearing glasses or when the face is highly rotated.
   - This issue could be mitigated with a larger dataset. Techniques such as using **VAE** or **GAN** to generate augmented data with latent vector representations of glasses could also help, but gathering more real-world data is likely the better approach.

3. **Dataset Quality**:
   - The WFLW dataset contains some labeling errors, which may have impacted the overall performance and accuracy of the model.

4. **Potential Improvements**:
   - Train on a larger dataset or incorporate a stronger model than EfficientNetB5, given sufficient computational resources.
   - Explore additional hyperparameter tuning for the AdamW optimizer.
   - Try further augmentations, such as **ElasticTransform**, to improve the robustness of the model.

## Future Work
- Investigate using heatmap-based output layers like the Hourglass architecture.
- Explore advanced data augmentation techniques, including latent vector-based augmentations.
- Train the model on more computationally intensive architectures, depending on available resources.

## Conclusion
The current implementation shows promising results but faces limitations with certain edge cases, such as faces with glasses or extreme rotations. With a larger dataset and more computational power, the model’s performance can be further improved.
