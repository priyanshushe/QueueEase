# QueueEase-Automated-Queue-Department-Management-using-AI-and-ML
A lightweight, Flask-based queue and token management system with MongoDB storage, staff & user workflows, slot-time prediction using machine learning, and optional OpenAI-powered conversation responses.

# ✨ Features
 User token creation with automatic department classification
 Staff login, dashboard view, and token lifecycle management
 Token status API (JSON)
 ML-powered time-slot prediction (LinearRegression)
 MongoDB-backed storage (smartqueue database)
 Helper scripts for adding/removing staff & creating department data
 Optional OpenAI integration for improved responses

# 📁 Repository Structure
Queue management system/
├─ app.py                   # Main Flask server
├─ predict_slot.py          # Slot prediction model (Linear Regression)
├─ create_staff.py          # CLI tool to add staff
├─ delete_staff.py          # CLI tool to delete staff
├─ setup_department.py       # Department initialization helper
├─ requirements.txt         # Python dependencies
├─ templates/               # (If included) Flask HTML templates
└─ static/                  # (If included) CSS/JS files

# 🧰 Tech Stack
Backend: Python, Flask, Flask-Login
Database: MongoDB (via PyMongo)
Machine Learning: scikit-learn, pandas
Optional AI: OpenAI Python Client

# 🚀 Installation
1. Clone the repo
git clone <your-repo-url>
cd "QueueEase"

2. Create & activate a virtual environment
python -m venv venv
source venv/bin/activate        # macOS/Linux
venv\Scripts\activate           # Windows

3. Install dependencies
pip install -r requirements.txt

4. Start MongoDB

Ensure MongoDB is running on:

mongodb://localhost:27017/

# ⚙️ Configuration

Database name: smartqueue

Secret key: Update app.secret_key before production.

OpenAI (optional): set OPENAI_API_KEY environment variable.

# ▶ Running the Application
  1. (Optional) Add staff accounts
  python create_staff.py

  2. Start the Flask server
  python app.py

  3. Access the app
  http://127.0.0.1:5000/

# 🔌 API Endpoints
User & Token
Method	Endpoint	Description
POST	/user	Create token
GET	/api/token_status/<token_number>	Get token status
Staff
Method	Endpoint	Description
POST	/staff_login	Staff login
GET	/staff_logout	Logout staff
GET	/staff	Staff dashboard
POST	/done/<token>	Mark token done
POST	/cancel/<token>	Cancel token
Prediction & Feedback
Method	Endpoint	Description
GET	/api/suggest_slot	Predict optimal time slot
POST	/feedback	Submit user feedback
# 📊 Time-Slot Prediction Logic

The function predict_best_slot():

Loads previous tokens with recorded slot_time

Converts slot times into numeric minutes

Trains a LinearRegression model

Predicts the next likely slot for the following token

Falls back to 11:00 AM if data is insufficient

Enforces business hours (09:00–17:00)

This allows dynamic queue balancing based on historical load.

# 🗄 MongoDB Collections
tokens
Stores user tokens:
token_number
issue_text
slot_time
status (Active/Done/Cancelled/Expired)
staff
Stores staff login credentials:
username
password (⚠ currently plaintext — improve before production)
departments
Used for issue classification:
name
keywords
# 🔐 Security Notes

Before deploying:

Replace plaintext passwords with hashed passwords

Move secret_key to environment variables

Disable debug=True

Add rate limiting for API routes

# 🛠 Future Improvements

JWT or session-based authentication for users

Docker support

Staff analytics dashboard

Time-series models for improved predictions

Background training jobs
