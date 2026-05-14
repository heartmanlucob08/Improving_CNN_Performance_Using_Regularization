# Improving_CNN_Performance_Using_Regularization

## 🔗 Google Colab Notebook

You can view and run the full implementation of this project using Google Colab:

[Open in Google Colab](https://colab.research.google.com/drive/1GSN5m4eBcEtQJnutJKQdnCdKwEwbGDDx?usp=sharing)

# LW4 Reflection Answers  
## Improving CNN Performance Using Regularization, Fine-Tuning, and Advanced Evaluation

## Final Model Summary

For my final LW4 model, I used a fine-tuned **MobileNetV2 transfer learning model** because my previous custom CNN models improved but still struggled to reach the required benchmark. The final fine-tuned model achieved strong performance:

| Metric | Final Result |
|---|---:|
| Validation Accuracy | **85.31%** |
| Validation Loss | **0.4573** |
| Macro Precision | **85.91%** |
| Macro Recall | **85.34%** |
| Macro F1-score | **85.02%** |
| Macro AUC | **0.9946** |

Based on the validation accuracy, the model reached the **Good Model** benchmark of **85%+**. However, the validation loss is still slightly above the ideal target of **< 0.4**, so there is still minor room for improvement.

---

# A. Model Evaluation Analysis

## 1. What were the weakest-performing classes based on the confusion matrix?

Based on the classification report and confusion matrix, the weakest-performing classes were the ones with lower F1-scores and lower recall. In my final model, some of the weaker classes were:

- **pandanus_tectorius**
- **Solidago sempervirens**
- **Ipomoea_pes-caprae**
- **Vigna marina**
- **Canavalia rosea**

These classes were weaker because their visual features can look similar to other plant species. Some plant images also have similar leaf shapes, colors, and backgrounds, which can confuse the model.

---

## 2. How did Precision, Recall, and F1-score vary across classes?

The Precision, Recall, and F1-score varied depending on how easy or difficult each plant class was to distinguish.

Some classes performed very well, such as:

- **Cakile maritima**
- **Wedelia trilobata**
- **Heliotropium curassavicum**
- **Crinum asiaticum**
- **Abronia maritima**

These classes had high scores because the model was able to recognize their features more clearly.

Other classes had lower scores because they looked visually similar to other species or had more variation in image quality. For example, some classes had high precision but lower recall, meaning the model was careful when predicting that class but still missed some actual samples. Overall, the final macro F1-score was **85.02%**, which shows that the model performed well across most classes.

---

## 3. What does a low recall indicate in your model?

A low recall means that the model failed to correctly detect many actual images from a certain class.

For example, if a plant class has low recall, it means many images that truly belong to that plant were predicted as another plant species. In my model, this usually happens when two classes have similar leaves, flowers, or backgrounds. Low recall is important because it shows which classes the model is missing most often.

---

## 4. How does AUC score reflect model performance compared to accuracy?

Accuracy only measures how many predictions were correct overall. AUC gives a deeper view because it measures how well the model separates one class from the others using prediction probabilities.

In my final model, the validation accuracy was **85.31%**, while the AUC score was **0.9946**. This means that even when the model made some wrong predictions, it was still very good at ranking and separating the correct classes from incorrect ones. The high AUC shows that the model learned strong discriminative features.

---

# B. Model Improvement

## 5. How did data augmentation affect validation accuracy?

Data augmentation helped improve validation accuracy by making the model see different variations of the training images. This included flipping, rotating, zooming, and adjusting contrast.

For my dataset, this was helpful because plant images can appear in different positions, angles, lighting conditions, and backgrounds. Data augmentation helped the model generalize better instead of memorizing the exact training images. However, too much augmentation can also make the images unrealistic, so it needed to be balanced.

---

## 6. Why is Batch Normalization important in CNNs?

Batch Normalization is important because it helps stabilize training. It normalizes the activations inside the network, which allows the model to train more smoothly and sometimes faster.

In my model, Batch Normalization helped reduce unstable learning and supported better generalization. It also helped the model handle deeper layers more effectively, especially during fine-tuning.

---

## 7. What role did Dropout play in improving your model?

Dropout helped prevent overfitting by randomly turning off some neurons during training. This forced the model to avoid relying too much on specific features or memorizing the training data.

In my experiments, Dropout helped improve generalization, especially because my dataset contains visually similar plant species. Without regularization, the model could easily memorize the training images but perform worse on validation images.

---

## 8. How did Early Stopping prevent overfitting?

Early Stopping prevented overfitting by stopping the training process when the validation performance stopped improving.

This was useful because after several epochs, the training accuracy could continue increasing while the validation accuracy no longer improved. Early Stopping helped restore the best model weights instead of keeping the final epoch, which might already be overfitted.

---

# C. Performance Comparison

## 9. What improvements were observed after modifying the model?

There was a clear improvement from the baseline model to the final fine-tuned model.

| Model | Validation Accuracy |
|---|---:|
| Baseline Model | **58.45%** |
| Enhanced Custom CNN | around **66%–67%** |
| Fine-tuned MobileNetV2 | **85.31%** |

The biggest improvement was seen after using transfer learning and fine-tuning. The final model achieved:

- **85.31% validation accuracy**
- **85.02% macro F1-score**
- **0.9946 AUC score**

This shows that the final model learned stronger and more reliable features compared to the earlier custom CNN models.

---

## 10. Which enhancement contributed the most to performance improvement? Why?

The enhancement that contributed the most was **transfer learning with MobileNetV2 fine-tuning**.

My custom CNN models improved slightly, but they still struggled because the dataset has 20 fine-grained plant classes that look similar. MobileNetV2 already has strong feature extraction ability from pretraining, so it was better at detecting patterns such as leaf shape, flower structure, texture, and color.

Fine-tuning the top layers helped the model adapt those learned features to my plant dataset, which is why the validation accuracy increased significantly.

---

## 11. Did the gap between training and validation accuracy decrease? Explain.

The final model still had a small generalization gap, but it was much more controlled compared to earlier overfitting models.

The final training accuracy was around **91%**, while the validation accuracy was around **85%**. This gives a gap of around **6%**. Ideally, the gap should be 5% or lower, so my model still shows slight overfitting. However, compared to earlier models where the training accuracy was high but validation accuracy was much lower, this final model generalized much better.

So, the gap did not become perfect, but it became acceptable and manageable.

---

# D. Explainability: Grad-CAM Integration

## 12. How did Grad-CAM help in understanding model predictions?

Grad-CAM helped me understand which parts of the image influenced the model’s prediction. Instead of only seeing the predicted class, Grad-CAM showed the regions where the model focused when making a decision.

This was helpful because I could check whether the model was looking at the actual plant features, such as leaves, flowers, or stems, instead of focusing on the background.

---

## 13. Did the improved model focus on more relevant regions? Provide evidence.

Yes, the improved model generally focused on more relevant plant regions. Based on the Grad-CAM overlay, the highlighted areas were usually located on the plant body, leaves, or flower regions.

This suggests that the model was using meaningful visual features for prediction. However, in some misclassified examples, the heatmap also showed attention on general leaf areas or background regions. This means the model still sometimes struggles when plant species have very similar visual features.

---

## 14. Why is explainability important in real-world AI applications?

Explainability is important because it helps users understand why an AI model made a certain prediction. In real-world applications, it is not enough for a model to only give an answer. Users also need to trust the prediction.

For example, in plant classification, Grad-CAM can show whether the model is focusing on the correct plant part. If the model focuses on the background instead of the plant, then the prediction may not be reliable. Explainability helps developers identify model weaknesses, improve the system, and make AI decisions more transparent.

---

# Final Reflection

Overall, my LW4 model improved significantly after applying model enhancement techniques and fine-tuning. The baseline model achieved only **58.45% validation accuracy**, while the final fine-tuned model achieved **85.31% validation accuracy** and **0.9946 AUC**.

The model reached the Good Model benchmark in terms of validation accuracy, but the validation loss was still slightly above the ideal target. This means the final model is strong and usable, but it can still be improved through better dataset cleaning, more balanced images, and further tuning.

This laboratory activity helped me understand that improving a CNN model is not only about adding more layers. It also requires proper evaluation, regularization, data quality checking, and explainability tools like Grad-CAM.
