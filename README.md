# Instance Segmentation using Mask R-CNN

There are various techniques that are used in computer vision tasks such as classification, semantic segmentation, object detection and instance segmentation. Instance Segmentation is identifying each object instance for every known object within an image. It assigns a label to each pixel of the image.

![person](https://user-images.githubusercontent.com/47391270/71358534-54c62e00-25af-11ea-8ff1-bf788c22b6c8.png)

### What is Mask R-CNN ?

The Mask R-CNN algorithm was introduced by He et al. in their 2017 paper, [*Mask R-CNN*](https://arxiv.org/abs/1703.06870). It is an instance segmentation technique which locates each pixel of every object in the image instead of the bounding boxes. It has three main stages:
1. **Backbone network** which is a standard CNN such as ResNet50 or ResNet101. It is used to generate the feature maps.
2. **Region proposal network (RPN)** to propose candidate object bounding boxes.It uses a CNN to generate the multiple Region of Interest(RoI) using a lightweight binary classifier. 
3. **RoI Align network** outputs multiple bounding boxes and warps them into a fixed dimension. Warped features are then fed into *fully connected layers* to make classification (using Softmax) and boundary box prediction (using regression). 
The features are also fed into *Mask classifier*, which consists of two CNN’s, to output a binary mask for each RoI. Mask Classifier generates masks for every class without competition among classes.
![mrcnn](https://user-images.githubusercontent.com/47391270/71436870-2febcb00-2715-11ea-937e-6bf3bf525517.png)
### Data

The images have been taken from the Leukocyte Images for Segmentation and Classification Database [(LISC)](http://users.cecs.anu.edu.au/~hrezatofighi/Data/Leukocyte%20Data.htm). 
![Screenshot from 2019-12-25 13-04-24](https://user-images.githubusercontent.com/47391270/71437336-38450580-2717-11ea-9732-4e39cc5c0147.png)
The images have to segmented into these 5 types of WBC's:
1. Basophil 
2. Eosinophil
3. Neutrophil
4. Lymphocyte
5. Monocyte

### Training the model

1. Download/fork Matterport's [Mask R-CNN](https://github.com/matterport/Mask_RCNN).
2. Download the training images and divide them into train and validation set.
3. In the root directory of Mask R-CNN creating a folder named WBC consisting of images and their corresponding masks. It's structure should be as follows:
```bash
    WBC
    ├──train(same for val)
    │   ├──image
    │   │   ├──Basophil
    │   │   │   ├──Basophil_01.png
    │   │   │   └── ...
    │   │   ├──Eosinophil
    │   │   │   ├──Eosinophil_01.png
    │   │   │   └── ...
    │   │   .
    │   │   .
    │   │   .   
    │   ├──mask
    │   │   ├──Basophil
    │   │   │   ├──Basophil_01.png
    │   │   │   └── ...
    │   │   ├──Eosinophil
    │   │   │   ├──Eosinophil_01.png
    │   │   │   └── ...
    │   │   .
    │   │   .
    └── └── .
```
4. Download the pre-trained COCO [weights](https://github.com/matterport/Mask_RCNN/releases)(mask_rcnn_coco.h5) and save them in the root directory of Mask R-CNN.
5. Also save the `WBC.py` file in this repository into the Mask R-CNN folder.
6. To start training, open terminal in the folder and write
`python3 WBC.py train --dataset=WBC --weights=coco`

### Evaluation of the model

The model was trained for 75 epochs with 60 steps per epoch. The following are some predictions of the model on images in the **validation** set:

![Screenshot from 2019-12-22 14-38-11](https://user-images.githubusercontent.com/47391270/71446932-e029f580-274e-11ea-9492-69201170db54.png)

![Screenshot from 2019-12-22 14-42-57](https://user-images.githubusercontent.com/47391270/71446952-1bc4bf80-274f-11ea-8fad-b556ec07ff31.png)

![Screenshot from 2019-12-22 14-48-01](https://user-images.githubusercontent.com/47391270/71446953-2a12db80-274f-11ea-8528-aeb71a4f9e7a.png)



