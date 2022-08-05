# TMEscore

## Requirements

TMEscore requires `Python 3.8` to run. Also you should have an access to this repository to install `TMEscore` package.

## Installation

TMEscore is protected by Arontier Proprietary License. 
Only authorized users can access `TMEscore` package.
If you are interested, please send an email to `hyahn@arontier.co`.

Assuming you have an access to this repository,
you can install `TMEscore` package by using pip:

```bash
pip install git+ssh://git@github.com/arontier/TMEscore.git   
or   
python setup.py develop
```

If you want to install a specific version:

```bash
pip install git+ssh://git@github.com/arontier/TMEscore.git@version
```

where `version` above is something like `0.0.1`, well a *version*.

All package dependencies will be resolved automatically.
If you stuck with SSH key business, please read [https://help.github.com/en/github/authenticating-to-github/adding-a-new-ssh-key-to-your-github-account](https://help.github.com/en/github/authenticating-to-github/adding-a-new-ssh-key-to-your-github-account) to register your SSH key to GitHub.

## Quickstart

### 1. Data, Model Preparation
To test-drive, you will need an input H&E(Hematoxylin & Eosin) staining WSI(additionally annotated hotspot region)   
and model files.   
Model files are too big to upload here,   
so you may want to request these files too when you ask for access to this repository.   

Image format supported by `TMEscore` is: svs.   
After installing `TMEscore`, make `input` directories and place your image file under `input` directory.   
Put your 3 model weight files, say `CK.pth`, `LCA.pth`, `DESMIN.pth` in the `data/checkpoint/` directories.   
Also, you can add hotspot annotation json file made by [QuPath program](https://qupath.github.io/)   
For example, the folder structure should look like this:   

```bash
├── data
│   ├── checkpoint
│   │   ├── CK.pth
│   │   ├── LCA.pth
│   │   ├── DESMIN.pth
├── TMEscore
│   ├── input
│   │   ├── sample.svs
│   │   ├── sample.geojson

``` 

<br />

### 2. Inference
For inference, we support `2 types of inference : WSI(Whole Slide Image) and Hotspot.`   
For WSI inference, you need to prepare just input svs files.   
For Hotspot inference, you need to prepare input image files(support only svs file) and corresponding json files.   

#### 2-1. Using Library
For example

```python
from TMEscore.test import main

main(input_directory='Input',
     output_directory='Output',
     hotspot_prediction = None,
     CK_model_file_path = 'data/checkpoint/CK.pth',
     DESMIN_model_file_path = 'data/checkpoint/DESMIN.pth',
     LCA_model_file_path = 'data/checkpoint/LCA.pth'):

```

※※ Here, if ```hotspot_prediction``` is set to None, WSI prediction will be done.   
If ```hotspot_prediction``` is set to True and corresponding geojson file is in input_directory, Hotspot prediction will be done.   
The name of svs, geojson file shoule be same.   
(ex) sample.svs, sample.geojson)   


#### 2-2. Using Binary
Run the following command to run `TMEscore-test` for wsi test:

```bash
TMEscore-test --input_directory Input --output_directory Output --hotspot_prediction None --CK_model_file_path data/checkpoint/CK.pth --DESMIN_model_file_path data/checkpoint/DESMIN.pth --LCA_model_file_path data/checkpoint/LCA.pth
```

<br />

### 3. Results

#### 3-1. WSI


| Input(HE) | Output |
|---|---|
|![./doc/Input.PNG](./doc/Input.PNG)|![./doc/Output.PNG](./doc/Output.PNG)|
 
:red_square: : Stroma
:blue_square: : Tumor
:yellow_square: : Lympocyte on Stroma
:green_square: : Lympocyte on Tumor

The file name of output is as belows:   
```
Output : 'Stromal_TIL_0.3511_Intratumoral_TIL_0.1373_MIX.png'   
```

#### 3-2. Hotspot
| Input(HE) | Output | Output2 |
|---|---|---|
|![./doc/Input_Hotspot.PNG](./doc/Input_Hotspot.PNG)|![./doc/1x_TSR_0.8614_Stromal_TIL_0.2976_Intratumoral_TIL_0.0861.png](./doc/1x_TSR_0.8614_Stromal_TIL_0.2976_Intratumoral_TIL_0.0861.png)|![./doc/1x_TSR_0.9332_Stromal_TIL_0.2353_Intratumoral_TIL_0.0570.png](./doc/1x_TSR_0.9332_Stromal_TIL_0.2353_Intratumoral_TIL_0.0570.png)|


#### The file names of outputs are as belows:   
```
Output : 'TSR_0.8614_Stromal_TIL_0.2976_Intratumoral_TIL_0.0861.png'   
Output2 : 'TSR_0.9332_Stromal_TIL_0.2353_Intratumoral_TIL_0.0570.png'   
```

<br />

### 4. ETC
#### 4-1. Inference Time, GPU Memory

|  Sample  | Magnification | Width, Height | Batch size | GPU Memory (GB) | Processing Level | Processing Time |
| :-------: | :-----------------: | :-----: | :------: | :----: | :-: | :------------: |
|    [S12-32488_HE](./doc/S12-32488_HE.PNG) | 40x |   (10001, 10014)    |   8    | 8.15 | 4 |  3.5 minutes (1.5 m for inference, 2 m for postprocessing)  |
|    [S12-32488_HE](./doc/S12-32488_HE.PNG) | 40x |   (10001, 10014)    |   8    | 8.15 | 1 |  7 minutes (4.3 m for inference,  m for postprocessing)  |

