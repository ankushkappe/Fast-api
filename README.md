FastAPI Project
This is a simple FastAPI project setup tutorial. This project demonstrates how to create a basic FastAPI application, set up the directory structure, and configure VS Code for development.

Project Structure
bash
Copy code
fastapi-project/
│
├── fastapi-env/            # Virtual environment directory
│
├── app/
│   ├── __init__.py         # Makes app a package
│   ├── main.py             # Main FastAPI application
│   ├── models.py           # Pydantic models
│   ├── routes.py           # API routes
│
├── tests/
│   ├── __init__.py         # Makes tests a package
│   ├── test_main.py        # Tests for the main application
│
├── .gitignore              # Git ignore file
├── requirements.txt        # Python dependencies
├── README.md               # Project README file
│
└── .vscode/
    └── settings.json       # VS Code settings (optional)
Setup Instructions
1. Create and Activate a Virtual Environment
Open a terminal and create a virtual environment:

sh
Copy code
python3 -m venv fastapi-env
source fastapi-env/bin/activate
2. Install Dependencies
Install FastAPI and Uvicorn:

sh
Copy code
pip install fastapi
pip install 'uvicorn[standard]'
3. Create the Directory Structure
Create the necessary directories and files:

sh
Copy code
mkdir fastapi-project
cd fastapi-project
mkdir app
touch app/__init__.py app/main.py app/models.py app/routes.py
mkdir tests
touch tests/__init__.py tests/test_main.py
touch .gitignore requirements.txt README.md
mkdir .vscode
touch .vscode/settings.json
4. Write the FastAPI Application
Edit app/main.py:

python
Copy code
from fastapi import FastAPI
from app.routes import router

app = FastAPI()

app.include_router(router)

@app.get("/")
async def read_root():
    return {"message": "Welcome to the FastAPI application!"}
Edit app/routes.py:

python
Copy code
from fastapi import APIRouter
from app.models import Country, countries

router = APIRouter()

@router.get("/countries")
async def get_countries():
    return countries

@router.post("/countries", status_code=201)
async def add_country(country: Country):
    countries.append(country)
    return country
Edit app/models.py:

python
Copy code
from pydantic import BaseModel, Field

class Country(BaseModel):
    country_id: int = Field(default_factory=_find_next_id, alias="id")
    name: str
    capital: str
    area: int

countries = [
    Country(id=1, name="Thailand", capital="Bangkok", area=513120),
    Country(id=2, name="Australia", capital="Canberra", area=7617930),
    Country(id=3, name="Egypt", capital="Cairo", area=1010408),
]

def _find_next_id():
    return max(country.country_id for country in countries) + 1
5. Configure VS Code
Update .vscode/settings.json:

json
Copy code
{
    "python.pythonPath": "${workspaceFolder}/fastapi-env/bin/python",
    "python.terminal.activateEnvironment": true,
    "python.analysis.extraPaths": ["./app"],
    "editor.formatOnSave": true
}
6. Run the Application
Start the Uvicorn server:

sh
Copy code
uvicorn app.main:app --reload
Navigate to http://127.0.0.1:8000 in your browser to see the welcome message.

Explanation
Virtual Environment: A self-contained directory that contains a Python installation for a particular version of Python, plus several additional packages.
FastAPI and Uvicorn: FastAPI is a modern, fast web framework for building APIs with Python 3.7+ based on standard Python type hints. Uvicorn is an ASGI web server implementation for Python.
Directory Structure: Organizes your project into logical parts such as the main application (app), tests, and configurations.
Main Application: Contains the main logic of your FastAPI application including routes and models.
VS Code Configuration: Ensures that VS Code uses the correct interpreter and settings for Python development.
This setup should help you get started with FastAPI and build scalable, high-performance web APIs.
