---
toc: false
layout: post
description: Building interpretable Boosting Models with IntepretML
comments: true
categories: [Explainable AI, Machine learning Interpretibility]
image: images/2021-05-18-A-better-way-to-visualize-decision-trees/0.png
show_image: true
show_tags: true
title: "Interpretable or Accurate? Why Not Both?"
---

*The article was originally published [here](https://towardsdatascience.com/a-better-way-to-visualize-decision-trees-with-the-dtreeviz-library-758994cdf05e?sk=ad5fcdf665e07388a829bb5320be9a6f)*


![Image by [Kingrise](https://pixabay.com/users/kingrise-4297632/?utm_source=link-attribution&utm_medium=referral&utm_campaign=image&utm_content=3183317) from [Pixabay](https://pixabay.com/?utm_source=link-attribution&utm_medium=referral&utm_campaign=image&utm_content=3183317)](https://cdn-images-1.medium.com/max/2560/1*kWy3VIPUPhLGl4G2-ccTPw.png)

As summed up by [Miller](https://arxiv.org/abs/1706.07269), interpretability refers to the degree to which a human can understand the cause of a decision. A common notion in the machine learning community is that a trade-off exists between accuracy and interpretability. This means that the learning methods that are more accurate offer less interpretability and vice versa. However, of late, there has been a lot of emphasis on creating inherently interpretable models and doing away from their black box counterparts. In fact, Cynthia Rudin argues that [explainable black boxes should be entirely avoided for high-stakes prediction applications](https://www.nature.com/articles/s42256-019-0048-x) that deeply impact human lives. So, the question is whether a model can have higher accuracy without compromising on the interpretability front?

Well, EBMs precisely tries to fill this void. EBMs, which stands for [Explainable Boosting Machine](https://www.youtube.com/watch?v=MREiHgHgl0k), are models designed to have accuracy comparable to state-of-the-art machine learning methods like Random Forest and Boosted Trees while being highly intelligible and explainable.

This article will look at the idea behind EBMs and implement them for a Human Resources case study via [InterpretML](https://arxiv.org/pdf/1909.09223.pdf), a Unified Framework for Machine Learning Interpretability.

## Machine learning Interpretability — A primer

Machine Learning is a powerful tool and is being increasingly used in multi-faceted ways across several industries. The AI models are increasingly used to make decisions that affect people’s lives. Therefore, it becomes imperative that the predictions are fair and not biased or discriminating.

![Advantages of having Machine learning Interpretability in pipeline | Image by Author](https://cdn-images-1.medium.com/max/2000/1*0r29CPjHgDAVwyMki8LSzg.png)

Machine learning interpretability has a vital role to play in such situations. Interpretability gives you the ability not only to discover a model’s mispredictions but analyze and fix the underlying cause too. Interpretability can help you debug your model, detect overfitting and data leakage, and most importantly, inspire trust between models and humans by giving explanations.

### Interpretability Approaches

The approaches employed to explain the models' predictions can be grouped into two major categories depending upon the type of machine learning models.

### 1. Glassbox Models vs. Blackbox explanations

Algorithms that are designed to be interpretable are called Glassbox models. These include algorithms like simple decision trees, rule lists, linear models, etc. Glassbox approaches typically provide exact or lossless explainability. This means it is possible to trace and reason about how any prediction is made. The interpretation of GlassBox models is **Model-specific** because each method is based on some specific model’s internals. For instance, the interpretation of weights in linear models count towards [model-specific explanations](https://christophm.github.io/interpretable-ml-book/taxonomy-of-interpretability-methods.html).

Blackbox explainers, on the contrary, are **model agnostic**. They can be applied to any model, and such are **post-hoc** in nature since they are applied after the model has been trained. Blackbox explainers work by treating the model as a BlackBox and assume that they only have access to the model's inputs and outputs. They are particularly useful for complex algorithms like boosted trees and deep neural nets. Blackbox explainers work by repeatedly perturbing the input and analyzing the resultant changes in the model output. The examples include [SHAP](https://arxiv.org/abs/1705.07874), [LIME](https://arxiv.org/abs/1602.04938v3), [Partial Dependence Plot](https://christophm.github.io/interpretable-ml-book/pdp.html)s, etc., to name a few.

![](https://cdn-images-1.medium.com/max/2000/1*8ov3dWV39WHkx8SG6pMXWA.png)
<sub>Glassbox vs. Blackbox explainability approaches | Image by Author

### 2. Local vs. Global explanations

Another category could be depending upon the scope of explanations. Local explanations aim to explain individual predictions, while global explanations explain the entire model behavior.

Now that we have sufficient intuition into the interpretability mechanism employed by machine learning models, let’s switch gears and understand EBMs in more detail.

---

## Explainable Boosting Machine (EBMs)

[EBMs](https://dl.acm.org/doi/10.1145/2339530.2339556) are Glassbox models designed to have accuracy comparable to state-of-the-art machine learning methods without compromising accuracy and explainability*.*

EBM is a type of [generalized additive mode](https://projecteuclid.org/journals/statistical-science/volume-1/issue-3/Generalized-Additive-Models/10.1214/ss/1177013604.full)l or GAM for short. Linear models assume a linear relationship between the response and predictors. Thus, they are unable to capture the non-linearities in the data.

`Linear Model: y = β0 + β1x1 + β2x2 + … + βn xn`

To overcome this shortcoming, in the late 80’s statisticians [Hastie & Tibshirani developed generalized additive models](https://projecteuclid.org/journals/statistical-science/volume-1/issue-3/Generalized-Additive-Models/10.1214/ss/1177013604.full)(GAMs), which keep the additive structure, and therefore the interpretability of the linear models. Thus, the linear relationship between the response and predictor variable gets [replaced by several non-linear smooth functions](https://datascienceplus.com/generalized-additive-models/)(f1, f2, etc.) to model and capture the non-linearities in the data. GAMs are more accurate than simple linear models, and since they do not contain any interactions between features, users can also easily interpret them.

`Additive Model: y = **f1**(x1) + **f2**(x2) + … + **fn** (xn)`

EBMs are an improvement on the GAMs utilizing techniques like gradient boosting and bagging. EBMs include pairwise interaction terms, which increases their accuracy even further.

`EBMs: y = Ʃifi (xi) + Ʃijfij(xi , xj) + Ʃijk fijk (xi , xj , xk )`

The following talk from Richard Caruana, the creator of EBM, goes deeper into the intuition behind the algorithm.

 <iframe src="https://medium.com/media/d5cacb248136b23c76025cc3518f8fdd" frameborder=0></iframe>

The vital point to note here is that even after all these improvements, EBM still preserves the interpretability of a linear model but often matches the accuracy of powerful BlackBox models, as shown below:

![Classification performance for models across datasets (rows, columns)|The official paper: [InterpretML: A Unified Framework for Machine Learning Interpretability](https://arxiv.org/pdf/1909.09223.pdf)](https://cdn-images-1.medium.com/max/2118/1*-gnKXfPsi5FHYcPiaLK50Q.png)

---
 
 ## Case Study: Predicting Employee Attrition Using Machine Learning
>  Here is the [nbviewer link](https://nbviewer.jupyter.org/github/parulnith/Data-Science-Articles/blob/main/Interpretable%20or%20Accurate%3F%20Why%20not%C2%A0both/Interpretable%20or%20Accurate%3F%20Why%20not%C2%A0both.ipynb) to the code notebook in case you want to follow along.

![[](https://pixabay.com/photos/get-me-out-escape-danger-security-1605906/)](https://cdn-images-1.medium.com/max/3840/1*289fHah3E3BX9CkKrIJegw.jpeg)
<sub>Andrew Martin from Pixabay

It’s time to get our hands dirty. In this section, we’ll train an EBM model to predict employee attrition. We’ll also compare the performance of EBMs with other algorithms. Finally, we’ll try and explain the predictions that our model made with the help of a tool called InterpretML. What is interpretML? Let’s find out.
 
 ### IntepretML: A Unified Framework for Machine Learning Interpretability

EBMs come packaged within a Machine Learning Interpretability toolkit called [InterpretML](http://Unified Framework for Machine Learning Interpretability). [I](https://github.com/interpretml/interpret)t is an open-source package for training interpretable models as well as explaining black-box systems. Within InterpretML, the explainability algorithms are organized into two major sections, i.e., **Glassbox models** and **Blackbox explanations**. This means that this tool can not only explain the decisions of inherently interpretable models but also provide possible reasoning for black-box models. The following code architecture from the [official paper](https://arxiv.org/pdf/1909.09223.pdf) sums it nicely.

![code architecture from the official paper | Source: [InterpretML: A Unified Framework for Machine Learning Interpretability](https://arxiv.org/pdf/1909.09223.pdf)](https://cdn-images-1.medium.com/max/2030/1*MxM1QHK31w16F9U0d5t7CQ.png)

As per the authors, InterpretML follows four fundamental design principles:

![](https://cdn-images-1.medium.com/max/2000/1*3KXqAPM9YmONgN9wZf0x5g.png)

InterpretML’s also offers an interactive visualization dashboard. The dashboard provides valuable insights about the nature of the dataset, model performance, and model explanations.

### Dataset

We’ll use the publicly available [IBM HR Analytics Employee Attrition & Performance](https://www.kaggle.com/pavansubhasht/ibm-hr-analytics-attrition-dataset) dataset. This dataset contains data about an employee’s age, department, gender, education level, etc., along with information on whether the employee left the company or not, denoted by the variable Attrition. “No” represents an employee that did not leave the company, and “Yes” means an employee who left the company. We will use the dataset to build a classification model to predict the employees’ probability of attrition.

Here’s a snapshot of the dataset features.

![Features of the dataset | Image by Author](https://cdn-images-1.medium.com/max/2000/1*lVoiOjtNnnD8QgJBiEDCgQ.png)

As stated above, InterpretML supports training interpretable models (**glass-box**), as well as explaining existing ML pipelines (**Blackbox **), and is supported across Windows, Mac, and Linux. Currently, the following algorithms are supported in the package:

![Algorithms are supported by InterpretML | Image by Author](https://cdn-images-1.medium.com/max/2000/1*n4r1n6T5p0f6c3AJUtWEEg.png)

**Exploring the dataset**

The first task is always to explore the dataset and understand the distributions of various columns. InterpretML provides histogram visualizations for classification problems.

![](https://cdn-images-1.medium.com/max/2720/1*N7-QigRky33FIP3BdsSe6g.png)

![Histogram visualization | Image by Author](https://cdn-images-1.medium.com/max/2410/1*G67PKzjun3wszNTHnWQTHg.gif)

**Training the model**

Training an EBM is relatively easy with InterpretML. After preprocessing our dataset and splitting it into training and a test set, the following lines of code get the job done. InterpretML conforms to the familiar scikit learn API.

![](https://cdn-images-1.medium.com/max/2720/1*wzfPy8pYgK0HL4ypdy4-5w.png)

Once the model is trained, we can visualize and understand the model’s behavior globally and locally.

**Global Explanations**

Global Explanations help better understand the model’s overall behavior and the general model behavior across the population.

![](https://cdn-images-1.medium.com/max/2720/1*9MeZEKvWkmXYkFJ1my29TQ.png)

The first graph that we see is the Summary plot which states that the Overtime variable is the most critical feature in determining if someone will leave the company or not.

![Viewing Global Explanations | Image by Author](https://cdn-images-1.medium.com/max/2346/1*j_mIItfKqWYn-wZtsccKOQ.gif)

We can also look deeper into each feature plot on drilling down.

![Effect of age on attrition | Image by Author](https://cdn-images-1.medium.com/max/2356/1*-FhB-jPrPGb5Y4v31voP7w.png)

The score here refers to the logit since the problem is a classification one. The higher you are on the y-axis, the higher your odds of leaving the company. However, after around 35 years of age, this behavior changes, and you have more chances of staying back.

**Local Explanations**

Local Explanations help us understand the reasons behind individual predictions and why a particular prediction was made.

![Viewing Local Explanations | Image by Author](https://cdn-images-1.medium.com/max/2000/1*giADRNtdAvltV_E_L59BWg.png)

**Comparing the performance with other models**

It is also easy to compare the performance of different algorithms and display the results in a dashboard format.

![Comparison Dashboard | Image by Author](https://cdn-images-1.medium.com/max/2920/1*rge1s00o89Id6o6J1pTntA.jpeg)

**Training BlackBox models**

If required, InterpretML can also train BlackBox models and provide explanations for the predictions. Here is an example of a trained Random ForestClassifier model on the same dataset and the subsequent explanation provided by LIME.

![Analyzing Blackbox models | Image by Author](https://cdn-images-1.medium.com/max/2000/1*jhruLFrrbUv020peVaLZHA.jpeg)

## Conclusion

This article showcased how EBMs emerge as an excellent choice for creating both interpretable and accurate models. Personally, when machine learning models are used in high-stakes decisions, interpretability should be given a higher preference over a loss of few points of accuracy. It is not only important to see if a model works, but we as machine learning practitioners should also care about how it works and whether it works without any intentional bias.

## References

A lot of sources and papers were referenced for this article which have been linked in the article. The primary source, however, was the [official paper of InterpretML](https://arxiv.org/pdf/1909.09223.pdf) and its [documentation](https://interpret.ml/docs/ebm.html).
