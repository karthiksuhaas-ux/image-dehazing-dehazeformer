
# Image Dehazing Using DehazeFormer

## Overview
This project explores single-image dehazing using a pretrained DehazeFormer model. The objective is to recover clearer images from hazy inputs and evaluate the quality of the restored images.

## Objectives
- Load and run a pretrained DehazeFormer model.
- Compare hazy input images with dehazed outputs.
- Evaluate image restoration using PSNR and SSIM.
- Measure inference time on a GPU-enabled Google Colab environment.

## Methodology
1. Load the pretrained model and its checkpoint.
2. Prepare hazy images as model inputs.
3. Generate dehazed images.
4. Compare outputs against corresponding clear reference images.
5. Calculate PSNR and SSIM before and after dehazing.

## Tools and Technologies
- Python
- PyTorch
- Google Colab
- DehazeFormer
- NumPy, Pandas and Matplotlib
- scikit-image

## Repository Contents
- `code/` — project notebook
- `results/` — evaluation CSV and result visualizations

## Dataset and Model
The project uses the RISE dehazing dataset available in Google Drive during development and a pretrained DehazeFormer model.

Dataset and model sources, licenses, and download instructions will be documented here after verification.

## Evaluation
Quantitative evaluation uses PSNR and SSIM, with inference time recorded separately. Results will be finalized after verifying the hazy-to-clear image pairings and evaluation procedure.

## Current Status
Work in progress. The project currently focuses on implementing and evaluating a pretrained dehazing model; it does not claim a newly developed architecture.

## Acknowledgements
Credit the original DehazeFormer authors and dataset creators. Refer to their original repositories and publications for licensing and citation details.
