# Neural Style Transfer (NST)

PyTorch 기반으로 구현한 **Neural Style Transfer** 프로젝트입니다.  
VGG-19 pretrained model과 Gram Matrix 기반 style loss를 사용하여  
콘텐츠 이미지와 스타일 이미지를 결합하는 다양한 실험을 수행했습니다.

본 프로젝트는 **하이퍼파라미터(α, β), layer 선택, loss 설계가  
결과 이미지에 미치는 영향**을 분석하는 데 중점을 둡니다.

---

## 📌 Consequences
### original image
![hanok](https://github.com/user-attachments/assets/7c8e8bcd-465d-46ae-a96d-51db20e7eb2b) ![gihbri](https://github.com/user-attachments/assets/6c70fc0a-1344-4e53-bef2-e391d18919b4)


###  Alpha Variation
<img width="1415" height="956" alt="image" src="https://github.com/user-attachments/assets/8ac008ee-5475-47cb-a015-1924250d9802" />

* I observe that as the style weight (α) increases, more details from the style image—such as textures and colors—are incorporated into the output image.
### Extract from different layers
<img width="436" height="418" alt="image" src="https://github.com/user-attachments/assets/e723acf8-7846-4b27-8292-5424d4c62c80" />
<img width="398" height="421" alt="image" src="https://github.com/user-attachments/assets/ee430bd6-9389-4026-b304-35fcbafe1e50" />


 ### Tv_weight Variation
---

## 🧠 Experiment



## 📉 Limitations

- Gram Matrix discards spatial information
- VGG features are texture-biased
- Difficult to achieve fully natural photo-level compositing
- α scaling alone cannot overcome strong content constraints

These limitations reflect the **fundamental constraints of  
VGG + Gram-based NST**, rather than implementation issues.

### Content Representation
- Extracted from intermediate VGG layers
- Default layer:
  - `r42`

### Style Representation
- Gram Matrix of feature maps
- Default layers:
  - `r21`, `r31`, `r41`, `r51`

---

## 🧮 Theory


---

