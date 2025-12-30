# Cinema Audience Forecaster (Term 3 – 2025)

Forecast daily cinema audience counts for a future period using historical theater attendance and metadata.

## 🏆 Result

- **Public Leaderboard Score:** $R^2 = 0.31003$
- **Approach:** XGBoost + LightGBM ensemble, adversarial validation to remove unstable time-leak features, and baseline blending.

## 📂 Dataset (Competition Files)

All data comes from the Kaggle “Cinema Audience Forecasting Challenge” dataset provided by IIT Madras.
Here is the description of the dataset used.

### Files used:
- **`booknow_visits.csv`**: Core training table with `book_theater_id`, `show_date`, `audience_count` (target).
- **`booknow_booking.csv`**: BookNow booking transactions (`tickets_booked`, `booking_datetime`, etc.).
- **`booknow_theaters.csv`**: BookNow theater metadata (type, area, latitude/longitude).
- **`cinePOS_booking.csv`**: CinePOS ticket sales transactions (`tickets_sold`, times).
- **`cinePOS_theaters.csv`**: CinePOS theater metadata.
- **`movie_theater_id_relation.csv`**: Mapping between BookNow and CinePOS theater IDs.
- **`date_info.csv`**: Calendar helper table (`show_date`, `day_of_week`).
- **`sample_submission.csv`**: Submission format template.

## ⚙️ Method (High Level)

1. **EDA**: Analysis of time coverage, weekend vs. weekday patterns, and data sparsity.
2. **Feature Engineering**:
   - Theater historical aggregates (avg/median/std audience).
   - Temporal features (day-of-week, weekend).
   - Booking/POS features (handled as 0 for test set where unavailable).
3. **Modeling**:
   - XGBoost (Tweedie objective) + LightGBM (Poisson Objective).
   - Weighted ensemble.
4. **Generalization Fix**:
   - **Adversarial Validation**: Used to detect drift/leaky time features (e.g., year-like signals) and remove unstable columns.
5. **Final Boost**:
   - Blended model predictions with a simple theater-average baseline.

## 📁 Repository Contents

- `Cinema_Audience_Forecasting.ipynb`: Final notebook containing the entire pipeline.
- `sample_submission.csv`: Submission template.
- `requirements.txt`: Minimal dependencies to run locally.
- `LICENSE`: MIT License.

## 🚀 How to Run Locally

1. **Install dependencies:**
   ```
   pip install -r requirements.txt
   ```
2. **Launch the notebook:**
   ```
   jupyter notebook
   ```

3. **Open `Cinema_Audience_Forecasting.ipynb` and run all cells.**

## 📄 License

This project is licensed under the `MIT License`.
