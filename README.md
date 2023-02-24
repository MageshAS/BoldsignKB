# BoldsignKB
                      How to send document on behalf of others
Introduction
In BoldSign, you can perform several operations on behalf of another user. For this, you should add that user as your sender identity, and that user should approve your request. Once this is done, you can perform the actions like sending documents, download audit log, revoke, remind, change access code etc. The documents you sent on behalf of another user will be displayed under the  Behalf Documents section in the BoldSign application.
When you send a document on behalf of another person, you will need to provide their email address in onBehalfOf property.
 
Here the another person’s email address is provided in onBehalfOf property.
CURL : 

curl -X 'POST' \ 'https://api.boldsign.com/v1/document/send' \
      -H   'accept: application/json' \
      -H   'X-API-KEY: {your API key}' \
      -F   'BrandId=' \
      -F   'OnBehalfOf=luthercooper@cubeflakes.com' \
      -F   'Signers={
               "name": "David",
               "emailAddress": "david@cubeflakes.com",
              }' \
      -F 'ExpiryDays=10' \




. NET : 

var apiClient = new ApiClient("https://api.boldsign.com", "{your API key}");
var documentClient = new DocumentClient(apiClient);

var documentFilePath = new DocumentFilePath
{
    ContentType = "application/pdf",
    FilePath = "agreement.pdf", 
};
var signer = new DocumentSigner(
  name: "David",
  emailAddress: "david@cubeflakes.com",
  formFields: formFieldCollections);

var documentSigners = new List<DocumentSigner>()
{
     signer
};

var sendForSign = new SendForSign()
{
    Message = "please sign this",
    Title = "Agreement",
    Signers = documentSigners,
    Files = filesToUpload,
    OnBehalfOf = "luthercooper@cubeflakes.com"
    };
var documentCreated = documentClient.SendDocument(sendForSign);
 

 










PYTHON : 

import requests

url = "https://api.boldsign.com/v1/document/send"

payload={'DisableExpiryAlert': 'false',
'EnableReassign': 'true',
'Message': 'Please sign this.',
'Signers': '{
          "name": "David",
          "emailAddress": "david@cubeflakes.com",
          "formFields": [
            {
              "isRequired": true
          ]
        }',
'ExpiryDays': '10',
'EnablePrintAndSign': 'false',
'AutoDetectFields': 'false',
'OnBehalfOf': 'luthercooper@cubeflakes.com',
files=[
  ('Files',('file',open('{file path}','rb'),'application/octet-stream'))
]
headers = {
  'accept': 'application/json',
  'X-API-KEY': '{your API key}'
}
response = requests.request("POST", url, headers=headers, data=payload, files=files)

print(response.text)


Sender Identity :
To perform on behalf of operations, the sender identity should be added and approved. Add the user as a sender identity, and then the user will get an email for approval. Once the user approves this request, you can perform operations on behalf of that user.
The below steps will guide you through step by step process of how to create a sender identity, update the identity, delete an identity, list all the identities, request for approval, and resend the invitation.



Create identity : 
Creates a new sender identity by taking the name and email address. Multiple sender identities can be created. You can refer more details from this link.
CURL : 

curl -X 'POST' \
  'https://api.boldsign.com/v1/senderIdentities/create' \
  -H 'accept: */*' \
  -H 'X-API-KEY: {your API key}' \
  -H 'Content-Type: application/json;odata.metadata=minimal;odata.streaming=true' \
  -d '{
  "name": "Luther Cooper",
  "email": "luthercooper@cubeflakes.com"
}'

Update identity : 
Updates the name of the existing sender identity. Should provide the email address of the sender identity for this. Refer this link.
CURL :

curl -X 'POST' \
  'https://api.boldsign.com/v1/senderIdentities/update?email=luthercooper@cubeflakes.com' \
      -H 'accept: */*' \
      -H 'X-API-KEY: {your API key}' \
      -H 'Content-Type: application/json;odata.metadata=minimal;odata.streaming=true' \
      -d '{
          "name": "Luther"
        }'

 
Delete Identity : 
Deletes the existing sender identity by taking the email address. Once it is deleted, it cannot be retrieved. Refer this link.
CURL :

curl -X 'DELETE' \
  'https://api.boldsign.com/v1/senderIdentities/delete?email=luthercooper@cubeflakes.com' \
      -H 'accept: */*' \
      -H 'X-API-KEY: {your API key}'


