# DADS7202_HW02 The pre-trained CNN
![image](https://user-images.githubusercontent.com/107410157/197267919-ac58b7ea-f75d-4610-9408-eb14e26ceb85.png)

## Introduction: 

Nowadays, there are a lot of mobile phones in the market. Because the appearance of mobile phone are very the same, it makes the customer very confused when they try to find a phone. When searching mobile phone on Google, the picture always looks like the brand that search but it isn't. Because of this problem, our team comes up with the idea to classify the picture of mobile phones. From our discussion, we choose 4 mobile phone brands that we think it's easy to confuse and hard to tell which brand is the right one.

There are a lot of mobile phone brands in the market. **The appearance of every mobile phone are look the same** so it hard for the customer to find the phone that they want. Because of this problem, we have the idea to classify the picture of mobile phone brands.

* 📱 **`Apple (iPhone)`**    
* 📱 **`Huawei`**
* 📱 **`OPPO`**   
* 📱 **`Samsung`**


## 📋 Image Dataset
 - [✨ Dataset](https://drive.google.com/drive/folders/16B2ut6co3qQ1eBGqpvZMb8ZJNta62rp4?usp=sharing) <br>
Link to download the dataset: https://drive.google.com/drive/folders/16B2ut6co3qQ1eBGqpvZMb8ZJNta62rp4?usp=sharing

We collected 4 brands of mobile phone image(3 color channel) datasets which are Apple(iPhone), Huawei, OPPO, and Samsung that are still sale in 2022. We try to select various images in every dimension of the phone (frontside, backside, and some specific areas such as the camera ) source of the official image are from  BaNANA online shop **`"https://www.bnn.in.th/th"`** and unofficial image from Facebook market place. The total image that we collected from 2 sources is 434 images (iPhone 100 images, Huawei 124 images, Oppo 109 images, and Samsung 100 images).


## Assumption:
We think the pre-trained model that validation on ImageNet dataset can't classify present moblie phone design. We choose 3 models including VGG16, ResNet152V2, and MobileNet for study in this project.

In this case our assumption about the pre-trained model is the largest model will have the best accuracy which is VGG16
and the lowest accuracy is MobileNet.

## Data pre-processing and splitting :
* Image Preparation : collected all images in .jpg and manually put them into the brand's folder then in a sub-folder split into 2 folders "train_ds" and "test_ds "of each brand. Ratio of train, validation and test as shown in table 1.

* We label images by importing datasets with tf.keras.utils.image_dataset_from_directory image will be labeled as the sub-folder name.

* label class : 0,1,2, and 3 mean Apple, Huawei, Oppo, and Samsung as ordered. then used "sparse_categorical_crossentropy" to calculate Loss.

* Resizing image dataset to 224 x 224 to match with model requirement.

![image](https://user-images.githubusercontent.com/107410157/197308226-29a91b68-5a4d-467e-9e3f-402624fc36fa.png)


**Table 1: Data pre-processing and splitting**
![MicrosoftTeams-image](https://user-images.githubusercontent.com/86920208/197348853-1eac9f2a-a8c0-490f-b524-6c8b382d9b65.png)


## Before Fine-tuning:
From testing all the pre-trained model (**`"VGG16"`**, **`"ResNet152V2"`** , **`"MobileNet"`**) before fine-tuning the result of all model show accuracy = 0 which mean all these 3 models can't tell the mobile phone brand that we want. Example of model prediction show iPhone = projector,  Huawei = iPod, Oppo = switch, and Samsung = notebook.

**Table 2: Result before fine-tuning**
| Model |Test Accuracy | Test Loss | Runtime with GPU (H:M:S) | GPU Name |
| :------ | :----: |:-----:|:-----:|:-----:|
|**`"VGG16"`**| 0 | 18.2531 | 0:02:41 | Tesla T4
|**`"MobileNet"`**| 0 | 13.3670 | 0:02:41 | Tesla T4
|**`"ResNet152V2"`**| 0 | 2508.23 | 0:03:10 | Tesla T4

Result of pre-trained model.
![image](https://user-images.githubusercontent.com/107410157/197340501-6658c397-1659-48f6-bbd2-8c6a4364263e.png)

![MicrosoftTeams-image (2)](https://user-images.githubusercontent.com/86920208/197349159-4e116fc5-017e-49b3-98ac-6dca7eda4dfb.png)


## Data Augmentation :
We decided to do data augmentation to increase the number of dataset and minimize overfit and each model use different data augmentation combination to perform the best result of each model as follow.

**Table 3: Data Augmentation**
| Model         | Image data augmentation                     |
| ------------- |---------------------------------------------|
| VGG16         |tf.keras.layers.RandomFlip                   |
|               |tf.keras.layers.RandomTranslation            |
| MobileNet     |tf.keras.layers.RandomFlip                   |
|               |tf.keras.layers.RandomRotation               |
| ResNet152V2   |tf.keras.layers.RandomFlip                   |
|               |tf.keras.layers.RandomTranslation            |
|               |tf.keras.layers.RandomRotation               |

## After Fine-tuning:

To get more accuracy, the parameter that we adjust from the pre-trained model.

**Table 4: Fine-tuning parameters**
| Model | epoc |Unfreeze pre-train model (Part Feature Extraction)|  Feature extraction layer | classifier | Optimizer | Initial learning rate |
| :---- | :--: |:----------:|:-----------------:|------------|:---------:|:-------------:|
|**`"VGG16"`**|15|10-19|Conv2D : 3 Layer|activation="relu" & "tanh"|Adam|0.0001|
|**`"MobileNet"`**|100|All|-|activation="relu" & Dropout =0.5|Adam|0.0001|
|**`"ResNet152V2"`**|30|130-564|-|activation="relu" & Dropout =0.2|Adam|0.0001|

**Train accuracy/Train loss**
![image](https://user-images.githubusercontent.com/107410157/197338882-ee1b09af-3c49-4c88-a945-29f753e8cb0b.png)

After running 5 times, 3 models after fine-tuning results say the models can predict the brand of mobile phone. However, the accuracy is different in each model as show in the table below.

**Table 5: Result after fine-tuning**
| Model | AVG. Test Accuracy | SD Test Accuracy | AVG. Test Loss | SD Test Loss | AVG. Runtime with GPU (H:M:S) |
| :---- | :----------------: |:----------------:|:-----:|:-----:|:-----:|
|**`"VGG16"`**|0.730|±0.0167|0.715|±0.0749|0:02:50|
|**`"MobileNet"`**|0.870|±0.0313|0.631|±0.1281|0:07:14|
|**`"ResNet152V2"`**|0.795|±0.0447|0.873|±0.1333|0:02:46|



The result of models (Actual brand - Predict Brand)
![image](https://user-images.githubusercontent.com/107410157/197340370-b178c8a0-4478-4d77-a95f-2cfe677bb599.png)
![image](https://user-images.githubusercontent.com/107410157/197340236-3596088e-27cb-46c3-9c76-139dc42eed42.png)
![image](https://user-images.githubusercontent.com/107410157/197340204-583dced2-bc65-476a-a6da-c19d97be76ac.png)



## Results:
All of the models that we choose,  **`"MobileNet"`** have the best accuracy score. Result after using random seed 5 times average test accuracy is 87.00% +/-3.13% and the average test loss is 63.13% +/-12.81%, the average runtime with GPU is 7 min 14 sec but if ranking model performance by runtime **`"MobileNet"`** is the slowest because it uses the most epoc and limitation of Google Colab.

![image](https://user-images.githubusercontent.com/107410157/197309429-bc6da6a4-b423-4b94-83ab-ac2f2abe1b16.png)





## Discussion & Conclusion:

1. Model before fine-tuning
* Model cannot distinguish mobile phone brands but can be predicted as things similar in ImageNet Dataset, such as an iPod.
* Train Accuracy is equal to zero because we freeze the whole model so it doesn't learn any new image dataset.
* Loss value derived from an initial loss that the model randomly generates.
2. Model before fine-tuning
* Based on our preliminary assumptions, we expect VGG 16 have the best accuracy. But, as a result, it turns out that MobileNet which is a small model that gives the best results.
* Unfreeze layer feature extraction has a significant effect on the performance. MobileNet had the most unfreeze, followed by RestNet152V2 and VGG16 respectively, corresponding to the predicted accuracy.
* Model architecture has an important role in simplifying the fine-tuning performance. With the more complex model, there is a chance to increase accuracy more easily.
* Preparing a small amount of train dataset resulted in the inability to adjust the batch size and cause overfit problems. In addition, there was a case of train accuracy hitting the ceiling by equal to 1, after it was going through multiple epochs.
* Train/Test Dataset segmentation has an important role, the team found the problem data collected is not completely mixed or random. ( Team random only Train/Valid dataset )
* Increasing the variety of Data augmentation does not increase accuracy. The team found that the more Data augmentation, the lower the accuracy value. It should be put to suit the situation.
* Choosing a model with a large number of parameters or increasing the number of layers, must take into account the amount of RAM memory. The size of the model that is suitable for the size of data, and the appropriate parameter tuning is important.

![MicrosoftTeams-image (11)](https://user-images.githubusercontent.com/107410157/197311406-017fbef7-854f-415a-a92b-a6b41c0b95ce.png)

## References version:
| Library | Version |
| :------ | :----: |
|Python|3.7.15|
|Numpy|1.21.6|
|TensorFlow|2.9.2|
|GPU|NVIDIA GeForce RTX 3060 Laptop GPU|
|Colab Pro|Tesla P100-PCIE-16GB/A100-SXM4-40GB|

## References:
* Code from class DADS7202
* https://keras.io/api/applications/
* https://keras.io/examples/vision/image_classification_from_scratch/
* https://keras.io/guides/preprocessing_layers/
* https://www.tensorflow.org/tutorials/load_data/images
* https://www.tensorflow.org/tutorials/images/classification


## 🙋 Deepsleep's Member:
| %|ID|Name |Responsibility  |
| :------ | ------ |:------|:-------|
|⭐ **`20%`** | **`6410414007`**  | 👦 Athit Santikarn  |**`Collect data(Oppo)`**, **`Write result`**, **`conclusion report`**|
|⭐ **`20%`** | **`6410422020`**  | 👩 Suphanun Sukamta |**`Collect data(Samsung)`**, **`Write result`**, **`conclusion report`**|
|⭐ **`20%`** | **`6410422004`**  | 👦 Chokchai Kenpho  |**`Collect data(Apple)`**, **`Train model-VGG16`**|
|⭐ **`20%`** | **`6410422009`**  | 👦 Noppol Anakpluek  |**`Preprocess data`**, **`Train model-ResNet152V2`**|
|⭐ **`20%`** | **`6420422006`**  | 👦 Watcharakorn Pasanta  | **`Collect data(Huawei)`**, **`Train model-MobileNet`**|


## End credit: 
**This project is a part of Course DADS7202 Deep Learning, Data Analytics and Data Science, NIDA.**

