'''
DOCSTRING GOES HERE
'''

import requests
from requests.auth import HTTPBasicAuth

# ServiceNow instance details
INSTANCE_URL = 'x'
TABLE_NAME = 'incident'  # Replace with your table name
USERNAME = 'xx'
PASSWORD = 'yy'

# Define Webex details
WEBEX_ACCESS_TOKEN = 'Bearer xxxx'
WEBEX_ROOM_ID = 'xxxx'

# Create the API endpoint URL
url = f'{INSTANCE_URL}/api/now/table/{TABLE_NAME}'

# Define headers for the request
headers = {
    'Content-Type': 'application/json',
    'Accept': 'application/json'
}
params = {
    'sysparm_query' : 'active=true^assigned_toISEMPTY^stateIN1,10^assignment_group=xxx',
    'sysparm_limit' : '100',  # Limit to 100 records per page (adjust as needed)
}

# Function to retrieve records from the ServiceNow table
def get_servicenow_data():
    '''
    DOCSTRING GOES HERE
    '''
    # Send a GET request to the ServiceNow API
    response = requests.get(
        url,
        auth=HTTPBasicAuth(USERNAME,
        PASSWORD),
        headers=headers,
        params=params
        )
    if response.status_code == 200:
        return response.json()["result"]
    else:
        print(f"Failed to retrieve records. HTTP Status Code: {response.status_code}")
        print(f"Error: {response.text}")



# Function to send a message to Webex
def send_webex_message(message):
    '''
    DOCSTRING GOES HERE
    '''
    url = 'https://webexapis.com/v1/messages'
    headers = {
        'Authorization': WEBEX_ACCESS_TOKEN,
        'Content-Type': 'application/json',
    }
    data = {
        "roomId": WEBEX_ROOM_ID,
        "text": message
    }
    response = requests.post(url, headers=headers, json=data)
    if response.status_code == 200:
        print("Message sent successfully!")
    else:
        print(f"Error sending message: {response.status_code}")


if __name__ == "__main__":
    unassigned_records = get_servicenow_data()
    for record in unassigned_records:
        message = f"Number: {record['number']}, Description: {record['short_description']}, Link: https://x.x.x/incident.do?sys_id={record['sys_id']}"
        send_webex_message(message) 
