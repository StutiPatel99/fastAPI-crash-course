## Crash course with CRUD operations using FastAPI

FastAPI is a modern, fast, high-performance web-framework for building APIs with Python based on standard Python type hints. FastAPI runs with uvicorn and Pydantic.
> Uvicorn is the lightning-fast web server that actually runs your application.
> Pydantic is the underlying library that handles data validation, parsing, and serialization.

## Step 1: Installation

-> create a virtual environment
 python3 -m venv fastapi
 source fastapi/bin/activate

-> install fastapi with uvicorn
 pip install fastapi uvicorn

-> move the packages to requirements file
 pip freeze > requirements.txt

## Step 2: Code

-> Create a file as main.py and copy the below code:
```
from fastapi import FastAPI
from pydantic import BaseModel
from typing import List

app = FastAPI()

class Tea(BaseModel):
    id: int
    name: str
    origin: str

teas: List[Tea] = []

@app.get("/")
def read_root():
    return {"message": "Welcome to tea house"}

@app.get("/teas")
def get_teas():
    return teas

@app.post("/teas")
def add_teas(tea: Tea):
    teas.append(tea)
    return tea

@app.put("/teas/{tea_id}")
def update_tea(tea_id: int, updated_tea: Tea):
    for index, tea in enumerate(teas):
        if tea.id == tea_id:
            teas[index] = updated_tea
            return updated_tea
    return {"error": "Tea not found"}

@app.delete("/teas/{tea_id}")
def delete_tea(tea_id: int):
    for index, tea in enumerate(teas):
        if tea.id == tea_id:
            deleted = teas.pop(index)
            return deleted
    return {"error": "Tea not found"}
```

## Step 3: Running the code

Run the code by running below command in the terminal: 
uvicorn main:app --reload

## Step 4: Testing the code

-> FastAPI provides documents where we can review and test our code base.
Go to this page: http://127.0.0.1:8000/docs#/

You can test the code by entering values is 'POST: Add tea' and check if the values are added in 'GET: Get Teas'. Also try updating and deleting the tea data from different functions.

## And voila! You have created your first FastAPI project.
As the next step, add more functions and test and break the code. 

For more in-depth understanding of the framework, visit https://fastapi.tiangolo.com/

