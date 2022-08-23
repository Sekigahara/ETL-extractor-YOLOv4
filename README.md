# ETLCDB Python extractor and YOLOv4 Training Format

ETLCDB is one of the handwritten Japanese character database. ETLCDB split the database into various sub ETL databases.
This repositories allows to extract Japanese characters especially Hiragana and katakana from ETL-1, ETL-8 and ETL-9 with Python.
In addition, this repo also be able to do various preprocess and augmentation then converted into YOLOv4 training format.

## Requirement
- This repo runs with Python 3.8
- Download the ETL-1, ETL-8 and ETL-9 [here](http://etlcdb.db.aist.go.jp/)
- Install the requirement file :
```sh
pip install -r requirements.txt
```
