# TCGA Ovary MSI High classification.

## Setup

#### Requirerements
- ubuntu 18.04
- RAM >= 128 GB
- GPU Memory >= 24 GB
- GPU driver version >= 418.152
- CUDA version >= 10.1
- cuDNN version >= 7.5.1

#### Download
Execution file, configuration file, and models are download from the [zip](https://drive.google.com/file/d/1MqGr6y_EgdS5CscmfWFmABvFkE1UCwe6/view?usp=share_link) file.  (For reviewers, "..._cwlab" is the password to decompress the file.)

#### File structure
```
TCGA_WSI_Ovary_Inv3/
│
├── Data/ - training and testing data location
│   ├── BB_tileout/
│   │   ├── TCGA-04-1335-01A-01-BS1.svs/
│   │   │   ├── 10_2.bmp
│   │   │   ├── 10_3.bmp
│   │   │   ├── 10_4.bmp
│   │   │   │       ⋮
│   │   │   └── 20_11.bmp
│   │   │
│   │   └── TCGA-04-1342-01A-01-BS1.svs/
│   │       ├──30_3.bmp
│   │       ├──32_1.bmp
│   │       ├──33_4.bmp
│   │       │       ⋮
│   │       └── 56_11.bmp          
│   │
│   │
│   └── WSI_Image/
│       ├── TCGA-04-1335-01A-01-BS1.svs
│       ├── TCGA-04-1342-01A-01-BS1.svs
│       ├── TCGA-10-0928-01A-01-BS1.svs
│       │       ⋮
│       └── TCGA-61-1730-11A-01-TS1.svs
│
│
├── List/ - demo list
│   ├── train.txt
│   └── test.txt
│
├── Training/
│   ├── solver.py - execution file
│   ├── Model_selection.py
│   ├── voc_layers.py
│   ├── voc_layers.pyc
│   ├── Model/ - storage location of training models
│   └── network/
│       ├── solver.prototxt - configuration file
│       ├── train_weight.prototxt
│       └── deploy.prototxt
│
└── Inference/ 
    ├── Model/ - demo model
    │   └── Ovary_TCGA_MSI50%_weight_iter_1050000.caffemodel
    ├── deploy.prototxt
    └── inference_TMA.py - execution file

```

## Steps

#### 1. Data preparing
Put the Whole slide image in the Data/WSI_Image.

Then in a terminal run:
```
python TileScale.py
```

After running in a terminal, the result will be produced in two folders named "BB_tileout"


#### 2. BB_Segmentation
Open the "caffe_root.txt" file to set up the root of caffe to use.

Then in a terminal run:
```
./Main_Segmentation
```
After running in a terminal, the image results will be produced in two folders named "AfterSeg_BB_tileout" and "BB_tileout"

#### 3. List_Preprocessing
Before doing "List_Preprocessing" execution file, the list of all patches needs to be produced first as shown in "TestingList_all.txt" and
"TrainingList_all.txt"

Then in a terminal run:
```
./Main_List_Preprocessing
```

After running in a terminal will produce two ".txt" files named  "TestingList_attentionScoring.txt" and "TrainingList_filter.txt"

#### 4. Trainining
Open the "solver.py" and "voc_layers.py" files to set up the storage location of training models and the location of training list("TrainingList_filter.txt") to use.

Then in a terminal run:
```
python solver.py
```

#### 5. Testing
Open the "inference_TMA.py" file to set up the storage location of training models and the location of testing list("TestingList_attentionScoring.txt") to use.

Then in a terminal run:
```
python inference_TMA.py
```

## License
This extension to the Caffe library is released under a creative commons license, which allows for personal and research use only. For a commercial license please contact Prof Ching-Wei Wang. You can view a license summary here:  
http://creativecommons.org/licenses/by-nc/4.0/


## Contact
Prof. Ching-Wei Wang  
  
cweiwang@mail.ntust.edu.tw; cwwang1979@gmail.com  
  
National Taiwan University of Science and Technology
