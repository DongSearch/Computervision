# Template Matching
Template matching finds the location in an image whose pixel pattern is most similar to a given template using a sliding-window comparison.
## Key Point
- **Cosine**: Removes the mean intensity, so it compares relative pixel variations (patterns) rather than absolute brightness.(find max)    
- **Square**: Compares absolute pixel values directly.(find min)  
---

## 📌 Consequences(Observation)
### original image
<img width="784" height="451" alt="image" src="https://github.com/user-attachments/assets/e6cf706e-9fff-457d-9615-7af91e9747c9" />

###  Crop
<img width="940" height="356" alt="image" src="https://github.com/user-attachments/assets/374293ba-0a69-418f-9d69-28bf8c3f2d41" />
<img width="977" height="321" alt="image" src="https://github.com/user-attachments/assets/03ec98cb-88e3-4df1-895d-3dad995d659f" />

* Using the entire image as a template leads to incorrect detections because background and grayscale intensity similarities dominate the matching.(above)  
Restricting the template to a discriminative object region reduces background influence and improves localization accuracy.(below)  
### Cosine Similarity vs Square difference
<img width="829" height="438" alt="image" src="https://github.com/user-attachments/assets/390bd0a4-2aac-4f57-bd0c-58d4828c486f" />

* Cosine similarity compares relative intensity patterns, making it robust to illumination changes and effective at highlighting object structures.  
Square difference compares absolute pixel values, so shadows and background with similar brightness can cause inaccurate matches.  

