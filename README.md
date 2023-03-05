# Where's Wallabies: Animal Detection / Recognition, by Troy Wilson & Daniel Barajas Torres


## SETUP

Naviate to the MegaDetector [github](https://github.com/microsoft/CameraTraps/blob/main/megadetector.md)

Downlaod the model **"MegaDetector v5a (.pt)"**

## Follow the [Using the model](https://github.com/microsoft/CameraTraps/blob/main/megadetector.md#using-the-model) section of the Megadetector github.
### Make sure to follow the section for **your operating system** and to take note of the paths for cameratraps, ai4eutils, and yolo5

Use those paths to set the pythonpath below:
```
Windows:
set PYTHONPATH=%PYTHONPATH%; {cameratraps}; {ai4eutils}; {yolov5}

Mac/Linux:
export PYTHONPATH="{cameratraps}:{ai4eutils}:{yolov5}"
```
*NOTE: This pythonpath has to be set each time the conda env is reset.*

Inside the cameratraps-detector enviornment install jupyter noteboook
```
pip3 install jupyter
```

open the notebook
```
jupyter notebook &
```

## ~Inside the notebook~

## Are variables predefined?
If the *'saved_vars'* folder exists and contains the four files:

- saved_train_array.npy
- saved_test_array.npy 
- saved_train_labels.npy
- saved_test_labels.npy 

Then the majority of the pipeline can be skipped.

Skip to the 'Load Data' section of the notebook and run the three cells the follow that title. If successful the final cell of the three should print results similar to this:
```
loading predefined variables
(31278, 64, 64, 3)
(31278,)
(639, 64, 64, 3)
(639,)
```
Then run the cells to load ResNet/Preprocess as well as the helper functions.

**Skip the standard sequential model section and proceed to the K-fold model**

Finally run the cell with the K-fold model and sit back!


## If variables are not predefined

When variables are not predefined then the pipeline likely must be run in its entirety. Assure that the *'all_images'* folder exists and has sub-folders named exactly the same as the categories. If this folder and sub-folders do not exist then they MUST be created and populated with the correlating data.

Follow the notebook down, running the cells, and run the cell following the title **'Run Detection'**. This cell will take a very long time (~10-12 hours) and once finished will result in a JSON file named 'all_images_detection.json' that contains all of the bounding box information for the images.

Load the JSON with the cell following the title **'Load JSON from MegaDetector'**

Continue to the section titled **Crop Images to their bounding boxes** these cells should setup and crop the images when provided the JSON file we just created.

Continue to the section **Setup training and testing sets** these cells, as expected, will take the cropped images from the previous section and create the folder *'data'* and its subfolders *'test'* and *'train'* populated with sub-folders correlating to the categories that are further populated by the cropped images.

**SKIP THE AUGMENTATION STEP**

Continue to the **Load Data** section and run the three cells following it. After running this cell, the values will be saved to files, so that the entire pipeline doesn't need to run again.

Continue and run the cell following the title **Load and Preprocessing for Resnet**

Continue and run the three cells following the title **Some helper functions**

**Skip the standard sequential model section and proceed to the K-fold model**

Finally run the K-fold model and sit back!