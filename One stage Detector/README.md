# YOLO

While R-CNN prcoess two stage(classification and regression), YOLO can process them only one stage at expense of accuracy. Here I would like to introduce three version of Yolo that are changed representatively (v5, v8, v10)

## Background
- **Yolo v5**:
  <img width="720" height="455" alt="image" src="https://github.com/user-attachments/assets/edf22be8-e5a4-4e7d-84c9-8863b83f6b8d" />

Yolo consists 3 parts principally, Backbone, Net, Head.
Backbone(CSPDarknet): the role is to extract features using Cross Stage Partial Network(Conv+BN+SiLU, Residual,Down sampling)
Neck(PANet) : They capture position and semantic information using bi-directional structure(FPN + PAN)
*FPN : large feature(location) -> upsample -> concate with small feature(semantic information)
*PAN : small feature(semantic inforamtion) -> downsample -> concate with large feature(localization)
Head : predict class and box 

Auto Anchor(data compatibility) : the center of having high accuracy from R-CNN, anchor box is automatically generated
Mosaic Augumentation(data diversity or augumentation) : they merge 4 images to one,which improve detecion of small obejct and reduce batch size reliance

different size depends on needs : nano, small, medium,large, XLarge

- **Yolo v8**:
<img width="850" height="478" alt="image" src="https://github.com/user-attachments/assets/9ac8247d-778f-41b7-a7da-68925a821a49" />


Anchor free : Anchor improves accuracy, but main cause of slowness. so Instead they predict center point of obejct directly and calculate distance from it.
Decoupled Head : seperate classification and regression
C2f(Cross Stage Partial + Feature Flow) :

  
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


