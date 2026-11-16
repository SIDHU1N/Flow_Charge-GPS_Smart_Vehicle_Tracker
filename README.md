FlowCharge – GPS-Based Smart Vehicle Tracking & Toll Collection System

A GPS and IoT-based vehicle tracking and automated toll management system that integrates location tracking, cloud-based processing, distance calculation, vehicle management and toll transaction records.

📌 Project Overview

FlowCharge is a GPS-based smart toll collection system designed to explore automated and distance-oriented toll processing using IoT and cloud technologies.

The system collects vehicle location information through GPS coordinates and sends the data to a Python Flask backend. The backend processes location updates, calculates travelled distance and toll charges, and stores vehicle and trip information in MongoDB.

A web-based dashboard provides vehicle management, live location updates, wallet management and trip history.

Objectives

Develop a GPS-based vehicle tracking system.

Collect and process geographical location data.

Calculate vehicle travel distance and toll charges.

Maintain vehicle and trip information in a cloud database.

Provide real-time vehicle monitoring through a web dashboard.

Support wallet management and digital payment integration.

🏗️ System Architecture

             VEHICLE
                |
                v
           GPS MODULE
                |
                v
            ARDUINO
                |
                v
          GSM COMMUNICATION
                |
                v
          FLASK BACKEND
                |
         +------+------+
         |             |
         v             v
      MONGODB       TOLL PROCESSING
         |             |
         +------+------+
                |
                v
        REAL-TIME DASHBOARD
                |
                v
       VEHICLE & TRIP HISTORY

The architecture represents the intended hardware-to-cloud workflow. The current software repository also includes a Python-based GPS route simulator for sending location updates to the backend.

🛠️ Technologies Used

Hardware

Component

Purpose

Arduino UNO R3

Microcontroller

NEO-6M GPS

Geographical location acquisition

SIM800L GSM

Cellular communication

Software

Technology

Purpose

Python

Backend programming

Flask

Web application and REST APIs

MongoDB

Vehicle, trip and location storage

Flask-SocketIO

Real-time dashboard updates

Google Maps API

Route and map services

Geopy

Geographical distance calculation

HTML, CSS, JavaScript

Frontend development

Leaflet.js

Map visualization

Razorpay

Payment integration

QR Code

Vehicle identification

⚙️ Key Features

1. Vehicle Registration

Register and manage vehicle information.

Generate QR codes for registered vehicles.

Maintain vehicle ownership details.

2. GPS-Based Vehicle Tracking

Receive geographical coordinates.

Store vehicle location updates.

Display vehicle location through the dashboard.

3. Distance and Toll Calculation

Calculate geographical distance between consecutive GPS points.

Estimate highway distance using the current prototype's distance-gap heuristic.

Calculate toll charges using the configured rate.

4. Cloud Database Management

MongoDB maintains the following collections:

Collection

Purpose

users

User account information

vehicles

Registered vehicle details

live_pings

Vehicle location updates

trips

Completed trip records

5. Real-Time Dashboard

Display vehicle information.

Receive location updates using Socket.IO.

View trip history.

Visualize vehicle routes.

6. Wallet and Payment Management

Manage vehicle wallet balances.

Add wallet balance.

Create Razorpay payment orders.

Verify payment signatures.

Algorithms and Logic

1. Geographical Distance Calculation

The system uses the Geopy geodesic distance function to calculate the distance between consecutive geographical coordinates.

2. Highway Distance Estimation

The current dashboard_app.py implementation uses a threshold-based heuristic. A GPS ping-to-ping distance greater than 0.5 km is counted as highway distance.

This is a prototype estimation method, not actual road classification using highway map data.

3. Toll Calculation

The current backend uses a configured rate of ₹2.50 per kilometre.

TOLL_RATE_PER_KM = 2.5

toll_amount = highway_distance * TOLL_RATE_PER_KM

The toll amount is calculated using the estimated highway distance.

4. Automatic Trip Finalization

