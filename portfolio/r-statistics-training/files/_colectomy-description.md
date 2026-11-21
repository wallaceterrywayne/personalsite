# Surgical approach and recovery after colectomy

A surgical department randomized 200 adults scheduled for elective
colectomy to either open surgery or laparoscopic surgery, 100 patients per
approach. Before surgery, staff recorded each patient's age, body mass
index, and whether they had diabetes. The hospital's records system also
captured how many days each patient stayed in hospital after the
operation.

Thirty days after surgery, patients completed the QoR-15, a
quality-of-recovery questionnaire scored from 0 to 150, with higher scores
meaning better recovery.

The department wants to know whether surgical approach affects quality of
recovery at 30 days.

## Variables

| Variable | Description | When measured |
|---|---|---|
| `patient_id` | Patient identifier |  |
| `approach` | Surgical approach (Open, Laparoscopic) | Randomization |
| `age` | Age in years | Before surgery |
| `bmi` | Body mass index (kg/m²) | Before surgery |
| `diabetes` | Diabetes diagnosis (No, Yes) | Before surgery |
| `length_of_stay` | Days in hospital after surgery | At discharge |
| `qor15_30d` | QoR-15 score, 0 to 150 | 30 days after surgery |

The data are in `colectomy-data.csv`.
