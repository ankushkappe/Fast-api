FastAPI Project
This is a simple FastAPI project setup tutorial. This project demonstrates how to create a basic FastAPI application, set up the directory structure, and configure VS Code for development.


1. Create and Activate a Virtual Environment
Open a terminal and create a virtual environment:


python3 -m venv fastapi-env
source fastapi-env/bin/activate
2. Install Dependencies
Install FastAPI and Uvicorn:


pip install fastapi
pip install 'uvicorn[standard]'

3. Run the Application
Start the Uvicorn server:

uvicorn app.main:app --reload
Navigate to -http://127.0.0.1:8000 in your browser to see the welcome message.

Explanation
Virtual Environment: A self-contained directory that contains a Python installation for a particular version of Python, plus several additional packages.
FastAPI and Uvicorn: FastAPI is a modern, fast web framework for building APIs with Python 3.7+ based on standard Python type hints. Uvicorn is an ASGI web server implementation for Python.
Directory Structure: Organizes your project into logical parts such as the main application (app), tests, and configurations.
Main Application: Contains the main logic of your FastAPI application including routes and models.
VS Code Configuration: Ensures that VS Code uses the correct interpreter and settings for Python development.
This setup should help you get started with FastAPI and build scalable, high-performance web APIs.
