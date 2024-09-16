Overview
This guide will help you set up the Grade Computation Tool, a Flask web application for computing required grades based on user input. Follow these steps to configure your environment and launch the web interface.

Prerequisites
Python 3.x: Ensure Python 3 is installed on your system. You can download it from python.org.
Pip: Python’s package installer, usually included with Python 3.

Setup Instructions
1. Clone or Create the Project
If you have the project repository URL, clone it using Git:
git clone https://github.com/yourusername/grade-computation-tool.git
cd grade-computation-tool
Alternatively, create a new directory and add your app.py file to it.

2. Set Up a Virtual Environment
A virtual environment helps manage dependencies separately for each project. Create and activate a virtual environment as follows:
On Windows:
python -m venv venv
venv\Scripts\activate

3. Install Flask
With the virtual environment activated, install Flask using pip:
pip install flask

4. Add the Flask Application Code
Create a file named app.py in your project directory and paste the code.

5. Run the Flask Application
With the virtual environment activated and dependencies installed, start the Flask server by running:
python app.py

6. Access the Web Interface
Open a web browser and navigate to:
http://127.0.0.1:5000/

You should see the Grade Computation Tool interface. Enter your Prelim grade and optionally Midterm and Final grades, then click the "Compute" button to see the results.

Notes
Ensure that your Flask application is running. If you make changes to app.py, restart the Flask server for the changes to take effect.
If you encounter issues with Flask not being found, verify that the virtual environment is activated and Flask is properly installed.

Troubleshooting
Flask Not Found: Ensure that the virtual environment is activated and Flask is installed.
Application Errors: Check the terminal for error messages if the application does not start correctly.
