# Building Extraction using U-Net Semantic Segmentation Architecture for Pre/Post Damage Monitoring

## Table of Contents  
- [Project Description](#project-Description)  
- [Datasets](#datasets)  
- [Workflow](#workflow)  
- [Preliminary Results](#preliminary-results) 

## Project Description 

Our main objective in this project was to investigate methods of building extraction and damage assessment throughout the state of California to support disaster mitigation and monitoring efforts, particularly from wildfire impacts. We implemented a deep learning semantic segmentation method to extract building footprint within fire boundaries from 2013 to 2018 using 1m spatial resolution NAIP imagery. 

<figure class="image">
  <img src="./docs/assets/Figure6.png" alt="workflow">
  <figcaption>Figure2. Boundaries of fires across CA that will be used as training/testing dataset for building polygons and pre-/post- disaster NAIP imagery. </figcaption>
</figure>

## Datasets 

Pre-derived building polygons for training purposes were acquired from Microsoft's building footprints opendata [source](https://www.microsoft.com/en-us/maps/building-footprints). While assessing the availability and completeness of various data sources from Open Street Map (OSM) to county-level datasets, we concluded this was the most useful for our purposes.


<figure class="image">
  <img src="./docs/assets/Figure1.png" alt="dataset visualization">
  <figcaption>Figure 1. Comparison of possible training dataset for building extraction workflow in Napa County.</figcaption>
</figure>

<figure class="image">
  <img src="./docs/assets/Figure4.png" alt="campfire post fire">
  <figcaption>Figure 3. Example of post-fire stuctural damage and loss for 2018 Camp fire in Paradise, CA.</figcaption>
</figure>

## Workflow 

The first phase of the project involved building footprint extraction using the U-Net semantic segmentation model architecture. 

We used Fastai’s dynamic Unet model with an ImageNet-pretrained resnet 34 encoder with a multi-combination loss function (i.e. Dice Loss and Focal Loss). The combination loss was particularly useful for its ability to fine-tune the weights for each class to account for disproportionate sampling w/ ‘contact’ class. 

Annotation included 3 labels (footprint, boundary, and contact) to help ensure differentiation between structures in close contact with one another. 


<figure class="image">
  <img src="./docs/assets/Figure5.png" alt="workflow">
  <figcaption>Figure 4. Overview of high-level workflow and project objectives. </figcaption>
</figure>

## Preliminary Results 

After training the dataset (with pre-fire imagery), we also performed model inference on post-fire imagery to visualize how the model will capture the changes. Sure enough, differences in building footprint detection pre-/post fire were seen that can be useful for identifying additional change detections for each fire instance. 

<figure class="image">
  <img src="./docs/assets/Figure7.png" alt="building detection 1">
  <figcaption>Figure5. Predicted building polygons for pre-/post- fire. Example shows model correctly detected building, contrary to training dataset. </figcaption>
</figure>

<figure class="image">
  <img src="./docs/assets/Figure8.png" alt="building detection 2">
  <figcaption>Figure6. Predicted building polygons for pre-/post- fire.  </figcaption>
</figure>


Additional visualizations from interactive maps can be found below, overlaying the original building polygons with predicted. Challenges were found particularly for connected buildings (condos) and structures covered by trees. 

<figure class="image">
  <img src="./docs/assets/Figure9.png" alt="comparison with true data">
  <figcaption>Figure7. Comparison between ground-truth and predicted building polygons. Colors representing true and false postives/negatives. </figcaption>
</figure>

The predicted building footprints were combined with a surveyed structural damage assessment layer to be used in phase 2 of the project which aims to automate damage detection. 

<figure class="image">
  <img src="./docs/assets/Figure10.png" alt="damage data">
  <figcaption>Figure8. Map of predicted building polygon with spatial joined structural damage survey data taken post-fire. </figcaption>
</figure>