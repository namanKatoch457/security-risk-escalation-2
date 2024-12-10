Security Risk Escalation API Documentation
Overview

The Security Risk Escalation API allows users to assess, adjust, and remove security risks in an organization. It helps manage vulnerabilities and take appropriate actions by enabling users to submit risk assessments, retrieve details of existing risks, and escalate or address identified issues.

Base URL
arduino
Copy code
https://api.example.com
Authentication
To interact with this API, you must authenticate using an API key. The API key must be included in the request header for authorization.

How to Obtain an API Key
Register an Account:

Create an account on the platform providing the API at https://example.com/signup.
Generate an API Key:

After logging into your account, navigate to the API Key Management section to generate a new API key at https://example.com/dashboard/api-keys.
Save the API Key:

The API key is sensitive, so store it securely and do not expose it publicly.
Using the API Key
Include the API key in the Authorization header of your HTTP request as a Bearer Token.

Example:

makefile
Copy code
Authorization: Bearer <YourAPIKey>
Example Request with Authentication
Using cURL:

bash
Copy code
curl -X GET "https://api.example.com/api/risk_assessments/12345" -H "Authorization: Bearer abc123"
In Postman:

Select Bearer Token under Authorization.
Enter your API key (abc123) in the token field.
Send the request to the API endpoint.
Error Handling for Authentication
401 Unauthorized: This error occurs when the API key is missing, invalid, or expired. Example response:

json
Copy code
{
  "error": "Unauthorized",
  "message": "Invalid or missing API key."
}
403 Forbidden: This error occurs if the API key does not have the necessary permissions to access the requested resource.

Endpoints


1. Create a New Risk Assessment

URL: /api/risk_assessments
Method: POST
Description: Allows users to submit a new risk assessment.
Request Body:
json
Copy code
{
  "risk_id": "12345",
  "description": "Unpatched software vulnerability in the server.",
  "severity": "high",
  "date_reported": "2024-12-10T10:00:00Z",
  "reported_by": "John Doe"
}


Response:

json
Copy code
{
  "risk_id": "12345",
  "description": "Unpatched software vulnerability in the server.",
  "severity": "high",
  "status": "open",
  "reported_by": "John Doe"
}
Errors:
400 Bad Request: Missing or invalid fields.


2. Get Risk Assessment

URL: /api/risk_assessments/{risk_id}
Method: GET
Description: Retrieves a specific risk assessment by its ID.
Path Parameters:
risk_id: The ID of the risk assessment to retrieve.
Response:
json
Copy code
{
  "risk_id": "12345",
  "description": "Unpatched software vulnerability in the server.",
  "severity": "high",
  "status": "open",
  "reported_by": "John Doe",
  "date_reported": "2024-12-10T10:00:00Z"
}


Errors:
404 Not Found: Risk assessment not found.
401 Unauthorized: Missing or invalid API key.
3. Update Risk Assessment
URL: /api/risk_assessments/{risk_id}
Method: PUT
Description: Allows users to update the details of an existing risk assessment.
Path Parameters:
risk_id: The ID of the risk assessment to update.
Request Body:
json
Copy code
{
  "description": "Updated description of the vulnerability.",
  "severity": "medium",
  "status": "closed"
}

Response:
json
Copy code
{
  "risk_id": "12345",
  "description": "Updated description of the vulnerability.",
  "severity": "medium",
  "status": "closed",
  "reported_by": "John Doe"
}


Errors:
400 Bad Request: Invalid or missing fields.
404 Not Found: Risk assessment not found.


4. Delete Risk Assessment
URL: /api/risk_assessments/{risk_id}
Method: DELETE
Description: Removes a risk assessment from the system.
Path Parameters:
risk_id: The ID of the risk assessment to remove.
Response:
json
Copy code
{
  "message": "Risk assessment deleted successfully."
}
Errors:
404 Not Found: Risk assessment not found.
401 Unauthorized: Missing or invalid API key.
Request and Response Format
Request Format
All requests, except for GET requests, should be sent with the Content-Type: application/json header, and the request body should be in JSON format.

Example request body for POST and PUT requests:

json
Copy code
{
  "risk_id": "12345",
  "description": "Unpatched software vulnerability in the server.",
  "severity": "high",
  "date_reported": "2024-12-10T10:00:00Z",
  "reported_by": "John Doe"
}
Response Format
Responses are returned in JSON format. Successful requests will return data related to the resource.

Example response:

json
Copy code
{
  "risk_id": "12345",
  "description": "Unpatched software vulnerability in the server.",
  "severity": "high",
  "status": "open",
  "reported_by": "John Doe",
  "date_reported": "2024-12-10T10:00:00Z"
}
Error Handling
The API will return HTTP status codes to indicate the result of the request. Here are some common error codes:

400 Bad Request: The request is malformed or contains invalid data.
401 Unauthorized: The request is missing or has an invalid API key.
403 Forbidden: The API key does not have permission to access the requested resource.
404 Not Found: The requested resource could not be found.
500 Internal Server Error: The server encountered an error while processing the request.
Example Error Response:
json
Copy code
{
  "error": "Bad Request",
  "message": "Invalid data provided."
}
Rate Limiting
To ensure fair usage and prevent abuse, the API has rate limiting in place. The current limits are:

100 requests per minute per API key.
Exceeding the rate limit will result in a 429 Too Many Requests error. After waiting for the reset time, the API key can be used again.

Conclusion
This API provides the tools to assess, manage, and escalate security risks within an organization. By leveraging the endpoints provided, users can track vulnerabilities, update their status, and remove risks as necessary, helping maintain a secure environment.

