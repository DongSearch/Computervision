# Neural Style Transfer (NST)

PyTorch 기반으로 구현한 **Neural Style Transfer** 프로젝트입니다.  
VGG-19 pretrained model과 Gram Matrix 기반 style loss를 사용하여  
콘텐츠 이미지와 스타일 이미지를 결합하는 다양한 실험을 수행했습니다.

본 프로젝트는 **하이퍼파라미터(α, β), layer 선택, loss 설계가  
결과 이미지에 미치는 영향**을 분석하는 데 중점을 둡니다.

---

## 📌 Consequences
### original image
![hanok](https://github.com/user-attachments/assets/7c8e8bcd-465d-46ae-a96d-51db20e7eb2b)
![gihbri](https://github.com/user-attachments/assets/6c70fc0a-1344-4e53-bef2-e391d18919b4)

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

