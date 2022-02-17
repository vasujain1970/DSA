# Objection Handling

## Introduction

- Contains the code for the objection handling feature.
- Includes, 
    - **Information extraction:** an NER model that extract relevant objections such as Budget, Information, Internal, Interested, Not Interested, Timing, Competitor, Authority.  

## Prerequisites

- Language: Python 3.8+
- Dependencies: see `requirements.txt`

## How to run

- To run the complete project, run the following command: `python api.py`
- Once you have started the API app, you can also acess the swagger at `http://localhost:8000/docs/`

## Input/Output structure

- Both modules take mail body (text) as input and return a JSON object. One sample input is, `(curl)`
```
curl -X 'POST' \
  'http://127.0.0.1:8000/objection_handling' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "text": "Hey Sri,  TBH now isn't a great time to chat about this type of software. Full disclosure, I am pretty fresh into a contract with SalesLoft and dont have any additional budget or bandwidth to add to the sales stack right now.  That said, I very much appreciate your emails and style of outreach."
}'
```
- Mail classification:
```
- Information extraction:
```
{
  "status": "Success",
  "message": "Code ran successfully",
  "result": {
    "Competitor": ["I am pretty fresh into a contract with SalesLoft"],
	"Budget": ["dont have any additional budget or bandwidth to add to the sales stack right now"]
  }
}
```

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

- Inside the code folder we have following structure 

```
├── data_prepration.py      # conversion to required .jsonl format
├── data_validation.py      # validation of dataset for fine-tuning
├── fine_tuning.py          # fine-tune the latest model
└── helper.py               # contains helper modules for Mail Writer APIs
```

## Model changelog

- Objection Handling:
    - `v1`: SpaCy model trained on 705 examples
  
## Contact
- For any code related queries, please contact Mohit Mayank (mohit.m@outplayhq.com).