# Image Dehazing Using DehazeFormer-T and Dark Channel Prior

## 1. Project Overview

Image dehazing is a computer vision task that aims to recover clear images from hazy or degraded inputs. Haze reduces image contrast, visibility, and structural detail, which can affect applications such as autonomous driving, surveillance, remote sensing, and object detection.

This project compares a classical image restoration technique, **Dark Channel Prior (DCP)**, with **DehazeFormer-T**, a pretrained deep learning model designed for image dehazing.

The objective is to evaluate how effectively the two methods restore image quality using paired hazy images and their corresponding clear references.

## 2. Objectives

- Implement Dark Channel Prior as a classical dehazing baseline.
- Apply a pretrained DehazeFormer-T model to hazy images.
- Compare the methods using Peak Signal-to-Noise Ratio (PSNR) and Structural Similarity Index Measure (SSIM).
- Analyze performance across different hazy versions of the same scenes.
- Investigate cases where deep learning performs better or worse than the classical approach.

## 3. Methodology

### 3.1 Dark Channel Prior

Dark Channel Prior is a traditional image dehazing method based on assumptions about the intensity of pixels in haze-free outdoor images.

The method estimates atmospheric light and the transmission map, then reconstructs an image with reduced haze.

DCP is used as a non-deep-learning baseline for comparison.

### 3.2 DehazeFormer-T

DehazeFormer is a Transformer-based neural network developed for image restoration and dehazing. This project uses its compact T variant with pretrained weights.

The workflow is:

1. Load a hazy RGB image.
2. Normalize pixel values to the range [-1, 1].
3. Pass the image through DehazeFormer-T.
4. Convert the model output back to the [0, 1] image range.
5. Compare the restored image against the corresponding clear reference.

The pretrained model is used for inference; the network is not trained from scratch in this experiment.

**Official implementation:** https://github.com/IDKiro/DehazeFormer

## 4. Dataset

The experiment uses a paired indoor image dataset stored in Google Drive.

| Property | Description |
|---|---|
| Clear reference images | 50 |
| Hazy images | 500 |
| Hazy variants per scene | 10 |
| Image format | PNG |
| Example hazy image | `1400_1.png` |
| Corresponding clear image | `1400.png` |

Each hazy image is evaluated against its corresponding clear reference. Since multiple hazy images share the same clear scene, the 500 image pairs represent 50 distinct reference scenes rather than 500 independent scenes.

The exact provenance and benchmark version of this dataset have not yet been independently verified. Therefore, these results should not be described as results on the complete official SOTS benchmark.

## 5. Evaluation Metrics

### Peak Signal-to-Noise Ratio (PSNR)

PSNR measures pixel-level reconstruction quality relative to a reference image. Higher values generally indicate lower reconstruction error.

### Structural Similarity Index Measure (SSIM)

SSIM measures structural similarity between the restored image and the reference. Values closer to 1 indicate greater similarity.

Both metrics are calculated by comparing the output against the corresponding clear reference image.

## 6. Preliminary Results

The following results were obtained from the current evaluation of 500 hazy images.

| Method | Mean PSNR (dB) ↑ | Mean SSIM ↑ |
|---|---:|---:|
| Dark Channel Prior | 17.945 | 0.7773 |
| DehazeFormer-T | 23.143 | 0.9204 |

These preliminary results show higher average PSNR and SSIM for DehazeFormer-T than for DCP on the evaluated dataset.

The reported values use the current custom evaluation pipeline. They should not be compared directly with published benchmark results until the checkpoint provenance and evaluation protocol have been verified.

### Runtime

The current recorded mean runtimes are:

- Dark Channel Prior: approximately 0.036 seconds per image.
- DehazeFormer-T: approximately 0.098 seconds per image.

These timings are preliminary. A fair speed comparison requires both methods to be benchmarked on the same hardware under comparable timing conditions.

## 7. Analysis

### Performance Across Haze Versions

The experiment evaluates ten hazy variants for each clear scene. Initial results show a decline in DehazeFormer-T's mean PSNR across higher-numbered variants.

This indicates that reconstruction quality varies across the provided variants. The suffix numbers alone do not establish physical haze severity because the dataset's generation procedure has not been verified.

### Scene-Level Evaluation

To reduce the effect of treating related images as independent observations, results can be aggregated across the ten variants associated with each clear scene.

Scene-level analysis provides a more appropriate view of consistency across the 50 reference scenes.

### Failure Cases

Some images perform worse with DehazeFormer-T than with DCP. These cases are important because they show that a pretrained neural model does not necessarily outperform a classical method on every input.

Potential contributing factors include challenging image content, haze characteristics, training-data differences, and limitations of the reconstruction model. Further investigation is required to determine the causes in this dataset.

## 8. Limitations

- The checkpoint's exact training configuration has not yet been independently verified.
- The dataset's precise source and benchmark version remain unconfirmed.
- Results depend on the current implementation and metric calculation protocol.
- The experiment evaluates a limited set of 50 clear scenes.
- Runtime measurements require standardized hardware conditions for a fair comparison.
- The pretrained model may not generalize equally well to all real-world haze conditions.

## 9. Future Work

- Verify the checkpoint against the official indoor evaluation configuration.
- Reproduce the official evaluation protocol where applicable.
- Evaluate on additional independently sourced dehazing datasets.
- Investigate difficult scenes and cases where DCP performs better.
- Conduct controlled runtime and memory comparisons.
- Explore the effect of dehazing on downstream object detection.
- Investigate lightweight adaptation methods suitable for limited computational resources.

## 10. Technologies Used

- Python
- PyTorch
- NumPy
- Pandas
- Matplotlib
- Pillow
- scikit-image
- Google Colab
- Git and GitHub

## 11. Project Outputs

The evaluation generates:

- Per-image PSNR, SSIM, and runtime measurements.
- Summary comparison results.
- PSNR and SSIM comparison graphs.
- Performance analysis across haze versions.
- Scene-level PSNR distribution plots.
- Visual comparisons of hazy inputs, DCP outputs, DehazeFormer-T outputs, and clear references.

## 12. Acknowledgements

This project builds upon the DehazeFormer research and its publicly available implementation.

Repository: https://github.com/IDKiro/DehazeFormer

The authors of the original method are credited for their research, model architecture, and implementation.

## 13. Conclusion

This project implements a comparative image dehazing pipeline using Dark Channel Prior and pretrained DehazeFormer-T. Preliminary results on 500 paired hazy images indicate that DehazeFormer-T achieves higher average PSNR and SSIM than the classical baseline.

The experiment provides a foundation for further research into image restoration, model generalization, evaluation methodology, and downstream computer vision applications. Final benchmark claims will require verification of the checkpoint, dataset provenance, and evaluation protocol.
