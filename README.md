# Covid-Segmentation

## Overview
### Data
Model was trained on [COVID-QU-Ex Dataset](https://www.kaggle.com/datasets/anasmohammedtahir/covidqu).
The dataset is divided into two subsets for lung and covid segmentation.
These sets contain 33,920 and 5,826 chest X-ray respectively.

### Model
![U-net architecture](https://github.com/zhixuhao/unet/blob/master/img/u-net-architecture.png)

For this project I used pretrained [U-Net architecture](https://github.com/milesial/Pytorch-UNet) implemented using PyTorch.
The last layer of the network was updated to output a single value with added Sigmoid activation function to make sure, that mask pixels are in [0, 1] range.

### Training
Before training model was first pretrained on a lung segmentation task so that it would already be good at recognizing general patterns in chest X-Rays.

Lung and covid segmentation models were trained for 2 and 4 epoch respectively.

Training and evaluation was done using DiceLoss function with additional IoU and PA metrics also being computed.

### Inference
For a better inference both lung and covid segmentation models were exported to ONNX format with additional ORT functionality provided.

## Results
After pretraining on lung segmentation and training on covid segmentation the following results were achived (on test set):

DiceLoss: 0.02, IoU: 0.49, PA: 0.99 for lung segmentation

DiceLoss: 0.66, IoU: 0.17, PA: 0.92 for covid segmentation

## Examples

Lung segmentation:

![image](https://user-images.githubusercontent.com/77388859/225889998-1ff68175-72ea-4910-8190-f9ed31f8a69a.png)

Covid segmentation:

![image](https://user-images.githubusercontent.com/77388859/225889913-dba1d339-813c-44bd-9676-44d961d85d74.png)

