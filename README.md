![Image](https://github.com/UMU689/ct-angel-imgs/blob/master/logo.png)
# CT-Angel
---

## Table of Contents

* Background
* Data
* Model Development
* Usage
* Directory Structure
* About the author

---
## Background
Computed tomography (CT) is the preferred imaging method for diagnosing 2019 novel coronavirus (COVID19) pneumonia. CT-Angel aimed to construct a system based on deep learning for detecting COVID-19 pneumonia on high resolution CT, relieve working pressure of radiologists and contribute to the control of the epidemic.
## Datasets
### Datasets  source
1. Hospital
From Renmin Hospital of Wuhan University (Wuhan, Hubei province, China). 
2. Instruments
Included Optima CT680, Revolution CT and Bright Speed CT scanner (all GE Healthcare).
### Datasets  amount
1. Raw datasets
* 46,096 CT images from 106 patients
    25989 images from 51 COVID19 patients
    20107 images from 55 controls
2. Selected datasets(after filtering those images without good pneumonia)
* 35355  CT images selected
    20886 images from 51 COVID19 patients
    14469 images from 55 controls
## Model  development
### Workflow  diagram 
### Model  training
1. Training a model for extracting valid regions of CT images
    We first trained UNet++ to extract valid areas in CT images using 289 randomly selected CT images and tested it in other 600 randomly selected CT images. The training images were labelled with the smallest rectangle containing all valid areas by researchers. The model successfully extracted valid areas in 600 images in testing set with an accuracy of 100%.
2. Training a model for detecting suspicious lesions in CT images
    For detecting suspicious lesions on CT scans, 691 images of COVID-19 pneumonia infection lesions labelled by radiologists and 300 images randomly selected from patients of non-COVID-19 pneumonia were used. Taking the raw CT scan images as input with a resolution of 512×512, and the labelled map from the expert as output, UNet++ was used to train in Keras in an image-to-image manner. The suspicious region was predicted under a confidence cutoff value of 0.50, and a prediction box pixel of over 25. 
### Model  testing
1. Testing datasets
| Methods | COVID-19 Patients amount | COVID-19 images amount | Other Patients amount | Other images amount |
| :----: | :----: | :----: | :----: | :----: |
| Retrospective testing | 11 | 4382 | 31 | 9369 |
| Prospective testing | 16 | / | 11 | / |
2. Testing results
| Methods | Sensitivity | Specificity | Accuracy | PPV | NPV |
| :----: | :----: | :----: | :----: | :----: | :----: |
| Retrospective testing | |||||
| Per patient | 100% | 93.55% |95.24%|84.62%|100%|
| Per image | 94.34% | 99.16% |98.85%|88.37%|99.61%|
| Prospective testing(Per patient) | 100% | 81.82% |92.59%|88.89%|100%|
`Ps: PPV: positive prediction value,NPV: negative prediction value.`
* Representative images of model testing
## Usage
### Environmental  dependence
| Tools | Version |
| :----: | :----: |
| Python | 3.5+ |
| Tensorflow | 1.13.1 |
| Keras | 2.2.4 |
| Unet++ | / |
| OpenCV | 3.4.2 |
| CUDA | 10.1 |
### Instructions for use
## Directory Structure
```
├── Readme.md                   // help
├── app                         // 应用
├── config                      // 配置
│   ├── default.json
│   ├── dev.json                // 开发环境
│   ├── experiment.json         // 实验
│   ├── index.js                // 配置控制
│   ├── local.json              // 本地
│   ├── production.json         // 生产环境
│   └── test.json               // 测试环境
├── data
├── doc                         // 文档
├── environment
├── gulpfile.js
├── locales
├── logger-service.js           // 启动日志配置
├── node_modules
├── package.json
├── app-service.js              // 启动应用配置
├── static                      // web静态资源加载
│   └── initjson
│       └── config.js         // 提供给前端的配置
├── test
├── test-service.js
└── tools
```
## About the author
