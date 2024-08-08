# ATEC API INTEGRATION PROJECT

# imports
import json
import requests
from pprint import pprint
from json import dump
from json import load

# function to GET data from Angaza API
def request_get(url, params=None, headers=None):
    try:
        response = requests.get(url, params=params, headers=headers)
        response.raise_for_status()
        json_data = response.json()
        return json_data
    except requests.exceptions.RequestException as e:
        return {"error": f"An error occurred: {e}"}       

# function to POST data to Kiva API, same function will work for loan drafts and repayment reports    
def request_post(url, params=None, headers=None, data=None):
    try:
        response = requests.post(url, params=params, headers=headers, data=data)
        response.raise_for_status()
        json_data = response.json()
        return json_data
    except requests.exceptions.RequestException as e:
        return {"error": f"An error occurred: {e}"}

# headers; url and authorization will change according to: 
# Angaza clients list from Cambodia or Bangladesh, Kiva testing environment or Kiva PA2 API, loan drafts or repayment reports

# This first url obtains client ID, Name, Phone, Gender and Address for Bangladesh
API_1_1_bd = {
    "url": "https://payg.angazadesign.com/data/clients",
    "headers": {
        "Authorization": "YmRfa2l2YV9hbmdhemFfY29ubmVjdF9hcGlAZ21haWwuY29tOlJ0eUAzNGZASGpyIzJlRQ==",
        "Accept": "application/json",
        "Content-Type": "application/json"
    }
}
# This second url obtains currency, total loan amount, payment date, payment interest and total loan amount for Bangladesh
API_1_2_bd = {
    "url": "https://payg.angazadesign.com/data/accounts",
    "headers": {
        "Authorization": "YmRfa2l2YV9hbmdhemFfY29ubmVjdF9hcGlAZ21haWwuY29tOlJ0eUAzNGZASGpyIzJlRQ==",
        "Accept": "application/json",
        "Content-Type": "application/json"
    }
}

# This first url obtains client ID, Name, Phone, Gender and Address for Cambodia
API_1_1_cam = {
    "url": "https://payg.angazadesign.com/data/clients",
    "headers": {
        "Authorization": "Basic Y2FtX2tpdmFfYW5nYXphX2Nvbm5lY3RfYXBpQGdtYWlsLmNvbTpSdHlAMzRmQEhqciMyZUU=",
        "Accept": "application/json",
        "Content-Type": "application/json"
    }
}
#This second url obtains currency, total loan amount, payment date, payment interest and total loan amount for Cambodia
API_1_2_cam = {
    "url": "https://payg.angazadesign.com/data/accounts",
    "headers": {
        "Authorization": "Y2FtX2tpdmFfYW5nYXphX2Nvbm5lY3RfYXBpQGdtYWlsLmNvbTpSdHlAMzRmQEhqciMyZUU=",
        "Accept": "application/json",
        "Content-Type": "application/json"
    }
}


#This url sends the client data to Kiva API
API_2 = {
    "url": "https://partner-api-stage.dk1.kiva.org/v3/partner/636/loan_draft",
    "headers": {
        "Authorization": "Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6Ik5BQTdIeWlxIn0.eyJhdWQiOlsiaHR0cHM6Ly9wYXJ0bmVyLWFwaS1zdGFnZS5kazEua2l2YS5vcmciXSwic2NvcGUiOlsiY3JlYXRlOmxvYW5fZHJhZnQiLCJjcmVhdGU6cmVwYXltZW50IiwicmVhZDpsb2FucyJdLCJpc3MiOiJodHRwczovL2F1dGgtc3RhZ2UuZGsxLmtpdmEub3JnLyIsInBhcnRuZXJJZCI6IjYzNiIsImV4cCI6MTY5Mjg3NDY1MywianRpIjoibkIzUVhWSDRVbGNiUWRSSjhuYkk4U0NYM180IiwiY2xpZW50X2lkIjoiWHBXT3ZkekdsTjhrbTdKYXVNMkE0SkRWZzNuNVlScmpaIn0.OFRmVLVotu8-EyQa4zvMasqCyb2KHdkLbhKI6lgGNOb7ehCQZQVgnA0TYR9Fq6_tOYdAkD3LoxNK8pT3i8wY1NeYLwHyn5dlq4cNSmBcHFz7nHMCZVnWtZJcHUPOryhaEQtNzGEAII41YRrY3JkYLEmOHJuaAC7MCFr4R4dL4AUMOhDO-QFN2ZIMg4fianQrZ_kVHM8zTt3MGUU14eQ-qKKm8TRcEmpcyhm3RmYaHiaAzIGTR3aPbdG0L5pGz2S59Zi1i0fJrhdX0Uvf_ByYuoyAq-0V0Z6sM9ClVoOQu6sJck8z2bLL-nQKfDiD5liQUMEzxvCI-Y2E71v7xdNp6Q"
    },
    "params": {
        "client_id": "XpWOvdzGlN8km7JauM2A4JDVg3n5YRrjZ", 
        "client_secret": "j2JGxNL5eIeAtUJuT2P8o4DGn0SEUbeUB1GJGLYPsS/HrpS1jzz+9LvalpmBURB8Ua"
    }
}

