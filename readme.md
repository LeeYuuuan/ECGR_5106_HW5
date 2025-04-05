# Homework 5 — Sequence-to-Sequence Modeling

**Name**: Liyuan Zhang
**Student ID**: 801432783  
**GitHub Repo Link**: [Public GitHub Repository](https://github.com/LeeYuuuan/ECGR_5106_HW5)  

This report covers four main problems focusing on Transformer-based sequence models, applied to character-level language modeling and English↔French machine translation tasks. We report training/validation losses, accuracies, model complexities, and qualitative evaluations.

---

## Problem 1 (20 pts)

### Task Overview
We train and validate a Transformer model on a given text sequence. We use sequence lengths **10**, **20**, and **30** and compare these results against RNN-based models (with or without cross-attention). We report:
- Training loss, validation accuracy  
- Execution time  
- Model complexity (parameter count)  

### Key Figures

1. **Training & Validation Loss + Accuracy (Seq=10)**  
   ![P1 Loss & Accuracy](figs/p_1_loss_acc.png)

2. **Comparing Seq=20 & 30**  
   ![P1 Seq 20 vs 30](figs/p_1_seq_20_30.png)

3. **Validation Comparison**  
   ![P1 Validation Comparison](figs/p_1_Validation_Comparison.png)

### Problem 1 Analysis

- **Sequence Length Effects**  
  - As we increase the sequence length (from 10 to 30), we observe higher accuracy and lower training loss.  
  - However, due to the limited size of the dataset, there is a risk of overfitting. For instance, at **seq=30**, the training loss continues to decrease but the test loss actually increases, indicating potential overfitting.  
  - Interestingly, **seq=10** achieves the highest overall accuracy in this setup.

- **Transformer vs. RNN**  
  - The Transformer model does not perform as well as the RNN-based networks.  
  - A likely explanation is that RNN models (including variants such as GRU/LSTM) can effectively memorize or fit smaller datasets, while the Transformer—having more parameters—typically requires a larger dataset to reach its full potential. As a result, the Transformer may underperform on small-scale data.


## Problem 2 (20 pts)

### Task Overview
We build a Transformer model for the Tiny Shakespeare dataset. We train with **sequence lengths 20 & 30**, then also try **seq=50**. We focus on:
- 2 Transformer layers, 2 heads (baseline)  
- Additional hyperparameter combos: 1,2,4 layers × 2,4 heads  
- Compare with RNN-based models  
- Report training/validation losses, accuracies, execution time, model complexity

### Key Figures

1. **Loss & Accuracy Curves**  
   ![P2 Loss & Accuracy](p_2_loss_acc.png)

2. **Layer & Head Comparison**  
   ![P2 Layer & Head Comparison](p_2layer_and_head_comparison.png)

### Observations
- **Increasing heads/layers**: Tends to reduce validation loss and improve accuracy, at the cost of higher parameter counts and training time.  
- **Seq=50**: Gains can be modest but training time and overfitting risks increase.  
- **RNN vs Transformer**: Transformers generally handle longer contexts better; RNNs may converge quickly for shorter sequences but can struggle to maintain accuracy on bigger contexts.

---

## Problem 3 (40 pts)

### Task Overview
Here, we develop a Transformer-based encoder-decoder for **English→French** translation. We test:
- 1, 2, 4 layers × 2, 4 heads (8 combos)  
- Compare with RNN-based models (with/without attention)  
- Report training loss, validation loss, validation accuracy  
- Provide some **qualitative** translation checks

### Key Figures

1. **Training & Validation Loss**  
   ![P3 Loss](p_3_loss.png)  

2. **Validation Accuracy**  
   ![P3 Accuracy](p_3_acc.png)

### Observations
- **Transformer** significantly outperforms plain RNNs.  
- **Attention** in RNN narrows the gap but usually cannot surpass a deeper Transformer.  
- **Qualitative** checks indicate more fluent translations from deeper Transformers (e.g., 4 layers, 4 heads).

---

## Problem 4 (20 pts)

### Task Overview
We repeat Problem 3 but reverse the translation direction — **French→English**. We again explore 1, 2, 4 layers × 2, 4 heads, comparing with RNN-based approaches. We:
- Train on full dataset  
- Evaluate on full dataset (training/validation loss, validation accuracy)  
- Provide qualitative validation of translations

### Key Figures

1. **Training & Validation Loss**  
   ![P4 Loss](p_4_loss.png)

2. **Validation Accuracy**  
   ![P4 Accuracy](p_4_acc.png)

### Observations
- **French→English** can be slightly more challenging depending on the morphological complexity in French.  
- Deep Transformers again reach the best accuracy, with a higher compute overhead.  
- Qualitative translations show Transformers handle long or complex sentences more gracefully than baseline RNNs.

---

## Overall Summary

1. **Transformer vs RNN**  
   - Transformers generally converge faster and yield higher accuracy for longer sequence tasks. RNN with attention is decent but usually not as strong as a multi-headed Transformer.  

2. **Effect of Sequence Length**  
   - Shorter sequences (e.g., seq=10 or 20) train faster but capture less context, limiting accuracy.  
   - seq=30 or 50 can further improve performance but cost more time and risk overfitting.  

3. **Layers & Heads**  
   - More layers and heads generally improve performance in Transformers, yet also raise parameter count and slow training.  
   - Optimal choice depends on resource constraints.  

4. **Translation Direction**  
   - English→French vs. French→English may differ slightly in accuracy, often due to morphological or syntactic complexities of the source or target language.  

5. **Future Work**  
   - Incorporating beam search decoding can improve generative quality.  
   - Subword tokenization (e.g., BPE) often yields more robust translations.  
   - Larger datasets and advanced regularization are beneficial for deeper models.

---

**References**  
- *List any references (papers, resources, or lecture notes) used.*

