# ETLCDB Python extractor and YOLOv4 Training Format

ETLCDB is one of the handwritten Japanese character database. ETLCDB split the database into various sub ETL databases.
This repositories allows to extract Japanese characters especially Hiragana and katakana from ETL-1, ETL-8 and ETL-9 with Python.
In addition, this repo also be able to do various preprocess and augmentation then converted into YOLOv4 training format.

## Main Repositories
- High level and low level overview of the project can be found in the main repositories.
- Main respositories can be found [here](https://github.com/Sekigahara/Multilabel-classification-Japanese-character-with-YOLOv4).

## Requirement
- This repo runs with Python 3.8
- Download the ETL-1, ETL-8 and ETL-9 [here](http://etlcdb.db.aist.go.jp/)
- Install the requirement file :
```sh
pip install -r requirements.txt
```
- The script is using .ipynb extension, make sure to install the jupyter notebook

## Workflow
- <b>Extract the Image first with available script for each sub ETL version in dataset folder.</b> </br>
There are 3 different script for each sub ETL database version, these 3 scripts extract 46 basic hiragana(あ-a to ん-n) and 46 basic katakana(ｱ-a to ﾝ-n) characters.</br></br>
The script also automatically perform reverse binarization into white background and black stroke by utilizes average of the color pixel as the threhold.</br></br>
Katakana characters are only exist in ETL-1 while Hiragana characters exist in ETL-8 and ETL-9.
The usage of this script are case dependent or optionals, if you required to utilizes hiragana only go for extract ETL-8 and ETL-9 while katakana only requires the ETL-1.</br></br>
Note : The ETL version is vary and may require different treatment to match the required format. In this cases, i utilizes ETL-1C, ETL-8G and ETL-9B

- <b>Cross validation script (cross_validation.ipynb). </b> </br>
This script are meant for data split into train and test using KFold, feel free to change and utilizes different approach such as holdout method. </br></br>
This script work by loading the path and extract the label for each images. After the data split happens, this script will calculate the gap between highest data distribution by each classes. This calculation will furthermore used for how many augmentation will be done for each classes. The last process is saving those configuration into .npz files in utils folder.</br>

- <b> Preprocess script. </b> </br>
This script has two different, the first one is only for hiragana and the second one is for hiragana & katakana. The focus of this script is to generate random augmentation from the given augmentation technique.</br></br>
The augmentation only done in trainset, the augmentation techniques are separated into two groups and could produce 11 different augmentation combination. Feel free to add more augmentation technique to increase the combination and generate more data.</br>

- <b> Train format. </b> </br>
This script focus is to generate YOLO darknet format based on AlexeyAB [here](https://github.com/AlexeyAB/darknet) especially for YOLOv4 and possibly new YOLOv7.</br>
This script will generate train.txt and test.txt that consist list of images for each set. </br>
In obj folder will also generated the images and for each image will generated .txt files for bounding box coordinates.</br></br>
Note : The calculation of bounding box is simply taking the whole images as the coordinates.

## Final Note
The generated data after augmentation and train format will be around 300k in total, for those who using harddisk please becareful due to the huge file indexing may reduce the lifetime of harddisk. The augmentation process may also consume a huge RAM and CPU resources, resource management be advised. </br>
