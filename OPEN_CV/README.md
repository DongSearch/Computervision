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

# Background remover
remove background, remaining only moving objects
## Key Point
- **Contour**: Removes small noisy blobs by keeping only contours whose area exceeds a threshold, preserving object-level shapes (e.g., people).
- **Temporal filtering**  : Stabilizes detection across frames by blending current and previous masks, reducing flickering and short-term noise.

- *history* (MOG2)
Controls how long past frames influence the background model; larger values help keep slowly moving people as foreground.
- *varThreshold* (MOG2)
Defines sensitivity to motion; higher values reduce noise but may miss subtle movements.
- *MIN_AREA* (Contour filtering)
Minimum contour area to be considered a valid object; too large removes distant or partially visible people.
- *TEMPORAL_ALPHA* (Temporal filtering)
Weight of the previous frame in temporal smoothing; higher values increase stability but reduce responsiveness to new motion.

---

## 📌 Consequences(Observation)

###  basic(only)
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/a14a9a36-0c83-41a2-ac71-3916841d1fce" />


* I use only basic filtering of it, but there are a lot of noise, and only guess certain people
  
### option + Contouring + Temporal filtering
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/c0fdf8ad-1cf5-47ae-8954-64d8ee833256" />

* it can detect people more smoothly, contour filtering finds contour overall based on object, and temporal filtering remove non-movable or slow object
