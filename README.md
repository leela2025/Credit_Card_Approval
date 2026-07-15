# Credit Card Approval Prediction

A machine learning–powered web application that predicts whether a credit
card application is likely to be **approved** or **declined**, based on
applicant demographics, income, employment, and household details.

Built with **Flask**, **XGBoost**, and **SQLite**, this project automates
the kind of screening banks perform manually — instantly, and at scale.

---

## ✨ Features

- **Home page** — project overview and entry point
- **User accounts** — sign up / log in with securely hashed passwords (SQLite + Werkzeug)
- **Application form** — 17 input fields covering demographics, income,
  employment, household, and contact information
- **Real-time prediction** — powered by a trained XGBoost classifier
- **Result page** — approval/decline verdict with an animated confidence
  gauge and a full summary of the submitted application

---

## 🧱 Tech Stack

| Layer          | Technology                          |
|----------------|--------------------------------------|
| Backend        | Python, Flask                       |
| ML Model       | XGBoost (Gradient Boosting)         |
| Other models compared during training | Logistic Regression, Decision Tree, Random Forest |
| Data handling  | Pandas, NumPy                       |
| Visualization (training/EDA) | Matplotlib, Seaborn         |
| Database       | SQLite (user accounts)              |
| Frontend       | HTML, CSS, vanilla JavaScript       |
| Auth           | Flask sessions + Werkzeug password hashing |

---

## 📁 Project Structure

```
credit-card-approval-prediction/
├── app.py                  # Flask backend: routes, auth, prediction logic
├── model.pkl               # Trained XGBoost classifier
├── requirements.txt        # Python dependencies
├── users.db                # SQLite database (auto-created on first run)
├── templates/
│   ├── home.html           # Landing page
│   ├── signup.html         # Account creation
│   ├── login.html          # Login
│   ├── apply.html          # Application form
│   └── result.html         # Prediction result page
└── README.md
```

---

## 🚀 Getting Started (Local Setup)

### 1. Clone the repository
```bash
git clone https://github.com/YOUR_USERNAME/credit-card-approval-prediction.git
cd credit-card-approval-prediction
```

### 2. Create a virtual environment (recommended)
```bash
python -m venv venv
venv\Scripts\activate        # Windows
source venv/bin/activate     # macOS/Linux
```

### 3. Install dependencies
```bash
pip install -r requirements.txt
```

### 4. Run the app
```bash
python app.py
```

Visit **http://127.0.0.1:5000** in your browser.

### 5. Log in
- **Demo account:** `admin` / `admin123`
- Or click **Sign Up** to create your own account.

---

## 🔄 Application Flow

```
Home (/) 
  └─▶ Sign Up (/signup) or Log In (/login)
        └─▶ Application Form (/apply)
              └─▶ POST /predict  (JSON, calls the ML model)
                    └─▶ Result Page (/result)
```

---

## 🧠 Model Details

The model is a trained **XGBoost Classifier** expecting exactly these 17
features, in this order:

```
CODE_GENDER, FLAG_OWN_CAR, FLAG_OWN_REALTY, CNT_CHILDREN, AMT_INCOME_TOTAL,
NAME_INCOME_TYPE, NAME_EDUCATION_TYPE, NAME_FAMILY_STATUS, NAME_HOUSING_TYPE,
DAYS_BIRTH, DAYS_EMPLOYED, FLAG_MOBIL, FLAG_WORK_PHONE, FLAG_PHONE, FLAG_EMAIL,
OCCUPATION_TYPE, CNT_FAM_MEMBERS
```

Categorical fields (income type, education, marital status, housing type,
occupation) are encoded using the standard scikit-learn `LabelEncoder`
convention — each column's unique values sorted alphabetically and numbered
`0..n-1`. **If your training notebook used a different encoding order,
update the option lists in `app.py` to match** — this is the one thing
that can silently affect prediction accuracy without throwing an error.

`DAYS_BIRTH` and `DAYS_EMPLOYED` are computed server-side from the
applicant's date of birth and employment status (a large placeholder value,
`365243`, is used for unemployed/retired applicants, matching the original
dataset's convention).

---

## 📊 Model Training (summary)

Four classification algorithms were trained and compared on the dataset:

- Logistic Regression
- Decision Tree Classifier
- Random Forest Classifier
- **XGBoost Classifier** ← best performer, used in production

Models were evaluated using accuracy score, confusion matrix, and
classification report. Data preprocessing included handling missing
values, removing duplicates, encoding categorical variables, and
converting multi-class payment status codes into binary approval labels.

*(See the training notebook for full EDA, preprocessing, and model
comparison details.)*

---

## 👥 Team

- Manyam Jagadeeswari — Team Lead
- Akash Medara
- Leela Venkata Parameswari Lankoji
- Kakumanu Yohan

---

## 📄 License

This project was built for educational purposes as part of a guided
machine learning program.
