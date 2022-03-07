# Out of Office

## Introduction

- Contains the code for the out of office feature.
- Includes, 
    - **Mail classification:** a classifier model that takes the mail body as input and classifies it as either an "Out of Office" or "Not Out of Office" mail.
    - **Information extraction:** a NER model that extract relevant informations from the mail body including the out of office dates, the reason for the out of office, alternative contact details the person's name.  

## Prerequisites

- Language: Python 3.8+
- Dependencies: see `requirements.txt`

## How to run

- We can either run the complete project or the individual modules.
- To run the complete project, run the following command: `python api.py`
- To run the individual modules,
    -  Mail classification: `python ooo_mail_classification/code/api.py`
    -  Information extraction: `python ooo_information_extraction/code/api.py`
- Once you have started the API app, you can also acess the swagger at `http://localhost:8000/docs/`

## Endpoints
- `/out_of_office/health/status`: endpoint to check status
- `/out_of_office/get_current_commit_id`: endpoint to get current commit id
- `/out_of_office/ooo_mail_classification`: endpoint to get mail classification
- `/out_of_office/ooo_information_extraction`: endpoint to get entities from mail

## Input/Output structure

- Both modules take mail body (text) as input and return a JSON object. One sample input is, `(curl)`
```
curl -X 'POST' \
  'http://127.0.0.1:8000/ooo_mail_classification' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "text": "Thank you for the response. I will be out of office from 11th August to 14th August due to sick leave. I will return back to office on 15th August. For other enquries please contact Mark Rober / johndoe@gmail.com (123-456-7891). Regards, Jane Smith, VP of sales."
}'
```
- Mail classification:
```
{
  "status": "Success",
  "message": "Mail classification done!",
  "result": {
    "class": "Out of Office",
    "probOutOfOffice": 83.71,
    "probNotOutOfOffice": 16.29
  }
}
```
- Information extraction:
```
{
  "status": "Success",
  "message": "Code ran successfully",
  "result": {
    "date": {
      "oooStartDate": [
        "11/08/2021"
      ],
      "oooEndDate": [
        "14/08/2021"
      ],
      "officeStartDate": [
        "15/08/2021"
      ],
      "oooDateRange": []
    },
    "oooReason": [
      "sick leave"
    ],
    "primaryContact": {
      "primaryContactName": [
        "Jane Smith"
      ],
      "primaryContactEmail": [],
      "primaryContactPhone": [],
      "primaryContactDepartment": [],
      "primaryContactDesignation": [],
      "primaryContactAddress": [],
      "primaryContactOrg": [],
      "primaryAccountWebsite": []
    },
    "alternateContact": {
      "alternateContactName": [
        "Mark Rober"
      ],
      "alternateContactEmail": [
        "johndoe@gmail.com"
      ],
      "alternateContactPhone": [
        "123-456-7891"
      ],
      "alternateContactDepartment": [
        "sales"
      ],
      "alternateContactDesignation": []
    }
  }
}
```

## Status Codes
- `Success [200]`: returns successful execution of api request
- `Warning [400]`: returns partially valid results
- `Failure [500]`: returns catched exceptions

## Project structure

- The roto directory contains following,
    - **Subdirectories:** 
        - `ooo_information_extraction`: the module path that hosts the code and model for the information extraction.
        - `ooo_mail_classification`: the module path that hosts the code and model for the mail classification.
    - **Files:**
        - `api.py`: the FastAPI application that hosts the project API with endpoints to the all modules.
        - `README.md`: the project README.
        - `requirements.txt`: the project python package requirements.
        - `.gitignore`: the project gitignore.
```  
.
├── README.md
├── api.py
├── ooo_information_extraction/
├── ooo_mail_classification/
└── requirements.txt
└── .gitignore
```
- Inside each modules we have following structure, 

```
.
├── __init__.py    # project init file
├── code           # contains all .py files
├── config         # config files
├── model          # the best model
└── notebooks      # experimental notebooks
```

## Model changelog

- Mail classification:
    - `v3.1`: TFIDF + LogisticRegression trained on 1523 sample dataset + Regex for mails containing the phrase "be back".
    - `v3`: TFIDF + LogisticRegression trained on 1523 sample dataset.
    - `v2`: TFIDF + SVC trained on 1034 sample dataset with new preprocessing code.
    - `v1`: TFIDF + LogisticRegression trained on 519 sample dataset.
- Information extraction:
    - `v3`: Spacy NER transformer model trained on 1000 sample dataset, batch size 4, 100 epochs.
    - `v2`: Spacy NER transformer model trained on 500 sample dataset, batch size 4, 100 epochs.
    - `v1`: Spacy NER transformer model trained on 500 sample dataset, batch size 32, <100 epochs.
  
## Contact
- For any code related queries, please contact Mohit Mayank (mohit.m@outplayhq.com).
