# Improving_CNN_Performance_Using_Regularization

## 🔗 Google Colab Notebook

You can view and run the full implementation of this project using Google Colab:

[Open in Google Colab](https://colab.research.google.com/drive/1GSN5m4eBcEtQJnutJKQdnCdKwEwbGDDx?usp=sharing)

# 🌿 Laboratory Work 4 Reflection  
## Improving CNN Performance Using Regularization, Fine-Tuning, and Advanced Evaluation

---

## 📌 Final Model Overview

For this Laboratory Work 4, I evaluated the baseline model, improved the model performance, and applied advanced evaluation techniques such as **classification report, confusion matrix, ROC/AUC, and Grad-CAM**.

After several experiments, the best-performing model was the **fine-tuned MobileNetV2 model**.

| Metric | Final Result |
|---|---:|
| **Validation Accuracy** | **85.31%** |
| **Validation Loss** | **0.4573** |
| **Macro Precision** | **85.91%** |
| **Macro Recall** | **85.34%** |
| **Macro F1-score** | **85.02%** |
| **Macro AUC** | **0.9946** |

> The model reached the **Good Model benchmark in terms of validation accuracy**, since it achieved more than 85%. However, the validation loss is still slightly above the ideal target of below 0.4, so there is still minor room for improvement.

---

# A. Model Evaluation Analysis

---

## 1. What were the weakest-performing classes based on the confusion matrix?

Based on the classification report and confusion matrix, some of the weaker-performing classes were:

- `pandanus_tectorius`
- `Solidago sempervirens`
- `Ipomoea_pes-caprae`
- `Vigna marina`
- `Canavalia rosea`

These classes had lower recall or F1-score compared to the stronger classes. This means the model sometimes confused them with other plant species. One possible reason is that many plant classes have similar leaf shapes, flower colors, and natural backgrounds.

---

## 2. How did Precision, Recall, and F1-score vary across classes?

The scores varied depending on how visually distinct each plant class was.

Some classes performed very well, such as:

- `Cakile maritima`
- `Wedelia trilobata`
- `Heliotropium curassavicum`
- `Crinum asiaticum`
- `Abronia maritima`

These classes had high precision, recall, and F1-scores because the model was able to recognize their features more clearly.

Other classes had lower scores because they looked similar to other plant species or had more variation in lighting, image angle, and background. Overall, the model achieved a **Macro F1-score of 85.02%**, which shows that most classes were classified well.

---

## 3. What does a low recall indicate in your model?

A low recall means that the model failed to correctly identify many actual images from a certain class.

For example, if a plant class has low recall, it means some images that truly belong to that class were predicted as another plant species. In this activity, low recall usually happened when two plant classes had similar leaves, flowers, or textures.

---

## 4. How does AUC score reflect model performance compared to accuracy?

Accuracy measures how many predictions were correct overall. AUC gives a deeper evaluation because it measures how well the model separates one class from the others using prediction probabilities.

In my final model, the validation accuracy was **85.31%**, while the AUC score was **0.9946**. This means the model was very strong at distinguishing between the 20 plant classes, even though some individual predictions were still incorrect.

---

# B. Model Improvement

---

## 5. How did data augmentation affect validation accuracy?

Data augmentation helped improve validation accuracy by creating variations of the training images. It allowed the model to see images with different rotations, zoom levels, flips, and contrast changes.

This helped because plant images can appear in different angles, lighting conditions, and backgrounds. Because of augmentation, the model became less dependent on memorizing exact training images and improved its ability to generalize to validation images.

---

## 6. Why is Batch Normalization important in CNNs?

Batch Normalization is important because it helps stabilize and speed up the training process. It normalizes the activations inside the network so that the model can learn more consistently.

In this activity, Batch Normalization helped the model train deeper layers more effectively and reduced unstable learning behavior during model improvement and fine-tuning.

---

## 7. What role did Dropout play in improving your model?

Dropout helped reduce overfitting by randomly turning off some neurons during training. This prevented the model from relying too much on specific features from the training images.

Since my dataset contains similar plant species, Dropout helped the model learn more general patterns instead of memorizing only the training set.

---

## 8. How did Early Stopping prevent overfitting?

Early Stopping helped prevent overfitting by stopping the training process when the validation performance stopped improving.

This was useful because the training accuracy could continue increasing while the validation accuracy stopped improving or started decreasing. Early Stopping restored the best model weights, which helped keep the model from overtraining.

---

# C. Performance Comparison

---

## 9. What improvements were observed after modifying the model?

There was a clear improvement from the baseline model to the final fine-tuned model.

| Model | Validation Accuracy |
|---|---:|
| **Baseline Model** | **58.45%** |
| **Enhanced Custom CNN** | **around 66%–67%** |
| **Fine-tuned MobileNetV2** | **85.31%** |

The final model significantly improved the validation accuracy, F1-score, and AUC score. The model became better at recognizing different plant species and separating visually similar classes.

---

## 10. Which enhancement contributed the most to performance improvement? Why?

The biggest improvement came from **transfer learning and fine-tuning using MobileNetV2**.

My custom CNN improved the baseline model, but it still struggled with visually similar plant species. MobileNetV2 already had strong feature extraction ability, so it was able to learn more meaningful image features such as leaf shape, flower structure, texture, and color patterns.

Fine-tuning helped the model adapt those learned features to my own plant dataset.

---

## 11. Did the gap between training and validation accuracy decrease? Explain.

The final model still had a small generalization gap, but it was much better compared to earlier overfitting models.

The training accuracy was around **91%**, while the validation accuracy was around **85%**. This gives a gap of around **6%**. Ideally, the gap should be around 5% or lower, so the model still shows slight overfitting.

However, compared to previous models where the training accuracy was high but the validation accuracy was much lower, the final model generalized much better.

---

# D. Explainability: Grad-CAM Integration

---

## 12. How did Grad-CAM help in understanding model predictions?

Grad-CAM helped me understand which parts of the image influenced the model’s prediction. Instead of only seeing the predicted class, Grad-CAM showed the regions that the model focused on when making a decision.

This helped me check whether the model was looking at important plant features such as leaves, flowers, or stems instead of focusing on the background.

---

## 13. Did the improved model focus on more relevant regions? Provide evidence.

Yes, the improved model generally focused on more relevant regions of the plant.

Based on the Grad-CAM overlay, the highlighted areas were mostly located on the leaves, flower regions, or plant body. This means the model was using meaningful visual features for prediction.

However, in some misclassified samples, the model still focused on general leaf areas or background details. This shows that visually similar plant species can still confuse the model.

---

## 14. Why is explainability important in real-world AI applications?

Explainability is important because it helps users understand why an AI model made a prediction.

In real-world AI applications, users need to trust the model’s decision. For example, in plant classification, Grad-CAM can show whether the model is focusing on the correct plant parts. If the model focuses on the background instead of the plant, the prediction may not be reliable.

Explainability helps developers identify model weaknesses, improve performance, and make AI systems more transparent.

---

# 🧠 Final Reflection

Overall, this laboratory activity helped me understand that improving a CNN model is not only about adding more layers. It also requires proper evaluation, regularization, dataset checking, performance comparison, and explainability.

The final model achieved:

- **85.31% validation accuracy**
- **85.02% macro F1-score**
- **0.9946 macro AUC**

The model reached the **Good Model benchmark in terms of validation accuracy**, but the validation loss was still slightly above the ideal target. This means the model performed well, but it can still be improved through better dataset cleaning, more balanced image quality, and further fine-tuning.

---
This laboratory activity helped me understand that improving a CNN model is not only about adding more layers. It also requires proper evaluation, regularization, data quality checking, and explainability tools like Grad-CAM.
