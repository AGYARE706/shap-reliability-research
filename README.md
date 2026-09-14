\# SHAP Explanation Stability Research

\### Class-Level SHAP Stability in Diabetes and CKD Prediction — A Multi-Dimensional Framework



\*\*Researcher:\*\* Frank Adu Agyare  

\*\*Institution:\*\* Kwame Nkrumah University of Science and Technology (KNUST), Ghana  

\*\*Supervisor:\*\* Prof. Luke E.K. Achenie, Virginia Tech  

\*\*Status:\*\* Active — Phase 4 complete, Phase 5 in progress  



\---



\## What This Project Is About



Machine learning models are increasingly being used in healthcare to detect diseases like diabetes and chronic kidney disease (CKD). To make these models trustworthy for clinical use, researchers apply explainability tools — most commonly SHAP (SHapley Additive exPlanations) — to explain why a model made a specific prediction.



But here is the problem: almost nobody asks whether those explanations are actually stable. If you retrained the same model with a slightly different random seed, or used a different model architecture, or trained on a slightly different sample of patients — would SHAP still point to the same features as most important?



This project tests exactly that. And it goes one step further: it tests whether SHAP explanations are equally stable for diabetic and CKD patients (the minority class) as they are for healthy patients (the majority class). The minority class patients are exactly the ones who most need reliable explanations — but they are also the ones the model is least confident about due to class imbalance.



The core research question is:



> \*"Are SHAP explanation stability levels different between the minority class (sick patients) and the majority class (healthy patients) in tabular medical prediction models — and does this difference hold across random seeds, model architectures, and bootstrap resamples?"\*



\---



\## Why This Is Novel



A thorough literature search confirmed that:



\- Every existing SHAP stability study measures consistency at the \*\*dataset level\*\* — averaging across all patients simultaneously

\- Nobody has \*\*disaggregated SHAP stability by predicted class\*\* to ask whether sick and healthy patients get equally reliable explanations

\- A 2024 CKD paper noticed that SHAP analysis was dominated by the majority class and explicitly flagged it as "warranting further work" — this project is that further work

\- A 2026 cardiovascular study tested cross-model SHAP stability but only at the dataset level with no class breakdown



This project also proposes a \*\*class-disaggregated SHAP Stability Index (SSI)\*\* — a composite metric combining all three stability dimensions into one score, computed separately for each class — as a new standardised reporting metric for medical ML papers.



\---



\## Datasets



| Dataset | Patients | Features | Target | Source |

|---|---|---|---|---|

| Pima Indians Diabetes | 768 | 8 | Diabetic / Not diabetic | UCI / Kaggle |

| UCI Chronic Kidney Disease | 400 | 24 | CKD / Not CKD | UCI / Kaggle |

| African data (pending) | TBD | TBD | TBD | Ghana STEPS 2023 / H3Africa |



\---



\## Project Structure

shap-reliability-research/

│

├── data/

│ ├── diabetes.csv ← original Pima dataset

│ ├── diabetes\_clean.csv ← cleaned version

│ ├── kidney\_disease.csv ← original UCI CKD dataset

│ └── ckd\_clean.csv ← cleaned version

│

├── notebooks/

│ ├── 01\_data\_exploration.ipynb ← Phase 2: data cleaning

│ ├── 02\_baseline\_models.ipynb ← Phase 3: model training

│ └── 03\_shap\_baseline.ipynb ← Phase 4: SHAP explainability

│

├── models/

│ ├── diabetes\_rf\_model.pkl ← trained Random Forest (diabetes)

│ ├── diabetes\_scaler.pkl ← StandardScaler (diabetes)

│ ├── ckd\_rf\_model.pkl ← trained Random Forest (CKD)

│ ├── ckd\_scaler.pkl ← StandardScaler (CKD)

│ ├── diabetes\_shap\_values\_baseline.npy ← baseline SHAP values (diabetes)

│ └── ckd\_shap\_values\_baseline.npy ← baseline SHAP values (CKD)

│

├── results/

│ ├── figures/

│ │ ├── shap\_baseline/ ← SHAP visualisation plots

│ │ │ ├── diabetes\_shap\_summary.png

│ │ │ ├── diabetes\_shap\_bar.png

│ │ │ ├── diabetes\_shap\_waterfall\_patient0.png

│ │ │ ├── diabetes\_shap\_dependence\_glucose.png

│ │ │ ├── ckd\_shap\_summary.png

│ │ │ └── ckd\_shap\_bar.png

