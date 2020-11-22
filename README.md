# 2020_healthhub_datathon
- Authors: [Kyuhee Jo](kyuhee0622@gmail.com), [Chae Young Lee](cylee7133@gmail.com)
- This project is part of 2020 Healthhub Datathon Track A: CBCT 3D Segmentation. For more information, please contact healthhub@2020healthhubdatathon.com.
- We modified the implementation of https://github.com/tkuanlun350/3DUnet-Tensorflow-Brats18.

## Development
- Computing environment: CentOS 7, 2 Nvidia Tesla V100 32GB, CUDA 10.1, CuDNN 7.5.0
- Training time: 3hrs
- Model file: [link](https://drive.google.com/file/d/1CMKKRj-dBMHkZ7u1FgbJUC8aT31eBjGV/view?usp=sharing)

## Get Started

### 1. Installation

**Please use Python 3.** In your virtual environment,
```
pip install -r requirements.txt
```

### 2. Data Format
All data, including the ground truth, must be in 3D NIfTI files (.nii.gz). To convert the DICOM data format of the datathon data to NIfTI, you can use our data processing pipeline in `data_preparation.ipynb`. Then, place your train data in the following format and set the path of the train data in `load_3d()` function from `data_loader.py`.
```
train/
├── patientID/
│   └── .nii.gz
└── ...
train_gt/
├── .nii.gz
├── ...
└── .nii.gz
```


### 3. Train and inference
```
# Train
python train.py --gpu 0,1 --logdir=./train_log
# Predict
python train.py --load=./train_log/model-30000 --gpu 0 --predict
```
