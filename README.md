# University Timetable Application

This project is a final submission for the COSC 2610 Operating Systems course under Professor Sokhibjamol Boeva.
It is a "University Timetable" application built using Flask and deployed on an AWS EC2 instance with a PostgreSQL database hosted on RDS.
The application allows users to select their academic level (Undergraduate or Graduate) and view a dynamically generated timetable of courses for that level.

## Features
- Dynamic timetable generation based on academic level.
- Flask-based web application.
- PostgreSQL integration for managing course data.
- Deployed on AWS (EC2 for hosting, RDS for the database).

## Technologies Used
- Python (Flask framework)
- PostgreSQL
- AWS EC2 (for deployment)
- AWS RDS (for database hosting)

---

## Steps to Build and Deploy

### 1. Set Up AWS Services
- Create an AWS account and log in.
- Configure an EC2 instance and security groups.
- Set up a PostgreSQL database on AWS RDS with public access enabled.

### 2. Connect to the EC2 Instance
Use the following command to connect:
ssh -i "C:\your_key_2_ec2.pem" ubuntu@<EC2_Public_IP>

### 3. Prepare the EC2 Instance
Update the instance and install the required dependencies:
sudo apt update
sudo apt install python3 python3-pip postgresql-client -y

### 4. Connect to the RDS PostgreSQL Database
Connect to the database using:
psql -h <RDS_End_Point> -U <RDS_User> -d <RDS_Database_Name>

### 5. Create and Populate the Database Table
- Create the `timetable` table:
CREATE TABLE timetable (
    id SERIAL PRIMARY KEY,
    course_name VARCHAR(100),
    level VARCHAR(20),
    day VARCHAR(20),
    time VARCHAR(20)
);

INSERT INTO timetable (course_name, level, day, time)
VALUES
    ('Computer Languages', 'Undergraduate', 'Wednesday', '2:00 PM'),
    ('Operating Systems', 'Graduate', 'Tuesday', '2:00 PM'),
    ('Database Concepts', 'Graduate', 'Tuesday', '11:30 PM'),
    ('College Algebra', 'Undergraduate', 'Thursday', '9:00 AM'),
    ('Political Theory', 'Undergraduate', 'Monday', '4:20 PM');
    
### 6. Set Up the Flask Application
- Create a project directory:
mkdir my_project
cd my_project
touch app.py

- Implement the Flask application in `app.py` to connect to the PostgreSQL database.

### 7. Design HTML Templates
Create a `templates` folder and add `index.html` and `timetable.html` files with the necessary HTML code.

### 8. Set Up a Virtual Environment
- Create and activate a Python virtual environment:
python3 -m venv venv
source venv/bin/activate

### 9. Install Python Dependencies
Install the required libraries:
pip3 install --upgrade pip
pip3 install flask psycopg2-binary

### 10. Run the Flask Application
Start the app with:
python app.py

### 11. Access the Application
Open a web browser and go to:
http://<EC2_Public_IP>:8000

## Additional Notes
- Ensure your security groups in AWS allow HTTP traffic on port 8000.
- The Flask application must be properly configured to connect to the RDS PostgreSQL database using the provided credentials.
