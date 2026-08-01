---
layout: default
title: Blog
---

[Home/Research Blog](/) | [ART](/art) | [AboutMe](/resume)

---
### "AI in Education: Machine Learning-based Revised Bloom Taxonomy Classifiers"
*26 July 2026*

The surge in AI-generated educational materials has outpaced our capacity to validate their pedagogical quality. Now, we can ask Large Language Models (LLMs) to quiz and assess our understanding of a topic. How do we ensure that AI-generated questions are aligned with Pedagogical Frameworks? Research studies have shown that Machine Learning models can automate and evaluate pedagogical alignment of educational materials at scale. 

In this blog, I demonstrate building ML models to assess the cognitive levels of text using the revised Bloom Taxonomy framework and public dataset. I ask these key questions,

(1) How do we build classifier models from text? and

(2) What are the limitations of ML models in assessing pedagogical alignment?


**Data**. I utilize the BloomBERT dataset compiled by [Ryan Lau (2025)](https://github.com/RyanLauQF/BloomBERT). The dataset contains ~6,000  entries and corresponding human-labeled with Bloom Level Taxonomy from studies of Devane et al, Mohammed et al. (2020), and Yahya et al (2012).


### A. Theoretical Foundations

#### A.1 Revised Bloom Taxonomy
The Revised Bloom Taxonomy for cognitive depth is one pedagogical frameworks used to assess the quality of assessment questions. The framework classifies questions into lower-order thinking tasks (i.e., remember, understand, and apply) to higher-order cognitive tasks (i.e., analyze, evaluate, and create). 

Bloom Trigger verbs influence the cognitive level of a text. **Figure 1** shows word clouds of frequent words appearing in each remember and evaluate Bloom level questions from the dataset. Low-order cognitive questions use words such as "write", "recall", "list" while high-order questions use words like "evaluate", "defend", and "recommend" requiring more student comprehension.

<p align="center">
<img src="./images/Blog_Bloom_1_WordCloud.png?raw=true" width=350>
</p>

**Figure 1**. The frequent stemmed (truncated) words found for text classified under Remember and Evaluate Bloom levels.

#### A.2 Machine Learning models
Research in Natural Language Processing (NLP) have developed models of detecting Bloom signals. The general approach is to map words into numerical features ($X$) via a mapping function ($M$), i.e., Term frequency-inverse document frequency (TF-IDF) with Part-of-Speech tags (POS), Word2Vec embeddings, or tokens for pre-trained transformer models.

$$
    X = M[\text{"Discuss the following ..."}] = (0.1, 0.04, 0.11, ...) 
$$

These features are then modeled against a corresponding label $Y$ - the six progressive Bloom levels (0:"remember", 1:"understand", 2:"apply", 3:"analyze", 4:"evaluate", 5:"create"). Models that can be explored such as multi-nomial logistic regression, Random Forest, XGBoost, and Transformer models. The performance of the models is assessed using the confusion matrix and macro F1-score.

#### A.3 Model Interpretability
Using Local Interpretable Model-Agnostic Explanations (LIME), I assess the important words that influence the prediction. I hypothesize that Bloom trigger verbs would be the top features that drive the prediction. However, we can ask how the prediction changes when Bloom trigger verbs are not present.

#### A.4 Pipeline
**Figure 2** below summarizes the pipeline in building classifier models from text - which answers **Question 1**.  

First, text inputs are provided with their corresponding labels. Second, the text inputs are processed by standard NLP techniques (e.g., nominalization, word stemming/lemmatization). The pre-processed words are then mapped to defined vector embeddings (e.g., TFPOS-IDF, Word2Vec, Tokenization for transformer models). Third, these feature vectors serve as inputs to machine learning models (XGBoost, Multi-nomial Logistic Regression, Random Forest, Support Vector machines, or Transformers). Fourth, the performance of the models are evaluated in terms of classification scores, explainability. Models is also tested for Dataset Drift and robustness.


<p align="center">
<img src="./images/Blog_Bloom_pipeline.png?raw=true" width=500>
</p>

**Figure 2**. The pipeline for building ML-based text classifiers.

### B. Results
I performed a standard auto-ML pipeline to evaluate the train/test performance of different ML models. **Figure 3** shows the resulting confusion matrices of two best models XGBoost and DistilBERT (referred as BERT). The results of few-shot prompting with Gemini 3.1 LLM model with few-shot prompting (Gemini 3.1 - FS) is also shown.

<p align="center">
<img src="./images/Blog_Bloom_2_CM.png?raw=true" width=700>
</p>

**Figure 3**. The confusion matrices of different ML models and LLM on the test set. 


We can observe that ML models excel in classifying the Bloom Taxonomy level in the dataset with F1-scores of 0.88 (XGBoost) and 0.89 (BERT). The two models tend to misclassify text that require "remember" and "understand" Bloom level. Notably, few-shot prompting with Gemini 3.1 Flash-lite also showed acceptable results (F1-score = 0.76) but misclassifies higher order cognitive text to just "remember" and "understand".

Using LIME on the BERT model, we can examine the words that influenced the prediction. In the example below, the word "refute" (with LIME weight of 0.41) is a trigger Bloom verb for evaluation (**Figure 4**). Thus, the reader is tasked to evaluate a product design theory based on data.

<p align="center">
<img src="./images/Blog_Bloom_4.png?raw=true" width=350>
</p>

**Figure 4**. Based on LIME, the words "refute", "or", "empirical" tagged the text to be "evaluate" Bloom level.

In this second example, we can find that the model predicts the text to be either understand or apply (**Figure 5**). The presence of the word "sketch" requires reader to apply his/her knowledge using a diagram. In contrast, the word "explain" suggest that the users only need to understand what a torsion dynanometer is.

<p align="center">
<img src="./images/Blog_Bloom_5.png?raw=true" width=350>
</p>

**Figure 5**. Based on LIME, the text Bloom level could either be understand or apply. The word "sketch" suggests that the text is "apply" Bloom level while the word "explain" suggests that the text is "understand" Bloom level.

> **insight**:
> 1. The choice of vector embeddings determines the information represented in the text. For the Bloom Taxonomy Classification task, Mohammed et al (2020) show that trigger verbs is a strong determinant of the Bloom levels. Thus, TFPOS-IDF approach of capturing the weighted occurence of verbs, nouns, adjectives (POS-tags) in a document is sufficient for the tasks. However, the meaning words change when paired/followed by other words. In this case, a more complex word representation such as Word2Vec and BERT embeddings would be suitable.
> 
> 2. Indeed, both examples demonstrate the usefulness of LIME to diagnose the model predictions by highlighting the key words (features) that influence prediction. Instructional designers can use this as:
> (a) a guide in varying the cognitive level of the text to a higher/lower Bloom levels to support instructional scaffolding; and
> (b) an assessment tool to evaluate the clarity of the instruction (i.e., Does it targeting one or multiple cognitive levels).
> 
> 3. Dataset shift is an important aspect to consider especially when evaluating new dataset. It is common issue for pre-trained ML models to underperform on a new data particularly when the characteristics of the new text is different from that of the train set (Waheed et al 2021). Further text processing and model retraining are ways to address dataset shift.

### C. App Demo
I've prepared an application to run the trained XGBoost model in evaluating text. You may access the "ML-based Bloom Classifier" app (url = "appappsgit-fo5u86tmrnqbcfwd9yb7uh.streamlit.app"). Password is "education".
<p align="center">
<img src="./images/Blog_Bloom_app.png?raw=true" width=700>
</p>

### Final thoughts
Deploying automated classifiers into educational systems introduces strategic opportunities. However, successful integration also requires clear operational safeguards.

Machine Learning models are capable to evaluate assessment quality at scale. Instructional designers can leverage this automated feedback balance cognitive load across curricula. The issue on dataset shift requires continuous monitoring of model performance and retraining when applied to new academic domains.

Institutions should adopt a hybrid oversight framework. While machine learning models perform the initial automated screening, human educators remain the final validation authority.


Disclaimer of AI use: Claude Sonnet was used to improve the flow of the discussion.


### Reference:
Lau, Ryan. (2025). BloomBERT: A Task Complexity Classifier. https://github.com/RyanLauQF/BloomBERT.

Mohammed, Muna, and Nazlia Omar. 2020. “Question Classification Based on Bloom’s Taxonomy Cognitive Domain Using Modified TF-IDF and Word2vec.” PLoS ONE 15 (3): e0230442. https:
//doi.org/10.1371/journal.pone.0230442.

Yahya, Anwar Ali, Zakaria Toukal, and Addin Osman. 2012. “Bloom’s Taxonomy–Based Classification for Item Bank Questions Using Support Vector Machines.” In Modern Advances in Intelligent Systems and Tools, edited by Wei Ding, He Jiang, Moonis Ali, and Mingchu Li. Springer Berlin Heidelberg.

Waheed, Abdul, Muskan Goyal, Nimisha Mittal, Deepak Gupta, Ashish Khanna, and Moolchand Sharma. 2021. “BloomNet: A Robust Transformer Based Model for Bloom’s Learning Outcome Classification.” In Proceedings of the 4th International Conference on Natural Language and Speech Processing (ICNLSP 2021), edited by Mourad Abbas and Abed Alhakim Freihat. Association for Computational Linguistics. https://aclanthology.org/2021.icnlsp-1.24/.