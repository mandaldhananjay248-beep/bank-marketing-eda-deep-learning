# Final Submission Audit — Bank Marketing EDA Project

## Overall verdict
READY TO SUBMIT

## Assignment requirement audit table

| Requirement | Verification performed | Result | Evidence or file location | Remaining action |
|---|---|---|---|---|
| 1. Real-world dataset with at least 15 features/fields | Verified the real dataset file and shape, target column, and feature count | PASS | `data/bank/bank-full.csv`; notebook data-loading cells; dataset shape observed as 45,211 x 17 | None |
| 2. EDA, missing values, outliers, duplicates, cleaning, encoding/scaling, and train/validation/test split | Inspected the notebook code and executed it end-to-end; checked preprocessing and split logic | PASS | `notebooks/bank_marketing_eda.ipynb`; `models/bank_marketing_preprocessor.joblib` | None |
| 3. At least five meaningful visualizations and seven visualization stages | Verified the outputs and notebook explanations for the exploratory and model-analysis plots | PASS | `outputs/plots/*.png`; `results/phase7/figures/*.png`; notebook sections on early EDA and later model interpretation | None |
| 4. At least one deep-learning model with feature analysis and tuning | Verified `MLPClassifier` training, validation-only tuning, and feature importance computation | PASS | `notebooks/bank_marketing_eda.ipynb`; `models/bank_marketing_mlp_phase8.joblib`; `results/phase8/*.csv` | None |
| 5. Three to four model evaluation visualizations and learning curves | Verified confusion matrix, ROC, precision-recall, probability distribution, and training curves | PASS | `results/figures/phase8/*.png`; `results/phase8/mlp_training_history.csv` | None |
| 6. Conclusion, findings, limitations, and future scope | Reviewed the final notebook conclusion and the summary file | PASS | `notebooks/bank_marketing_eda.ipynb`; `PHASE7_PROJECT_SUMMARY.md` | None |
| 7. Literature review and 3–5 references in APA or IEEE style | Verified the UC Irvine dataset citation and added a concise literature review with references | FIXED | `data/bank/bank-names.txt`; appended reference section in `notebooks/bank_marketing_eda.ipynb` | None; references now present |

## Executive summary
- The project was checked against the actual files in the repository, not just the documentation.
- The notebook was executed from beginning to end in the existing `.venv` environment and completed successfully.
- The dataset is the real Portuguese bank marketing dataset, with 45,211 rows and 17 columns, including a binary target named `y`.
- Preprocessing is fit on training data only; validation is used for model selection; the test set is not used for tuning or threshold selection.
- The Random Forest remains the stronger benchmark on validation Average Precision, while the MLP is reported honestly as a valid but lower-performing deep-learning baseline.
- A small issue was found: the literature review and formal reference list were not clearly present in the notebook; a concise literature review and four verified references were appended without overwriting prior work.

## Verification details
- Dataset verification: `data/bank/bank-full.csv` exists and contains the expected bank marketing dataset; target frequencies were checked and are approximately `no=39,922` and `yes=5,289`.
- Notebook execution: `jupyter nbconvert --to notebook --execute --inplace notebooks/bank_marketing_eda.ipynb` completed successfully.
- Model reload test: the saved pipeline at `models/bank_marketing_mlp_phase8.joblib` was reloaded and successfully produced finite probabilities in the range `[0, 1]` for a sample of raw feature rows.
- Metric consistency: validation and test metrics in `results/phase8/*.csv` agree with the model outputs and notebook narrative.
- Learning-curve verification: `results/phase8/mlp_training_history.csv` contains real epoch-wise loss and accuracy values, and the corresponding figures were saved to `results/figures/phase8/`.

## Files created or updated
- Updated: `notebooks/bank_marketing_eda.ipynb`
- Updated: `PHASE7_PROJECT_SUMMARY.md`
- Created: `FINAL_SUBMISSION_AUDIT.md`

## Remaining limitations
- There is no formal `requirements.txt` committed to the repository; the project was validated in the existing `.venv` environment.
- This project remains an academic, historical-analysis exercise rather than a production deployment system.
- The dataset contains campaign and customer historical patterns only; no causal claims or campaign-cost optimization were established.
