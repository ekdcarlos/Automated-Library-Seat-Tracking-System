 DeKUT Automated Library Seat Tracking System
Overview
DeKUT Automated Library Seat Tracking System is a web-based application designed to help students find available study spaces in real-time. The system displays live seat availability across different library sections, tracks occupancy changes automatically, and provides historical data for analysis. It's built with a focus on simplicity, accessibility, and zero-cost deployment.

The project was developed as a fourth-year IT project for Dedan Kimathi University of Technology (DeKUT).

 Features
Feature	Description
Live Dashboard	Displays real-time seat availability across Main Floor, Upper Floor, Computer Lab, and Study Rooms with color-coded status indicators (Green = Available, Yellow = Almost Full, Red = Full)
Seat Layout View	Visual map showing individual seats (taken = grey, available = white) for each section, helping students find specific spots
Sensor Simulation	Python script generates random ENTRY and EXIT events to simulate student traffic, demonstrating automation without physical hardware
Admin Panel	Staff can manually update seat counts as a fallback option, with password protection
Historical Logging	Every seat count change is recorded with timestamps and event types (ENTRY/EXIT/manual)
Daily Usage Charts	Visual trend analysis showing occupancy patterns over the past 7 days
E-Resources Access	Direct links to e-books and online resources for remote students
Auto-Refresh	Dashboard updates every 2 seconds without page reload
Mobile Responsive	Works on phones, tablets, and desktops
 Technology Stack
Layer	Technology
Backend	Python 3.10+ with Flask
Database	SQLite (via Flask-SQLAlchemy)
Frontend	HTML, CSS, JavaScript
Charts	Chart.js
HTTP Client	Requests library (for simulation)
Project Structure
DeKUT_Library_Tracker/
│
├── app.py                  # Flask application
├── sensors.py              # Sensor simulation script
├── requirements.txt        # Python dependencies
│
├── templates/
│   ├── dashboard.html      # Main student dashboard
│   ├── seat.html           # Seat layout view
│   └── admin.html          # Admin panel
│
├── static/
│   ├── style.css           # Stylesheet
│   └── script.js           # JavaScript
│
└── instance/
    └── resource.db         # SQLite database (auto-created)
 Database Schema
The system uses three tables:

Table	Purpose	Key Fields
Resource	Current seat counts	id, name, available, total, last_updated
ResourceHistory	Change log	id, resource_id, old_count, new_count, event_type, changed_at
EBook	E-resource list	id, title, author, category, link, is_open_access
 Installation
1. Clone or download the project
text
git clone <repository-url>
cd DeKUT_Library_Tracker
2. Create and activate a virtual environment
Windows:

text
python -m venv venv
venv\Scripts\activate
Mac/Linux:

text
python3 -m venv venv
source venv/bin/activate
3. Install dependencies
text
pip install -r requirements.txt
4. Run the application
text
python app.py
5. (Optional) Run the sensor simulation in a separate terminal
text
python sensors.py
6. Open your browser
Navigate to http://127.0.0.1:5000

 Configuration
Admin Panel Access
Go to /admin?password=admin123 to access the admin panel.

Default password: admin123

Sample Data
The database is seeded with:

Main Floor: 45/60 available

Upper Floor: 8/30 available

Computer Lab: 0/30 available

Study Rooms: 12/20 available

E-Resources Sample Data
Three sample e-books are pre-loaded for demonstration.

How It Works
Student opens the dashboard → Sees live seat counts for all sections

Sensor simulation runs → Sends random ENTRY/EXIT events to the backend

Flask processes events → Updates seat counts, logs history

Dashboard auto-refreshes → Students see updated counts every 2 seconds

Admin can override → Manual updates via admin panel if needed

 System Architecture Diagram

┌─────────────────────────────────────────────────────────────────────┐
│                    DeKUT AUTOMATED LIBRARY SEAT TRACKING            │
└─────────────────────────────────────────────────────────────────────┘

   ┌──────────────┐
   │   STUDENT    │
   │  (On Phone)  │
   └──────┬───────┘
          │
          ▼
   ┌──────────────────────────────────────┐
   │       STUDENT DASHBOARD             │
   │   - Live seat counts                │
   │   - Color-coded status              │
   │   - E-book list                     │
   │   - Peak hour predictions           │
   └─────────────────┬────────────────────┘
                     │
                     ▼
   ┌──────────────────────────────────────┐
   │        FLASK BACKEND                │
   │   - Handles requests                │
   │   - Processes sensor events         │
   │   - Runs ML predictions             │
   └─────────────────┬────────────────────┘
                     │
       ┌─────────────┴─────────────┐
       │                           │
       ▼                           ▼
   ┌──────────────┐        ┌────────────────┐
   │   DATABASE   │        │   SIMULATION   │
   │   (SQLite)   │        │     SCRIPT     │
   │              │        │                │
   │ - Resource   │        │ Generates      │
   │ - History    │        │ ENTRY/EXIT     │
   │ - EBooks     │        │ events         │
   └──────────────┘        └────────────────┘
 License
This project is open-source and free to use for educational purposes.

 Author
Emmanuel Kalongo Dena
Dedan Kimathi University of Technology
Bachelor of Science in Information Technology (4th Year)
