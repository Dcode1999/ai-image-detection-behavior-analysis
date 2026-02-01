# AI Image Detection – Behavior Analysis

## Overview
This project presents an evidence-based analysis of a publicly available AI image detection model that attempts to classify images as AI-generated or human-created. Instead of focusing on accuracy metrics or model optimization, the goal is to evaluate real-world behavior, false positives, confidence instability, and practical limitations when such models are applied outside controlled benchmarks.

The analysis is designed to understand how these models behave on diverse image types and to highlight risks associated with over-reliance on automated AI image detection.

---

## Model Used
This project uses the pre-trained model **capcheck/ai-image-detection**, hosted on Hugging Face.  
The model is based on a Vision Transformer (ViT) architecture and performs binary image classification with the labels:

- **Real** — human-created images  
- **Fake** — AI-generated images  

No additional training, fine-tuning, or dataset modification was performed. The model is used strictly as provided by the original author, with full attribution.



---

## Testing Methodology
Testing was conducted using Google Colab with the Hugging Face `transformers` image-classification pipeline.

The evaluation dataset consisted of **eight images** divided into two categories:

- **Four real photographs** sourced from Unsplash (royalty-free), including:
  - Outdoor portraits
  - Natural landscapes
  - Man-made objects in real environments
- **Four AI-generated images**, including:
  - Cinematic fantasy scenes
  - Architectural interiors
  - AI-generated portraits

All images were tested in their original form without additional preprocessing. Model outputs were evaluated based on confidence scores, consistency across image categories, and observed behavior rather than correctness alone.

---

## Screenshots

The screenshots below are taken from the live Hugging Face Space demo and illustrate how the AI image detection model behaves across different image types.

These examples are included to demonstrate:
- High-confidence predictions on AI-generated images
- False positives on real-world photographs
- The probabilistic nature of model outputs

All results shown are model predictions and should not be interpreted as definitive judgments.

### 1. AI-Generated Portrait — High Confidence Detection
<img width="2168" height="1342" alt="Screenshot 2026-02-01 145133" src="https://github.com/user-attachments/assets/83a35cb8-1de5-48f4-ac49-9da7a564409d" />

The model assigns a high probability to the image being AI-generated. This represents a case where the detector aligns with expectations on a synthetic portrait-style image.

---

### 2. AI-Generated Cinematic Scene — Very High Confidence Detection
<img width="2144" height="952" alt="Screenshot 2026-02-01 145211" src="https://github.com/user-attachments/assets/a219e806-3ab1-49f6-b0b0-1e8a95755839" />

A cinematic, AI-generated scene is classified as AI-generated with very high confidence. Such images often exhibit stylistic and structural cues that current detectors are more sensitive to.

---

### 3. Real Photograph (Unsplash) — False Positive Example
<img width="2279" height="1164" alt="Screenshot 2026-02-01 145243" src="https://github.com/user-attachments/assets/5c88be2d-079c-4f52-a764-3baee90f037e" />

A real photograph sourced from Unsplash is classified as AI-generated with high confidence. This example highlights a key limitation of current AI image detectors: false positives on high-quality, professionally shot photographs.

These examples reinforce the core conclusion of this project: current AI image detection models can produce confident predictions, but those predictions are not consistently reliable in real-world scenarios.


---

## Key Observations
- All four real photographs were classified as **AI-generated (Fake)**, often with moderate to extremely high confidence.
- Natural landscape photographs were consistently labeled as Fake with **very high confidence (>99%)**, despite being real-world scenes.
- Outdoor portraits with shallow depth of field were flagged as Fake, indicating a strong false-positive tendency on high-quality photography.
- A real image containing a structured man-made object was also confidently classified as Fake, showing that false positives are not limited to portraits or landscapes.
- AI-generated images were generally classified as Fake, but confidence levels varied significantly:
  - Highly stylized cinematic scenes produced extremely high Fake confidence.
  - Architecturally similar AI images produced inconsistent confidence scores despite visual similarity.
- Confidence scores were unstable across visually similar images, indicating sensitivity to lighting, symmetry, texture smoothness, and color saturation.

---

## Why These Failures Occur
The observed behavior suggests that the model relies heavily on statistical visual patterns such as texture smoothness, symmetry, lighting uniformity, and color gradients. High-quality real photographs—especially landscapes and professionally composed images—often share these characteristics with AI-generated content, leading to false positives.

Additionally, AI-generated images that closely resemble realistic photography can produce lower confidence scores, revealing difficulty in distinguishing between photographic realism and synthetic realism. This indicates that the model’s learned features are not exclusive indicators of AI generation.

---

## Limitations & Ethical Considerations
This analysis demonstrates that current AI image detection models are **not reliable indicators of authenticity** in real-world conditions. High-confidence predictions do not guarantee correctness, and real images may be incorrectly labeled as AI-generated.

These models should be treated strictly as **experimental and probabilistic tools**. They are not suitable for legal, forensic, journalistic, or identity-related decisions. Misclassification—particularly false positives—poses ethical risks when such systems are applied without human judgment or contextual understanding.

---

## Live Demo
A live demonstration of this model is available via a Hugging Face Space, allowing users to test images and observe prediction confidence and instability in real time.

🔗 Hugging Face Space: https://huggingface.co/spaces/SoulWolf2023/ai-image-detection-demo

---

## Conclusion
Based on controlled testing across diverse real and AI-generated images, this project shows that publicly available AI image detection models struggle significantly with real-world photography and exhibit inconsistent confidence behavior. While the model can correctly identify highly stylized AI-generated content, it fails reliably on real images and demonstrates instability across similar inputs. These findings highlight the current limitations of AI-generated image detection and underscore the need for caution when interpreting such model outputs.

---

## Acknowledgements & Attribution

### Model Attribution
This project uses the pre-trained **AI image detection model** published by **CapCheck** on Hugging Face:

- Model: `capcheck/ai-image-detection`
- Hugging Face: https://huggingface.co/capcheck/ai-image-detection

The CapCheck model is based on and fine-tuned from earlier work by **dima806**, building upon the `ai_vs_real_image_detection` model and the `google/vit-base-patch16-224-in21k` architecture.

All credit for model training and development belongs to the original authors. This project does not modify or retrain the model and is focused solely on evaluation, analysis, and demonstration of model behavior.

---

### Image Sources
All real photographs used in this project were sourced from **Unsplash**, a free-to-use photography platform:

- Unsplash: https://unsplash.com

Unsplash images are used in accordance with the Unsplash License and are included only for experimental evaluation and demonstration purposes.

AI-generated images used in testing were created using publicly available image generation tools and are included solely to compare detector behavior across real and synthetic content.

---

### Disclaimer
This project is an independent experimental analysis and is not affiliated with, endorsed by, or associated with CapCheck, dima806, Unsplash, or Hugging Face.

---

## License
This project is released under the **MIT License**.
