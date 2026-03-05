# Single Shot Multi-Box Detector

- SSD was developed to perform both classification and localization simultaneously in a single forward pass, similar to YOLO. Compared to early versions of YOLO (such as YOLOv1 and YOLOv3), SSD achieved better accuracy. However, as later versions of YOLO significantly improved, SSD gradually became less competitive.


## Structure and Characteristic
- VGG 16 Backbone : Instead of using fully connected (FC) layers at the end of VGG-16, SSD converts them into 1×1 convolutional layers.Therefore, High-resolution feature maps detect small objects with fine details, while low-resolution feature maps detect larger objects with broader context.
  
- Anchor Boxes : SSD uses predefined default boxes (anchor boxes) with various aspect ratios and scales.
  default anchor 1:1, 2:1, 1:2, 3:1, 1:3
  it improves detection precision and significantly accelerate inference compared to two-stage detectors such as R-CNN-based models. Each feature map cell predicts offsets and class probabilities for multiple default boxes.
  
- NMS(Non-Maximum Suppression) : After prediction, SSD applies Non-Maximum Suppression (NMS) to remove redundant bounding boxes. Only the boxes with the highest confidence scores are retained. Without NMS, multiple overlapping boxes would remain for the same object, resulting in noisy detections.
  
- Loss function :
  <img width="483" height="138" alt="image" src="https://github.com/user-attachments/assets/c936390c-ed28-4ed7-a910-03f62d3ac185" />

  x : default box
  c : class
  l : bbox coordinate
  g : gt coordinate
  N : the number of boxes
* Localization loss : smooth L1 LOss -> combination of L2 and L1 Loss(strong to outlier and guarantee derivertive)

- Center ffset : Bounding box regression is performed using center offsets. The predicted offsets are normalized by the size of the default box, which improves scale invariance and helps maintain translation invariance.

- Hard Negative Mining : There is a strong imbalance between: Positive samples (objects) vs Negative samples (background)   
To address this issue, SSD uses Hard Negative Mining, which selects the most difficult negative samples based on confidence loss.

## Pipeline

Foward -> Box Matching(IOU check) -> Hard Negative Mining -> Loss calc -> Backprop

## Result

the most left image is original image, and last three images shows based on differnt confidences(0.2,0.5,0.7)

<img width="2790" height="1494" alt="image" src="https://github.com/user-attachments/assets/0c10e278-3cf2-484c-b7d8-3104d234ad93" />
