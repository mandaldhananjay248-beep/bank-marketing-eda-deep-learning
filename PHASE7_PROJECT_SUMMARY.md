# Bank Marketing EDA and Subscription Prediction — Phase 7 Summary

## Project overview
This student project explores the UCI Bank Marketing dataset, performs EDA and preprocessing, compares baseline models, tunes a Random Forest, and discusses cautious business implications. The target records whether a client subscribed to a term deposit.

## Verified data
- Dataset: data/bank/bank-full.csv (semicolon-delimited).
- Shape: 45,211 rows x 17 columns; 16 input features and target y.
- Target: yes = 5,289 (11.70%); no = 39,922 (88.30%).
- Earlier checks found no conventional missing values or exact duplicates; unknown category values were retained.
- pdays = -1 means the customer had not previously been contacted.

## Modeling workflow
- Phase 4 used stratified 70/15/15 train/validation/test splits and 15 primary features; duration was excluded because it is known only after a call.
- Categorical features were one-hot encoded, numerical features scaled, and preprocessing was fitted on training data only.
- Phase 5 compared Dummy, Logistic Regression, Decision Tree, and Random Forest baselines. Phase 6 tuning did not improve validation Average Precision, so the Phase 5 Random Forest was retained.
- Selected threshold: 0.62, chosen on validation. Phase 6 reused the already-observed Phase 5 test holdout; it is not independent.

## Phase 7 findings
- Top aggregated native importance features: month, poutcome, contact.
- Top validation permutation importance features: month, poutcome, contact.
- The methods measure different properties; neither proves causation or effect direction.
- Category rates include denominators; validation threshold analysis uses validation data only.
- Three held-out inference examples use feature rows only; their labels are not shown or used.

## Limitations and responsible use
Results are observational, historical, campaign-specific, and subject to target imbalance and distribution shift. Probabilities may be miscalibrated, and the selected threshold does not encode real campaign costs. The reused test holdout is not independent. Duration is excluded to prevent post-contact leakage. Some demographic and financial fields can be sensitive or proxy variables. This is an educational experiment, not a production decision system.

## Generated deliverables
- Category rates: results/phase7/category_subscription_rates.csv
- Importance comparison: results/phase7/aggregated_feature_importance_comparison.csv
- Validation threshold trade-offs: results/phase7/validation_threshold_tradeoffs.csv
- Feature-only prediction examples: results/phase7/three_feature_only_prediction_examples.csv
- Seven-phase summary: results/phase7/seven_phase_project_summary.csv
- Figures: results/phase7/figures/

## Computed category and model findings
The following observed rates are calculated from the loaded dataset:
- job = student: 269/938 subscribed (28.68%).
- job = retired: 516/2,264 subscribed (22.79%).
- housing = no: 3,354/20,081 subscribed (16.70%).
- housing = yes: 1,935/25,130 subscribed (7.70%).
- loan = no: 4,805/37,967 subscribed (12.66%).
- loan = yes: 484/7,244 subscribed (6.68%).
- poutcome = success: 978/1,511 subscribed (64.73%).
- On validation, threshold 0.50 flagged 1,343 records positive (precision 36.71%, recall 62.09%).
- On validation, selected threshold 0.62 flagged 818 records positive (precision 48.29%, recall 49.75%).
- Phase 6 selected-model result on the reused test holdout at threshold 0.62: precision 47.50%, recall 49.18%, F1 0.4833, Average Precision 0.4544.
- The high poutcome=success rate represents prior campaign history and a limited subgroup; it should not be interpreted as a causal lift.

## Practical follow-up
1. Run randomized, consent-aware pilots to test messaging and timing; compare incremental outcomes rather than raw historical rates.
2. Use category rates as hypotheses only, retaining counts and uncertainty checks for small groups.
3. Protect customers with frequency caps and opt-out handling; do not infer that repeated contact is beneficial from sparse groups.
4. Do not use demographic or financial inputs for eligibility, denial, pricing, or other consequential decisions without legal and fairness review.
5. Before operational use, evaluate calibration, fairness, distribution shift, external validity, privacy, and campaign economics.

## Final Submission Audit — Phase 8

### Overall verdict
READY TO SUBMIT

### What was verified
- The real dataset file at `data/bank/bank-full.csv` was checked and contains 45,211 rows and 17 columns, with target `y` and 16 input features.
- The notebook at `notebooks/bank_marketing_eda.ipynb` was executed from beginning to end in the existing project environment.
- The preprocessing pipeline was inspected and reused correctly for the MLP, with the same stratified train/validation/test split and no leakage from `duration`.
- The Phase 8 MLP model and learning curves were verified using the saved outputs in `results/phase8/` and `results/figures/phase8/`.
- The Random Forest benchmark and the MLP were compared on the same validation data with consistent metrics; the Random Forest remains slightly stronger on validation average precision, which is reported honestly.
- A short literature review and reference list were appended to the notebook to satisfy the assignment requirement for academic references.

### Audit status by requirement
- Requirement 1 (real-world dataset): PASS
- Requirement 2 (EDA and preprocessing): PASS
- Requirement 3 (visualizations and seven-stage coverage): PASS
- Requirement 4 (deep learning): PASS
- Requirement 5 (evaluation plots and metrics): PASS
- Requirement 6 (conclusion/future scope): PASS
- Requirement 7 (literature review): FIXED and now present

### Remaining limitations
- No formal project-level `requirements.txt` file is committed; the notebook was validated in the existing `.venv` environment.
- The project remains an academic historical-analysis exercise and does not claim deployment readiness or causal business effect.
- The dataset cannot establish campaign profitability or fairness without more experimental or external data.
