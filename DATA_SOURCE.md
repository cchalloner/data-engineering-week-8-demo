# Data source and field roles

`data/week8_service_requests.csv` was created for classroom practice. It contains fictional service requests and does not describe real people or organizations. It contains 180 independent completed IT service requests and no actual people or organizations. Relationships and missingness are simulated. No dataset download or external account is required.

| Field | Meaning and role |
|---|---|
| request_id | Unique tracking identifier. Exclude from features. |
| device_count | Devices involved, known at submission. Numerical feature, some missing. |
| complexity_score | Intake estimate on a 1–5 scale. Treat as numerical as specified in this exercise. |
| request_channel | portal, phone, or email. Nominal feature, some missing. |
| system_type | desktop, network, or software. Nominal feature. |
| actual_work_minutes | Measured technician work time after completion. Continuous target, three missing values. |
| resolution_steps | Steps recorded after completion. Exclude because unavailable at prediction time. |

Rules: remove rows with missing targets only. Median-impute numerical features, then apply StandardScaler. Most-frequent-impute nominal features, then use OneHotEncoder(handle_unknown="ignore", sparse_output=False). Keep the target in its original minutes. Split 75% training/25% test with random_state=8 before fitting any preprocessing. Use LinearRegression() and a DummyRegressor(strategy="median") baseline trained on y_train. Evaluate both on the same test rows.

Success means test MAE <= 12 minutes and strictly lower than baseline MAE. The fictional limit supports practicing a judgment against a stated need.
