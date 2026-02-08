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


# Optical Flow(Lucas–Kanade)
It estimates optical flow by assuming local brightness constancy and spatially smooth motion within a small window, and iteratively minimizes the intensity difference between consecutive frames.
## Key Point
- **window size**: A smaller window size can track small objects more precisely, but it is more sensitive to noise and abrupt motion. A larger window size reduces the influence of noise, but may miss small or fine movements.
- **pyramid**  : The Lucas–Kanade method is specialized for tracking small motions. To handle larger displacements, an image pyramid can be used.
- **critierion**  : Defines how long the algorithm continues tracking, based on convergence conditions such as the number of iterations or the error threshold.
---

## 📌 Consequences(Observation)

###  flow(only)
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/0371c171-4588-4225-be37-d3e7e00be585" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/546fbd65-733a-4b40-971d-0f2c7514b8b4" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/8a5f335e-7697-4abf-9bab-d932e50aef91" />


- The algorithm tracks people well when they move consistently at similar speeds and do not overlap.
- The initialization of feature points is critical for stable tracking performance.
- The method is sensitive to changes in brightness and illumination.

# Optical Flow(Farnback)
It estimates optical flow by approximating local neighborhoods with quadratic polynomials and computing pixel-wise displacement from changes in these polynomial expansions across frames.

## Key Point
- **window size**: A smaller window size can track small objects more precisely, but it is more sensitive to noise and abrupt motion. A larger window size reduces the influence of noise, but may miss small or fine movements.
- **pyramid**  : The Lucas–Kanade method is specialized for tracking small motions. To handle larger displacements, an image pyramid can be used.
- **Gausian blur**  : remove noise
---

## 📌 Consequences(Observation)

###  flow(only)
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/1aef3e06-e8a6-40ca-af3b-286ad2c42fad" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/79b305c8-3bab-425b-83c5-2e37f489315a" />


- Farneback computes optical flow for all pixels, which increases computational cost and makes it slower than sparse methods.
- Upsampling(pyramid) can induece accumulation of error from lower pyramid levels
