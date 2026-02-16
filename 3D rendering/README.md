<img width="172" height="45" alt="image" src="https://github.com/user-attachments/assets/8a31b615-eb9a-461d-89dc-c6d7b9624aca" /># 3D Rendering
3D renering is the process of simulating how light travels in a 3D scene and interacts with obejcts to produce a 2D image.

## Key Point
- **Homogeneous Transformation Matrix**:
  <img width="1350" height="375" alt="image" src="https://github.com/user-attachments/assets/792f5198-c38d-44fc-bd89-61b4b644365a" />
  this Matrix describes an entire doordinate frame(both direction and position in space)
  R means rotation matrix(orientation), t is translation vector(position)
  last 4th row make it possible to put multiplication and addition in same matrix

- **positional encoding**:
  <img width="1426" height="232" alt="image" src="https://github.com/user-attachments/assets/eb9c0d0e-7fef-4222-8ee7-c022fc5bf024" />

In LLMs, positional encoding tells the model where each word is in a sentence.
In NeRF, positional encoding helps the network represent detailed spatial variations like sharp edges and textures.

- **Ray**:  
  <img width="172" height="45" alt="image" src="https://github.com/user-attachments/assets/a62a36d6-1ac0-4fc4-93fe-fb79050549e4" />

it calculate current ray vector per pixel using ray origin(camera positio), ray direction, distance parameter

- **Transmittance**:  
  <img width="302" height="81" alt="image" src="https://github.com/user-attachments/assets/543a6026-bcfb-4937-b27f-20fe52556970" />

it is the possibility for the ray to keep rest starting from t

- **Weight**:    
<img width="108" height="33" alt="image" src="https://github.com/user-attachments/assets/efd72ecf-2350-4a42-8c5f-ff2ce8ef3f8b" />

it is importance to contribute to decide color at i-th pixel

- **Volume Rendering**:
  <img width="1255" height="301" alt="image" src="https://github.com/user-attachments/assets/05129a68-e63b-4759-b3af-06bc310abd97" />

it computes the color of a pixel by integrating the radiance along a ray weighted by the density and transmittance at each sampled point.
Desnity(sigma) : how likely light stops there
Transmittance(T) : how much light survives until that point
Distance(delta) : how thick that small segment is

---

## 📌 Consequences(Observation)
### original image
<img width="977" height="374" alt="image" src="https://github.com/user-attachments/assets/e33f7d12-0570-443d-932d-83a2f6ebe30f" />  
  
https://github.com/user-attachments/assets/222d75f2-e33e-4144-9852-22bbe20599bf





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


