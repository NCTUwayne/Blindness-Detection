# Blindness-Detection
NCTU VRDL Final Project
# Hardware
* Ubuntu 16.04 LTS
* Intel(R) Core(TM) i7-6700 CPU @ 3.40GHz
* NVIDIA TitanX
## Dataset
* APTOS 2019 Blindness Detection
Contains 3662 training data and 1928 testing data.
* Diabetic Retinopathy
This dataset contains images from the 2015 Diabetic Retinopathy Detection, a left and
right field is provided for every subject. Images are labeled with a subject id as well as
either left or right. Contains 35.1K training images.
## Requirements
* Torch
* Torchvision
* Fastai
* Sklearn
* Numpy
* Tqdm
## Data preprcessing
We use Ben Graham's preprocessing: 
center crop first, resize the image to 244x244, and then adjust the brightness and the transparency of the image.
## Augmentations
Horizontal and Vertical Flip, 360 rotation, zoom 20%-25%, lighting 50%.
## Models
Efficientnet B0, Efficientnet B1, Efficientnet B2, Efficientnet B3
## Hyperparameters
Learning rate: 1e-3, reduced by factor=0.5, patience=1
Optimizer: Adam
Loss: MSE Loss
## Training method
We trained 10 epochs using 2015 data as train and 2019 data as validation set. Then split the 2019 data into 80:20 ratio and
finetuned the previously trained model over it for 15 epochs. We took the best model based on validation loss.
## Experimental results
Model           |   Val  Kappa  | Public  Kappa | Private Kappa |
----------------|:-------------:|--------------:|--------------:|
Efficientnet B0 |    0.908657   |    0.788192   |    0.901865   | 
Efficientnet B1 |    0.915766   |    0.787105   |    0.909380   |
Efficientnet B2 |    0.904228   |    0.785692   |    0.901226   |
Efficientnet B3 |    0.896781   |    0.786012   |    0.899652   |
Ensemble        |               |    0.797852   |    0.909811   |
