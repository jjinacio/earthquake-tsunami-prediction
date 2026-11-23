# Earthquake Tsunami Prediction

Can the location and size of a major earthquake predict whether it triggers a tsunami? This project trains three classifiers on 782 earthquakes and looks at which features matter most.

## Data
[Global Earthquake-Tsunami Risk Assessment Dataset](https://www.kaggle.com/datasets/ahmeduzaki/global-earthquake-tsunami-risk-assessment-dataset) (A. M. Zaki, Kaggle): 782 earthquakes of magnitude 6.5 and above, recorded 2001-2022. 304 triggered a tsunami and 478 did not (39% / 61%).

The CSV is not included. Download it from Kaggle and save it as `data/earthquake_data_tsunami.csv`.

## Method
- Four core features: magnitude, depth, latitude, longitude.
- Standardized the features, then trained Logistic Regression, Random Forest (800 trees, balanced class weights) and Gradient Boosting (300 trees, learning rate 0.05).
- Evaluated on a held-out test set of 157 earthquakes with accuracy, a confusion matrix, a classification report and ROC-AUC.

## Results
| Model | Test accuracy |
|---|---|
| Logistic Regression | 58.6% |
| Random Forest | 65.6% |
| **Gradient Boosting** | **70.1%** (ROC-AUC 0.769) |

- Always predicting "no tsunami" would be right 61% of the time on the test set (96 of 157), so accuracy alone flatters every model here. That is why the notebook also reports ROC-AUC and per-class precision and recall.
- In the Gradient Boosting model, longitude (0.60) and latitude (0.23) account for about 83% of the importance across the four features, which fits the fact that tsunamis follow plate boundaries.

## Limits
Only 782 earthquakes from 2001-2022, and a modest 70% accuracy. This is a class project to practice classification and model evaluation, not a hazard model.

## Run it
```bash
pip install -r requirements.txt
jupyter notebook earthquake_tsunami_prediction.ipynb
```
A short write-up is in [`docs/technical-report.pdf`](docs/technical-report.pdf), and a project portfolio is in [`docs/portfolio.pdf`](docs/portfolio.pdf).