# actions
if __name__ == "__main__":

# Calling Angaza API to GET Angaza client data
    result_1 = request_get(url=API_1_1_bd["url"], headers=API_1_1_bd["headers"])
    print (result_1)
    print(type(result_1))

    result_1_2 = request_get(url=API_1_2_bd["url"], headers=API_1_2_bd["headers"])
    print (result_1_2)
    print(type(result_1_2))

    result_2 = request_get(url=API_1_1_cam["url"], headers=API_1_1_cam["headers"])
    print (result_2)
    print(type(result_2))

    result_2_1 = request_get(url=API_1_2_cam["url"], headers=API_1_2_cam["headers"])
    print (result_2_1)
    print(type(result_2_1))


# From the dictionary 1 create a JSON archive and save it in input.txt
    f = open("input.txt", "w")
    dump(result_1, f)
    
#From the dictionary 2 create a JSON archive and save it in input2.txt
    f = open("input2.txt", "w")
    dump(result_1_2, f)

#From the dictionary 3 create a JSON archive and save it in input3.txt
    f = open("input3.txt", "w")
    dump(result_2, f)

#From the dictionary 4 create a JSON archive and save it in input4.txt
    f  = open("input4.txt", "w")
    dump(result_2_1, f)  


def find_attribute(l, attribute):
    m = list(filter(lambda x: x["name"] == attribute, l))
    if len(m) > 0:
        return m[0]["value"]
    return None

def convert_for_sql(d):
    return {
        "client_id": d["qid"],
        "name": find_attribute(d["attribute_values"], "Full Name"),
        "gender": find_attribute(d["attribute_values"], "Gender"),
        "phone_1": find_attribute(d["attribute_values"], "Primary Phone"),
        "phone_2": find_attribute(d["attribute_values"], "Phone Number 2"),
        "serial": find_attribute(d["attribute_values"], "Serial number of Bio"),
        "hubspot_id": find_attribute(d["attribute_values"], "Hubspot deal ID"),
        "district": find_attribute(d["attribute_values"], "District"),
        "sub_district": find_attribute(d["attribute_values"], "Sub District"),
        "address": find_attribute(d["attribute_values"], "Address"),
        "agent": find_attribute(d["attribute_values"], "Agent"),
        "credit_upfront": find_attribute(d["attribute_values"], "Credit/Upfront"),
    }

# functions to filter some attributes for the SQLite database
def convert2_for_sql(d):
    return {
        "Client_id": d["client_qids"],
        "Loan_amount": d["full_price"],
        "Payment_date": d["payment_due_date"],
    }

#Bangladesh clients
f = open("input.txt", "r")
response = load(f)
clients = response["_embedded"]["item"]

for d in clients:
    pprint(convert_for_sql(d))

#Cambodia clients
f = open("input3.txt", "r")
response = load(f)
clients = response["_embedded"]["item"]  

for d in clients:
    pprint(convert_for_sql(d))


# This will be the data from API_1
    data_1 = {}

#  Calling Kiva API to POST Angaza client data, passing the object data=data_1
#    result_2 = request_post(url=API_2["url"], params=API_2["params"], headers=API_2["headers"], data=data_1)
#    print(result_2)

