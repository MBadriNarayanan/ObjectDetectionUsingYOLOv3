# ObjectDetectionUsingYOLOv3
Object detection using YOLO v3 Algorithm with custom dataset.

For this project I have downloaded 3 types of classes from [Open Images Dataset v4](https://storage.googleapis.com/openimages/web/index.html) : Camera, Glasses and Microphone

## Steps Involved :

### Downloading the dataset 

* Clone this repository [OIDv4](https://github.com/EscVM/OIDv4_ToolKit)
* Activate your python environment and navigate to the directory where the repository was cloned and type the following command : pip install -r requirements.txt
* To verify type the following command : python main.py -h
* After verifying type the following command : python main.py downloader --classes Camera Microphone Glasses --type_csv train --multiclasses 1 --limit 10
* 30 Images of the classes Camera, Glasses, Microphone each will be downloaded and two csv file will also be downloaded in the OID Folder.
* One CSV file will contain annotations and the other will contain and the class description.
* In order to verify type the following command : python main.py visualizer
* For easier access I would have copied the Dataset and csv_folder Folders to CustomObjectDetection Folder and would have deleted the OIDv4 folder
* Convert annotations from the csv file using [Converting Annotations Notebook](https://github.com/MBadriNarayanan/ObjectDetectionUsingYOLOv3/blob/master/ConvertingAnnotations.ipynb)
* Prepare data in YOLO Format using [Data Preparation Notebook](https://github.com/MBadriNarayanan/ObjectDetectionUsingYOLOv3/blob/master/DataPreparation.ipynb) 

### Preparing CFG Files

* Max Batches = Number of Classes * 2000 (But not less than 4000)
* Number of Steps = 80 % and 90 % of Max Batches
* Number of Filters = (Number of Classes + 5) * 3
* It is needed to update number of classes in every of three yolo layers in the end of the configuration files. Also, it is needed to update number of filters in convolutional layers right before such every yolo layers but not anywhere else. It is needed in order to properly connect convolutional layer that is right before yolo layer in accordance with number of classes in dataset.

### Training 
* Go to darknet root directory and type the following command : darknet.exe detector train cfg\camera_microphone_glasses.data cfg\camera_microphone_glasses_train.cfg weights\darknet53.conv.74 -dont_show

### Testing 
* Copy Camera.jpeg , Glasses.jpeg and Microphone.jpeg file to the data folder in the darknet directory.
* Go to darknet root directory and type the following command : darknet.exe detector test cfg\camera_microphone_glasses.data cfg\camera_microphone_glasses_test.cfg weights\camera_microphone_glasses_train_last.weights -ext_output data\Camera.jpg
