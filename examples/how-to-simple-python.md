# Using OAuth2.0 and SolveXia Public API for internal scripts with Python

This document contains a step by step guide on how to create a simple Python script that works with SolveXia API and authorizes through Client Credentials Flow.
This documentation does not cover an integration with SolveXia Python SDK. If you would like to learn more how to use SDK please follow this [link](https://github.com/solvexia/solvexia-python-sdk).

## Libraries

In order to write a simple script in Python you will need the following libraries

[requests](https://requests.readthedocs.io/en/master/) - to make HTTP calls.

## Create authorization credentials

Any application that is intended to access SolveXia Public API must have authorization credentials that identify the application to SolveXia authorization server. 
Please follow the next steps to create credentials for your applications:

1. Navigate to SolveXia API portal from the user dropdown menu.
2. Choose "Create new application". 
3. Specify the name and callback URL. Click "Create application".
4. If the creation is successful you will see Client Id and Client Secret credentials generated.
5. Copy credentials and store them safely. You will not be able to see Client Secret again unless you generate a new one.

## Create authorization function
We've created authorization credentials and now we are ready to create a script.

### Retrieve access token
First we need to create a function that obtains an access token via Client Credentials Flow that we can use further to call SolveXia APIs.

```python

import requests
import sys

client_id = "your_client_id"
client_secret = "your_client_secret"
environment = "https://your_environment_name.solvexia.com"

def get_access_token():
    pload = {'client_id': client_id, 'client_secret': client_secret,
             'grant_type': 'client_credentials'}
    url = environment + '/oauth/token'
    r = requests.post(url, data=pload)
    if r.status_code != 200:
        print("Error with generating an Access Token via Client Credential Flow")
        sys.exit()
    access_token = r.json()['access_token']
    hload = {'Authorization': 'Bearer ' + access_token}
    return hload
```

### Make an API call

Now we are ready to make an API call. 
To run the script with your application credentials, replace client_id, client_secret, environment url and process id.

```python

import requests
import sys

client_id = "your_client_id"
client_secret = "your_client_secret"
environment = "https://your_environment_name.solvexia.com"

def get_access_token():
    pload = {'client_id': client_id, 'client_secret': client_secret,
             'grant_type': 'client_credentials'}
    url = environment + '/oauth/token'
    r = requests.post(url, data=pload)
    if r.status_code != 200:
        print("Error with generating an Access Token via Client Credential Flow")
        sys.exit()
    access_token = r.json()['access_token']
    hload = {'Authorization': 'Bearer ' + access_token}
    return hload


def get_process_by_id(pid):
    hload = get_access_token()
    resp = requests.get(
        environment + '/api/v1/processes/' + pid, headers=hload)
    if resp.status_code != 200:
        print("Error occured while getting a process with pid" + pid)
        print(resp.json().message)
        sys.exit()
    return resp.json()


process = get_process_by_id('your_process_id')

print(process)

```
