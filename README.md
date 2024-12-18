# Log Analysis Script

## Overview

The Log Analysis Script is a Python tool designed to analyze web server log files. It extracts and analyzes key information such as request counts per IP address, the most frequently accessed endpoints, and potential suspicious activity based on failed login attempts. This script is particularly useful for cybersecurity professionals and web administrators.

## Features

- **Count Requests per IP Address**: Parses the log file to count the number of requests made by each IP address and displays the results in descending order.
- **Identify the Most Frequently Accessed Endpoint**: Extracts endpoints from the log file and identifies the one accessed the most.
- **Detect Suspicious Activity**: Flags IP addresses with failed login attempts exceeding a configurable threshold (default: 10 attempts).
- **Output Results**: Displays results in a clear format in the terminal and saves them to a CSV file named `log_analysis_results.csv`.

## Requirements

- Python 3.13
- No external libraries are required.

## Installation

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/yourusername/log-analysis-script.git
   cd log-analysis-script
   ```
2. **Prepare the Log File**: Save your log entries in a file named sample.log in the same directory as the script.

## Usage

Run the script using Python:
   ```bash
   python main.py
   ```
## Sample Log File

You can use the following sample log entries for testing. Save it as sample.log:
   ```bash
   192.168.1.1 - - [03/Dec/2024:10:12:34 +0000] "GET /home HTTP/1.1" 200 512
   203.0.113.5 - - [03/Dec/2024:10:12:35 +0000] "POST /login HTTP/1.1" 401 128 "Invalid credentials"
   10.0.0.2 - - [03/Dec/2024:10:12:36 +0000] "GET /about HTTP/1.1" 200 256
   192.168.1.1 - - [03/Dec/2024:10:12:37 +0000] "GET /contact HTTP/1.1" 200 312
   198.51.100.23 - - [03/Dec/2024:10:12:38 +0000] "POST /register HTTP/1.1" 200 128
   203.0.113.5 - - [03/Dec/2024:10:12:39 +0000] "POST /login HTTP/1.1" 401 128 "Invalid credentials"
   192.168.1.100 - - [03/Dec/2024:10:12:40 +0000] "POST /login HTTP/1.1" 401 128 "Invalid credentials"
   10.0.0.2 - - [03/Dec/2024:10:12:41 +0000] "GET /dashboard HTTP/1.1" 200 1024
   198.51.100.23 - - [03/Dec/2024:10:12:42 +0000] "GET /about HTTP/1.1" 200 256
   192.168.1.1 - - [03/Dec/2024:10:12:43 +0000] "GET /dashboard HTTP/1.1" 200 1024
   203.0.113.5 - - [03/Dec/2024:10:12:44 +0000] "POST /login HTTP/1.1" 401 128 "Invalid credentials"
   203.0.113.5 - - [03/Dec/2024:10:12:45 +0000] "POST /login HTTP/1.1" 401 128 "Invalid credentials"
   192.168.1.100 - - [03/Dec/2024:10:12:46 +0000] "POST /login HTTP/1.1" 401 128 "Invalid credentials"
   10.0.0.2 - - [03/Dec/2024:10:12:47 +0000] "GET /profile HTTP/1.1" 200 768
   192.168.1.1 - - [03/Dec/2024:10:12:48 +0000] "GET /home HTTP/1.1" 200 512
   198.51.100.23 - - [03/Dec/2024:10:12:49 +0000] "POST /feedback HTTP/1.1" 200 128
   203.0.113.5 - - [03/Dec/2024:10:12:50 +0000] "POST /login HTTP/1.1" 401 128 "Invalid credentials"
   192.168.1.1 - - [03/Dec/2024:10:12:51 +0000] "GET /home HTTP/1.1" 200 512
   198.51.100.23 - - [03/Dec/2024:10:12:52 +0000] "GET /about HTTP/1.1" 200 256
   203.0.113.5 - - [03/Dec/2024:10:12:53 +0000] "POST /login HTTP/1.1" 401 128 "Invalid credentials"
   192.168.1.100 - - [03/Dec/2024:10:12:54 +0000] "POST /login HTTP/1.1" 401 128 "Invalid credentials"
   10.0.0.2 - - [03/Dec/2024:10:12:55 +0000] "GET /contact HTTP/1.1" 200 512
   198.51.100.23 - - [03/Dec/2024:10:12:56 +0000] "GET /home HTTP/1.1" 200 512
   192.168.1.100 - - [03/Dec/2024:10:12:57 +0000] "POST /login HTTP/1.1" 401 128 "Invalid credentials"
   203.0.113.5 - - [03/Dec/2024:10:12:58 +0000] "POST /login HTTP/1.1" 401 128 "Invalid credentials"
   10.0.0.2 - - [03/Dec/2024:10:12:59 +0000] "GET /dashboard HTTP/1.1" 200 1024
   192.168.1.1 - - [03/Dec/2024:10:13:00 +0000] "GET /about HTTP/1.1" 200 256
   198.51.100.23 - - [03/Dec/2024:10:13:01 +0000] "POST /register HTTP/1.1" 200 128
   203.0.113.5 - - [03/Dec/2024:10:13:02 +0000] "POST /login HTTP/1.1" 401 128 "Invalid credentials"
   192.168.1.100 - - [03/Dec/2024:10:13:03 +0000] "POST /login HTTP/1.1" 401 128 "Invalid credentials"
   10.0.0.2 - - [03/Dec/2024:10:13:04 +0000] "GET /profile HTTP/1.1" 200 768
   198.51.100.23 - - [03/Dec/2024:10:13:05 +0000] "GET /about HTTP/1.1" 200 256
   192.168.1.1 - - [03/Dec/2024:10:13:06 +0000] "GET /home HTTP/1.1" 200 512
   198.51.100.23 - - [03/Dec/2024:10:13:07 +0000] "POST /feedback HTTP/1.1" 200 128
   ```
## Output
### Terminal Output
The script will print the following information to the terminal:
   ```bash
   IP Address, Request Count
   192.168.1.1, 7
   203.0.113.5, 8
   10.0.0.2, 6
   198.51.100.23, 8
   192.168.1.100, 5
   
   Most Accessed Endpoint, Access Count
   /login, 13
   
   IP Address, Failed Login Count
   203.0.113.5, 8
   192.168.1.100, 5
   ```
![image](https://github.com/user-attachments/assets/e91f28a8-c93c-4e40-9fea-d76dbffb0b04)

CSV Output
The results will be saved in log_analysis_results.csv with the following structure:

**Requests per IP**: Columns: IP Address, Request Count
**Most Accessed Endpoint**: Columns: Endpoint, Access Count
**Suspicious Activity**: Columns: IP Address, Failed Login Count

## UI
### Thinker UI
To enhance user experience, the project includes a user-friendly Thinker UI. This interface allows users to interact with the log analysis features seamlessly. Key functionalities of the Thinker UI include:

**Upload Log Files**: Easily upload your web server log files for analysis.
**View Results**: Display analysis results in a visually appealing format, making it easier to interpret data.
**Filter Options**: Apply filters to focus on specific IP addresses or endpoints.
**Export Data**: Download the analysis results in CSV format directly from the UI.

## Getting Started with Thinker UI
Installation: Ensure you have the required dependencies installed. You can do this by running:
   ```bash
   pip install -r requirements.txt
   ```
Run the Application: Start the Thinker UI by executing:
   ```bash
   python app.py
   ```
**Upload Your Log File**: Use the upload button in the UI to select your log file.
![Screenshot 2024-12-05 002753](https://github.com/user-attachments/assets/dc4cbc36-d990-4dea-b3d5-f4cce75a88d5)

**Analyze**: Click on the "Analyze" button to process the log file and view the results.
![Screenshot 2024-12-05 002803](https://github.com/user-attachments/assets/991ad0e1-f2e7-42c8-ae3f-eb0e35d4a46d)

**Export**: If you wish to save the results, use the "Export" button to download the data in CSV format.
![ScreenRecording2024-12-05002723-ezgif com-video-to-gif-converter](https://github.com/user-attachments/assets/eb056366-3cb1-45bb-a16a-b904139c6420)

## Log Analysis Web Application

This project is a web application built using Flask that allows users to upload web server log files, analyze them, and download the results in CSV format. The application provides insights such as the number of requests per IP address, the most accessed endpoints, and failed login attempts.

### Features

- **Upload Log Files**: Easily upload your web server log files for analysis.
- **View Results**: Display analysis results in a visually appealing format.
- **Filter Options**: Apply filters to focus on specific IP addresses or endpoints.
- **Export Results**: Download the analysis results in CSV format directly from the UI.

### Getting Started
![ScreenRecording2024-12-09012529-ezgif com-video-to-gif-converter](https://github.com/user-attachments/assets/095ec3ce-dd35-4c74-ab8b-56bb9f8d5f8e)

### Prerequisites

- Python 3.13
- Flask
- Flask-WTF
- Flask-Bootstrap

### Running the Application
1.Start the Flask Application:
   ```bash
   python app.py
   ```


https://github.com/user-attachments/assets/59f85d23-b70f-44d4-884f-caf025373ec0


2. Access the Application:
Open your web browser and go to http://127.0.0.1:5000/.

### Project Structure
**app.py**: The main Flask application file handling routes and file uploads.
**main.py**: Contains the logic for analyzing log entries.
**templates/**: HTML templates for the web pages.
**static/**: Contains static files like CSS for styling.

### Usage
1. **Upload a Log File**: Use the upload form on the homepage to select and upload your log file.
2. **View Analysis Results**: After uploading, view the analysis results on the results page.
3. **Download CSV**: Click the download button to save the analysis results as a CSV file.License

## License
This project is [licensed](https://github.com/yogaV28/Log_Analysis_assigmentVRV/blob/main/LICENSE) under the MIT License. See the LICENSE file for details.
