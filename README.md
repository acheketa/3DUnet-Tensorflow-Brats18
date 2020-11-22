# 2020_healthhub_datathon
- Authors: [Kyuhee Jo](kyuhee0622@gmail.com), [Chae Young Lee](cylee7133@gmail.com)
- This project is part of 2020 Healthhub Datathon Track A: CBCT 3D Segmentation. For more information, please contact healthhub@2020healthhubdatathon.com.
- We modified the implementation of https://github.com/tkuanlun350/3DUnet-Tensorflow-Brats18.

## Development
- Computing environment: CentOS 7, 2 Nvidia Tesla V100 32GB, CUDA 10.1, CuDNN 7.5.0
- Training time: 3hrs
- Model file: link

## Get Started

### 1. Installation

**Please use Python 3.** In your virtual environment,
```
pip install -r requirements.txt
```

### 2. Data Format
The dataset structure follows the format used by the [Medical Segmentation Decathlon](http://medicaldecathlon.com/) (MSD). `nnUNet_raw_data_base` is an environment variable of the directory that has the subfolder `nnUNet_raw_data` that contains raw data for training. More specifically, in this subfolder are subfolders for each task. For more information, please refer to the [documentation](https://github.com/MIC-DKFZ/nnUNet/blob/master/documentation/dataset_conversion.md) from the original implementation.
```
nnUNet_raw_data_base/nnUNet_raw_data
├── Task100_CBCT3DSeg/
│   ├── dataset.json
│   ├── imagesTr
│   ├── (imagesTs)
│   └── labelsTr
└── ...
```
Note that all files in `imagesTr, imagesTs, labelsTr` are 3D NIfTI files (.nii.gz). To convert the DICOM data format of the Datathon data to NIfTI, you can either use the [dicom2nifti](https://pypi.org/project/dicom2nifti/) Python module or use our data processing pipeline in `preprocessing/dicom2nifti.py`.

### 3. Train and inference
```
# Train
python train.py --gpu 0,1 --logdir=./train_log
# Predict
python train.py --load=./train_log/model-30000 --gpu 0 --predict
```
