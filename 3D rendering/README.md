# 3D Rendering

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



- **Hierarchical sampling**:  

this objective is we want to focus on that part that has higher weight, which means we want to do sampling more densly nearby object. First, we do even sampling(beacuase we don't know anything at the beginning, and then we get weights from them, and we can narrow down more based on weight



---

## 📌 Consequences(Observation)
### original image
<img width="977" height="374" alt="image" src="https://github.com/user-attachments/assets/e33f7d12-0570-443d-932d-83a2f6ebe30f" />  
  
https://github.com/user-attachments/assets/222d75f2-e33e-4144-9852-22bbe20599bf

### with Hierarchical sampling
<img width="1260" height="374" alt="image" src="https://github.com/user-attachments/assets/7f56a09e-401a-40c4-8dc8-f8a6f2b8b586" />


https://github.com/user-attachments/assets/8652da61-47cf-4283-84e6-d5e6670ba2f3


