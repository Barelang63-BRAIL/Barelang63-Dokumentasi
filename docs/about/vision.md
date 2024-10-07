# Yolov8-custom-object-detection
Before starting the training process, you need to prepare your dataset with the following folder structure. This structure ensures that YOLOv8 can easily locate the training and validation data.

## Dataset Folder Structure

The dataset should be organized as follows:
```
dataset_example/
│
├── images/
│   ├── train/
│   │   ├── img001.jpg
│   │   ├── img002.jpg
│   │   └── ...
│   ├── val/
│       ├── img001.jpg
│       ├── img002.jpg
│       └── ... 
│        
├── labels/
│   ├── train/
│   │   ├── img001.txt
│   │   ├── img002.txt
│   │   └── ...
│   ├── val/
│       ├── img001.txt
│       ├── img002.txt
│	    └── ...
│       
└── data.yaml
```
You can refer to the folder "dataset/dataset_example" as a reference for setting up your dataset and data.yaml file. Make sure that each image in the train and val folders has a corresponding .txt file in the labels folder with the same filename. These .txt files contain the bounding box information for each object in the images.

## Training Output
When you run the training script in Jupyter Notebook or any other platform, a runs folder will be created automatically. You can check the terminal/output during the training process to see where your training results will be saved. Typically, it will save the results to a directory like runs/detect/train, where you can find model weights, logs, and metrics.
