# SmartLendXAI-AI-Powered-Lending-Decisions-for-Early-Stage-Retailers
SmartLendXAI is an AI-based loan approval prediction system for early-stage retailers with 2–3 years of business history. It uses multiple ML algorithms to assess credit risk and integrates Explainable AI (XAI) to provide transparent, interpretable, and data-driven lending decisions.

This project demonstrates a robust end-to-end approach to **model selection** for loan default prediction. It includes evaluation of 13 ML models, protection against overfitting via generalization scoring, and post-hoc explainability using XAI tools.

---

## 🔁 Project Workflow

### 📁 Folder Structure

![image](https://github.com/user-attachments/assets/16229fcd-3c67-4470-9777-6e584d002be9)


---

## ✅ Baseline Models for Initial Training and Evaluation

| No. | Algorithm                       | Purpose & Characteristics                                                                 |
|-----|---------------------------------|--------------------------------------------------------------------------------------------|
| 1   | Decision Tree Classifier        | Simple and interpretable but prone to overfitting on small data.                          |
| 2   | Random Forest Classifier        | Reduces variance with ensemble trees; generally better generalization than single trees.  |
| 3   | Naive Bayes (Gaussian/Bernoulli)| Fast and suitable for small datasets with conditional independence assumptions.           |
| 4   | Logistic Regression             | Interpretable and strong linear baseline.                                                  |
| 5   | Ridge Classifier CV             | Regularized model with internal CV; controls overfitting.                                 |
| 6   | K-Nearest Neighbors (KNN)       | Instance-based learner; sensitive to scaling.                                              |

---

## 🔍 Extended Models for Future Comparison and Tuning

| No. | Algorithm                       | Purpose & Characteristics                                                                 |
|-----|---------------------------------|--------------------------------------------------------------------------------------------|
| 7   | Support Vector Classifier (SVC) | Robust for high-dimensional problems; kernel choice is crucial.                           |
| 8   | Gradient Boosting Classifier    | Sequential boosting; balances bias and variance well.                                     |
| 9   | XGBoost                         | Efficient and regularized boosting; robust on tabular data.                               |
| 10  | LightGBM                        | Fast training with leaf-wise tree growth.                                                  |
| 11  | CatBoost                        | Handles categorical features natively; top performer.                                     |
| 12  | Linear Discriminant Analysis    | Linear boundaries with class-conditional distributions.                                   |
| 13  | Quadratic Discriminant Analysis | Flexible boundaries via class-specific covariances.                                       |

---

## 🧪 Model Evaluation Metrics

| Metric              | Description                                               |
|---------------------|-----------------------------------------------------------|
| **Train Accuracy**   | Accuracy on training data                                 |
| **Test Accuracy**    | Accuracy on unseen test data                              |
| **Accuracy Gap**     | Absolute difference between train and test accuracy       |
| **Generalization Score** | `Test Accuracy - Accuracy Gap` to penalize overfitting |

---

## 🔐 Overfitting Protection & Generalization

To ensure robustness:

- Models were evaluated **not just on test accuracy**, but also on how well they generalize.
- A **custom generalization score** penalized models with high training accuracy but poor test performance.
- Models were **labeled** as:
  - `Well-Generalized`
  - `Needs Review`
  - `Underfitted`

Top 2 models:

1. CatBoost Classifier       -> Gen Score: 0.7858
2. LightGBM Classifier       -> Gen Score: 0.7375

i have used few other model as well just to say "how we can use "

## Explainable AI (XAI) for Model Transparency

Understanding **why** the model made a prediction is as important as the prediction itself—especially in sensitive domains like loan approval.

To enhance interpretability, we used the following tools in the [`XAI.ipynb`](XAI.ipynb) notebook:

### ✅ Tools Used

- **LIME (Local Interpretable Model-agnostic Explanations)**  
  LIME generates local, human-understandable explanations for individual predictions. It's especially useful to explain specific cases and visualize which features influenced the decision.
  ![image](https://github.com/user-attachments/assets/e330f1b0-dc95-4331-be7c-dc1f23193e91)


- **SHAP (SHapley Additive exPlanations)**  
  SHAP provides global and local explanations based on game theory, attributing importance scores to each feature. It gives both summary plots and per-instance breakdowns.

### 🎯 Use Cases Covered

- Interpretation of CatBoost predictions on test samples
- Feature contribution visualizations (SHAP summary and force plots)
- Visual explanation exported as HTML (`lime_explanation.html`)
- Side-by-side comparison for multiple samples

These tools help provide **transparency, fairness, and auditability** of predictions in real-world deployment scenarios.


### Setup Instructions
    Clone the repo
    Install dependencies:
        pip install -r requirements.txt
    Run loan_prediction.ipynb to view model comparison and results
    Run testmodel.ipynb to test model and results
    Run XAI.ipynb to interpret predictions
