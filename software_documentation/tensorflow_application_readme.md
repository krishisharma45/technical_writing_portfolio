# Tensorflow Application

## About The Project
This is a tool that is used to train models using various data sources in order to predict whether a woman is at risk for balding. This repository contains code for training, predicitions and processing medical images into a compressed file format.

### Requirements
This project uses [Python 3.8](https://www.python.org). Besides Git, all you need for this project are:
- [Docker](https://www.docker.com)
- [Docker Compose](https://docs.docker.com/compose/install/)
- [NVIDIA Docker Container Runtime](https://github.com/NVIDIA/nvidia-container-runtime)

## Preprocessing
Preprocessing takes in medical images and uses business logic to generate compressed files (TFRecords) using Tensorflow.

### Example Dataset
To run the Cornell preprocessing pipeline run the following command on an EC2 instance:

```
python -m src.preprocessing.example.pipeline
```

**Note**: The TFRecord generation step will require a large instance to run. 

## Prediction
### Locally Running Predictions

You can run predictions locally if you have a GPU, as the Tensorflow processes running to generate the predictions require image processing.

The final predictions will be saved to S3.

### Isolated Predictions
If you don't want to generate predictions on the entire dataset, you can run predictions on the image encoder or classifier in isolation. To run it end to end, simply run the following script with the appropriate field: 

```
bin/launch_prediction.sh classifier
```

## Evaluation
Evaluation is the same for the output of the image encoder or the classifier. 