# Two-Stage Detection

an object detection approach where a model generates candidate object regions(region proposals) at first step and classifies and refines those regions at second step

## Back Ground
- **Type of Computer vision**:
  - classification : predict the class of the whole image
  - localization : predict the location of object(bounding box)
  - object detection : predict multiple bounding box and class
  - Instance segmentation : detect each object and predict exact pixel-level mask of them 
- **Sliding Window**:fixed-size window slides across image as well as using image pyramid for mutiple scales(very slow, computationally expensive, dominant background)  
- **Selective Search**: start with superpixels(tiny regions), merge similar regions based on texture, color,..., and generate 2000 region proposals, and finally it converts them to into bounding boxes 
- **IoU(Intersection of Union)**: one of measurement to estimate object detection. it calculates how much target and predicted boxes overlap(0:no overlap, 1: perfect overlap, 0.5: normally minimum criterion)
- **GIoU**:no overlap in IOU arises problem with zero gradient making training difficult, so we use it as support of IOU like regularized term adding minimum box including predicted and target box
<img width="307" height="57" alt="image" src="https://github.com/user-attachments/assets/3234be41-ead9-4309-9af3-44243b2f8e7e" />

- **NMS(Non-Maximum-Suppression)**: we want to get only one box per each object,removing others boxes.Therefore, we remove all boxes having less confidence, sort remaining boxes by decending, and pick one highest confidence box, remove all boxex with IoU being higher than threshold(we take them as indicating same object), repeat
- **mAP(Mean of Average)**: for each class, we compute Precision-Recall curve and AUC(AP), and mean of AP over all classes
- **History of Two-Stage Detector**:
  - R-CNN : Use selective search to generate region proposals,and warp each region to fixed size, pass each region through CNN to extract features, and use SVM for classification, finally refine bound box with regression. SVM,CNN,regression, they all need to be trained(very slow, computationally cost , not end-to-end)
  - Fast R-CNN : Pass the whole image through CNN only once and obatin feature map, and project region proposals on to feature map and use RoI Pooling to extract only important features and pass through FNN for classificaion and bounding box regression
  - Faster R-CNN : Faster R-CNN introduces a **Region Proposal Network (RPN)**, which generates object candidate bounding boxes directly from the CNN feature maps. The RPN slides a small convolutional network over the feature map. At each spatial location, it generates k predefined anchor boxes centered at that location. For each anchor, the RPN predicts: An objectness score (object vs background), and Bounding box regression offsets to refine the anchor’s position and size.
---

## 📌 Consequences(Observation)
### original image
![hanok](https://github.com/user-attachments/assets/7c8e8bcd-465d-46ae-a96d-51db20e7eb2b) ![gihbri](https://github.com/user-attachments/assets/6c70fc0a-1344-4e53-bef2-e391d18919b4)


###  Alpha Variation
<img width="1415" height="956" alt="image" src="https://github.com/user-attachments/assets/8ac008ee-5475-47cb-a015-1924250d9802" />

* I observe that as the style weight (α) increases, more details from the style image—such as textures and colors—are incorporated into the output image.
### Extract from different layers(Style)
<img width="436" height="418" alt="image" src="https://github.com/user-attachments/assets/e723acf8-7846-4b27-8292-5424d4c62c80" />
<img width="398" height="421" alt="image" src="https://github.com/user-attachments/assets/ee430bd6-9389-4026-b304-35fcbafe1e50" />

* I extracted features from second to final layers in left picture, but did from forth to final layers in the right one. I can observe characteristics from lower layer like colors
 ### Tv_weight Variation
 <img width="3120" height="576" alt="image" src="https://github.com/user-attachments/assets/6edcaaed-a9ee-4875-bea5-fa44ffce82e8" />

* The TV loss weight controls image smoothness. A very small weight has little to no effect on the output, while a larger weight enforces stronger smoothness. However, excessively large values can introduce artifacts and degrade visual quality.

### Extract from differnt layers(Content)
<img width="347" height="344" alt="image" src="https://github.com/user-attachments/assets/e94f1b19-cc5a-42c3-9697-b4920d44deb7" />
<img width="340" height="346" alt="image" src="https://github.com/user-attachments/assets/498ffb6c-3483-450a-9571-96cf775439dd" />

* In the left image, content features are extracted from a deeper layer (e.g., the 5th block), which preserves higher-level structural information such as object layout and shape.  
In contrast, the right image uses features extracted from a shallower layer (e.g., the 3rd block), which mainly captures lower-level information such as color and texture.  
As a result, the content constraint is weaker in the right image, allowing the style to be more strongly blended into the output.

## 📉 Limitations
- VGG has limited capability to extract disentangled and semantically aligned features at each layer, making it difficult to achieve natural feature blending.
- The Gram Matrix discards spatial information, which leads to loss of structural consistency.
- VGG features are biased toward texture rather than global shape.
- Achieving fully natural, photo-realistic compositing is challenging with VGG-based NST.
- Scaling the style weight (α) alone cannot overcome strong content constraints imposed by deep content layers.



