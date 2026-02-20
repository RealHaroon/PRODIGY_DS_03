

# 📊 Task 3 – Bank Marketing Decision Tree Classifier

---

# 1️⃣ Data Understanding

* The dataset contains **4,521 rows and 17 columns**.
* **Numerical Columns:**
  `age`, `balance`, `day`, `duration`, `campaign`, `pdays`, `previous`
* **Categorical Columns:**
  `job`, `marital`, `education`, `default`, `housing`, `loan`, `contact`, `month`, `poutcome`, `y`
* Target Variable:
  `y` (Whether the customer subscribed to a term deposit)

---

# 2️⃣ Data Cleaning

* No missing values were found.
* No duplicate rows were detected.
* The category `"unknown"` was present in `job`, `education`, and `contact`.
  It was retained as a valid category instead of removing rows.
* Outliers were observed in `balance` and `age`, but they were retained since they may represent real high-value customers.
* Dropped weak / potentially data-leakage features:

  * `day`
  * `duration` (removed because it directly relates to call outcome and can cause data leakage)

---

# 3️⃣ Exploratory Data Analysis (EDA)

### 📌 Target Variable Distribution

* 88% customers did **not subscribe**
* 12% customers **subscribed**
* The dataset is highly imbalanced.

---

### 📌 Age Distribution

* Most customers are between **20–60 years old**.
* Highest customer concentration is between **30–50 years**.

---

### 📌 Job Category

* Most common job categories:

  * Blue-collar
  * Management
  * Technician
* These categories also show higher subscription counts due to higher population size.

---

### 📌 Marital Status

* 62% Married
* 26% Single
* 12% Divorced

---

### 📌 Education

* Majority of customers have **secondary education**.
* Secondary education group dominates both subscription and non-subscription categories.

---

### 📌 Balance vs Subscription

* Customers who subscribed tend to have a **slightly higher median balance**.
* Non-subscribers contain the most extreme high-balance outliers.

---

### 📌 Housing Loan

* Customers **without housing loans** are more likely to subscribe.

---

### 📌 Personal Loan

* Majority of successful subscriptions come from customers **without personal loans**.

---

### 📌 Previous Campaign Outcome (`poutcome`)

* `"unknown"` dominates the dataset.
* Indicates many customers were not contacted previously.

---

### 📌 Campaign Contacts

* Most customers were contacted **1–3 times**.
* Higher campaign numbers do not necessarily increase subscription rate.

---

# 4️⃣ Data Preprocessing

* Mapped target variable:

  * `yes → 1`
  * `no → 0`
* Converted binary categorical columns (`default`, `housing`, `loan`) to numeric.
* Applied **One-Hot Encoding** to multi-class categorical columns:

  * `job`
  * `marital`
  * `education`
  * `contact`
  * `month`
  * `poutcome`
* Separated:

  * Features → `X`
  * Target → `y`
* Split dataset into training and testing sets.

---

# 5️⃣ Model Training

A **Decision Tree Classifier** was used to predict whether a customer would subscribe.

Initial model showed:

* High overall accuracy
* Very low recall for minority class (subscribers)

Because the dataset is imbalanced (88% No, 12% Yes), the model initially favored the majority class.

To address this:

* Applied `class_weight='balanced'`
* Tuned hyperparameters:

  * `max_depth`
  * `min_samples_split`
  * `min_samples_leaf`

---

# 6️⃣ Model Evaluation (Final Tuned Model)

### 📊 Final Results:

* Accuracy: **82%**
* Precision (Class 1): **0.30**
* Recall (Class 1): **0.38**
* F1-score (Class 1): **0.33**

### 📌 Key Insight:

Although overall accuracy decreased slightly from 87% to 82%, the recall for actual subscribers improved significantly (from 14% to 38%).

This demonstrates an important machine learning trade-off:

> Optimizing for minority class detection often reduces overall accuracy but improves business value.

---

# 7️⃣ Hyperparameter Tuning

Performed tuning using:

* Increased tree depth
* Adjusted minimum samples per leaf
* Applied class weighting to handle imbalance

This improved minority class detection performance while maintaining reasonable overall accuracy.

---

# 🎯 Final Conclusion

* The dataset is highly imbalanced.
* Decision Tree model provides moderate performance.
* Applying class balancing significantly improves subscriber detection.
* Accuracy alone is not a reliable metric for imbalanced classification problems.
* Recall and F1-score are more meaningful evaluation metrics in this case.

---

