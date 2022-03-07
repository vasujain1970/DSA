# Objection Handling

## Introduction

- Contains the code for the objection handling feature.
- Includes, 
    - **Information extraction:** a regex model that extract relevant objections such as Budget, Information, Internal, Interested, Not Interested, Timing, Competitor, Authority.  

## Prerequisites

- Language: Python 3.8+
- Dependencies: see `requirements.txt`

## How to run

- To run the complete project, run the following command: `python api.py`
- Once you have started the API app, you can also acess the swagger at `http://localhost:8000/docs/`

## Endpoints
- `/objection_handling/health/status`: endpoint to check status
- `/objection_handling/get_current_commit_id`: endpoint to get current commit id
- `/objection_handling/get_objections`: endpoint to get objections

## Input/Output structure

- Both modules take mail body (text) as input and return a JSON object. One sample input is, `(curl)`
```
curl -X 'POST' \
  'http://127.0.0.1:8000/objection_handling' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "text": "Hi Vamsi - appreciate the prep in your email. At the moment we're using outreach for our outbound engagement. I'm quite tight on time at the minute and not keen to put something in the calendar, but if you want to send me over why outplay would be a step up for us, I'm happy to take a look and come back to you if we're interested in exploring further. Thanks, Clay"
}'
```
- Objection extraction:
```
{
  "status": "Success",
  "message": "Code ran successfully",
  "result": "result": {
    "objections": [
      {
        "class": "Interested",
        "evidence": " if we're interested",
        "action": "",
        "answer": "",
        "evidence_start_index": 311,
        "evidence_end_index": 331
      },
      {
        "class": "Competitor",
        "evidence": "we're using outreach for ",
        "action": "",
        "answer": "",
        "evidence_start_index": 60,
        "evidence_end_index": 85
      }
    ]
  }
}
```
## Status Codes
- `Success [200]`: returns successful execution of api request
- `Warning [400]`: returns partially valid results
- `Failure [500]`: returns catched exceptions

## Project structure

- The root directory contains following,
    - **Files:**
        - `api.py`: the FastAPI application that hosts the project API with endpoints to the mail writer module.
        - `README.md`: the project README.
        - `requirements.txt`: the project python package requirements.
        - `.gitignore`: the project gitignore.
```  
.
├── README.md
├── api.py                  # runs the Fast API app
├── code/
└── requirements.txt
└── .gitignore
```

## Model changelog

- Objection Handling:
    - `v1`: Regex based system.
  
## Contact
- For any code related queries, please contact Bandi Saideva(bandi.s@outplayhq.com), Vasu Jain (vasu.j@outplayhq.com) and/or Mohit Mayank (mohit.m@outplayhq.com).