The backend checks vehicle movement and timestamps to identify when a trip should be finalized.

Application Workflow

A vehicle is registered in the system.

Vehicle location coordinates are generated or collected.

Location data is transmitted to the Flask backend.

The backend stores location updates in MongoDB.

Distance and toll-related calculations are performed.

Completed trip information is saved.

The dashboard displays vehicle and trip information.

📂 Project Structure

GPS_Smart_Vehicle_Tracker/
│
├── dashboard_app.py
├── simulate_tracker.py
│
├── app.py
├── app_1.py
├── app_2.py
├── app_3.py
│
├── templates/
│   ├── home.html
│   ├── register.html
│   ├── user_dashboard.html
│   ├── vehicle_register.html
│   ├── history.html
│   ├── trip_map.html
│   └── wallet_add.html
│
├── static/
│   ├── css/
│   ├── js/
│   └── qr/
│
├── requirements.txt
├── Dockerfile
├── docker-compose.yml
└── README.md

The structure above is illustrative; retain only folders and files present in the repository.

Installation and Setup

Prerequisites

Python 3.10 or later

MongoDB Atlas account or MongoDB instance

Google Maps API key

Git

Step 1: Clone the Repository

git clone https://github.com/HrithikgowdaD/GPS_Smart_Vehicle_Tracker.git

cd GPS_Smart_Vehicle_Tracker

Step 2: Create a Virtual Environment

python -m venv venv

Activate it on Windows:

venv\Scripts\activate

Step 3: Install Dependencies

pip install -r requirements.txt

Step 4: Configure Environment Variables

Create a .env file in the project root:

MONGO_URI=your_mongodb_connection_string
FLASK_SECRET_KEY=your_secret_key
RAZORPAY_KEY_ID=your_razorpay_key
RAZORPAY_KEY_SECRET=your_razorpay_secret
GOOGLE_MAPS_API_KEY=your_google_maps_api_key
APP_HOST=http://localhost:5000

Never upload actual credentials or API keys to GitHub.

Step 5: Run the Application

python dashboard_app.py

Open your browser:

http://127.0.0.1:5000

GPS Route Simulation

The repository includes simulate_tracker.py, which uses Google Directions API to generate route coordinates and send location updates to the Flask backend.

Run:

python simulate_tracker.py VEHICLE_NUMBER

Replace VEHICLE_NUMBER with a registered vehicle number.

The simulator sends location updates to:

/api/update_location

It finalizes the trip through:

/api/track_and_log

A valid Google Maps API key and running backend are required.

Expected Outputs

The application supports:

Vehicle registration and QR code generation.

Live GPS location records.

Vehicle tracking dashboard.

Trip distance and toll calculation.

Vehicle trip history.

Wallet balance management.

Payment order creation and verification.

Actual performance measurements should be added only after testing.

Current Prototype Limitations

GPS accuracy depends on satellite reception and environmental conditions.

Data transmission depends on network availability.

Highway distance is estimated using a simple distance-gap heuristic in the main backend.

The highway estimation method does not reliably distinguish highways from ordinary roads.

The prototype requires further validation on different routes and traffic conditions.

Large-scale deployment requires additional testing, security and scalability improvements.

Future Scope

Improve highway identification using digital road network classification.

Implement map matching for more accurate vehicle positioning.

Introduce AI-based traffic prediction.

Develop intelligent route optimization.

Improve distance-based toll calculation.

Integrate secure digital payment processing.

Develop advanced real-time analytics.

Project Contributors

Project: FlowCharge – GPS-Based Smart Vehicle Tracking and Toll Collection System

Contributors:

Hrithik Gowda D

Sidhu N

Department: Computer Science and Engineering (Data Science)

Academic Year: 2025–2026

Conclusion

FlowCharge demonstrates an approach to integrating GPS tracking, IoT hardware, Python-based backend services and cloud database technologies for vehicle monitoring and automated toll management.

The project provides a foundation for exploring intelligent transportation systems and future GPS-based distance-oriented toll collection solutions.