│ │ ├── feature\_distributions.png

│ │ ├── diabetes\_model\_comparison.png

│ │ ├── diabetes\_confusion\_matrix.png

│ │ └── ckd\_model\_comparison.png

│ └── tables/

│ ├── diabetes\_model\_comparison.csv

│ ├── ckd\_model\_comparison.csv

│ ├── diabetes\_shap\_baseline\_rankings.csv

│ └── ckd\_shap\_baseline\_rankings.csv

│

└── README.md





\---



\## Progress



| Phase | Description | Status |

|---|---|---|

| Phase 1 | Literature review and environment setup | ✅ Complete |

| Phase 2 | Data acquisition and cleaning | ✅ Complete |

| Phase 3 | Baseline prediction models | ✅ Complete |

| Phase 4 | Baseline SHAP explainability | ✅ Complete |

| Phase 5 | Class-level SHAP stability experiments | 🔄 In progress |

| Phase 6 | Cross-population analysis (African data) | ⏳ Pending data approval |

| Phase 7 | Write-up and presentation | ⏳ Pending |



\---



\## Key Findings So Far



\*\*Phase 3 — Baseline Models:\*\*

\- Diabetes: Random Forest achieved F1 = 0.6337, ROC-AUC = 0.8200

\- CKD: Random Forest achieved F1 = 0.9655, ROC-AUC = 0.9993

\- Class imbalance noted in both datasets — recall was the weakest metric for both



\*\*Phase 4 — Baseline SHAP:\*\*

\- Diabetes top features: Glucose → BMI → Age → DiabetesPedigreeFunction

\- SHAP dependence plot revealed glucose SHAP values turn positive at \~100 mg/dL — matching the clinical prediabetes threshold

\- CKD top features: hemo → pcv → sg → sc → al (all direct kidney function markers)

\- dm (diabetes mellitus) ranked 7th in CKD model — confirming the diabetes-CKD clinical link

\- pcc and cad have zero SHAP values in the CKD model — contribute nothing to predictions



\---



\## Phase 5 Experiments (Coming)



Four stability experiments, each measuring SHAP consistency separately for the minority class (sick patients) and majority class (healthy patients):



1\. \*\*Cross-seed stability\*\* — same model, 30 different random seeds

2\. \*\*Cross-model stability\*\* — same data, 4 different model architectures

3\. \*\*Cross-bootstrap stability\*\* — same model, 30 different data resamples

4\. \*\*SHAP Stability Index (SSI)\*\* — composite score combining all three dimensions



\---



\## Tech Stack



| Tool | Version | Purpose |

|---|---|---|

| Python | 3.11.9 | Core language |

| pandas | 3.0.3 | Data manipulation |

| numpy | 2.4.6 | Numerical operations |

| scikit-learn | 1.9.0 | Model training and evaluation |

| xgboost | 3.2.0 | Gradient boosting classifier |

| shap | 0.51.0 | Explainability analysis |

| scipy | latest | Spearman rank correlation |

| matplotlib / seaborn | latest | Visualisation |

| jupyter | latest | Interactive notebooks |



\---



\## How To Run This Project



\*\*1. Clone the repository:\*\*

```bash

git clone https://github.com/YourUsername/shap-reliability-research.git

cd shap-reliability-research

```



\*\*2. Create and activate a virtual environment:\*\*

```bash

python -m venv venv

venv\\Scripts\\activate.bat        # Windows

source venv/bin/activate         # Mac/Linux

```



\*\*3. Install dependencies:\*\*

```bash

pip install pandas numpy scikit-learn xgboost shap matplotlib seaborn jupyter scipy

```



\*\*4. Run notebooks in order:\*\*

01\_data\_exploration.ipynb → Phase 2

02\_baseline\_models.ipynb → Phase 3

03\_shap\_baseline.ipynb → Phase 4





\---



\## Supervisor



\*\*Prof. Luke E.K. Achenie\*\*  

Professor, Department of Chemical Engineering  

Virginia Tech, Blacksburg, Virginia, USA  

Patron, KNUST AI/Data Science Club  



\---



\## Researcher



\*\*Frank Adu Agyare\*\*  

Level 200, BSc Computer Science  

Kwame Nkrumah University of Science and Technology (KNUST), Ghana  

Deputy Research and Projects Coordinator, KNUST AI/Data Science Club  



\---



\*This project is supervised research conducted under Prof. Achenie's guidance as part of the KNUST AI/Data Science Club's research programme.\*

