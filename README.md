Overview:
This project creates a fully serverless backend for managing a simple data resource It uses:
Amazon API Gateway to expose RESTful HTTP endpoints.
AWS Lambda to process logic and act as middleware.
Amazon DynamoDB to persist data in a fast, scalable NoSQL store.


Architecture Overview
<img width="554" height="308" alt="image" src="https://github.com/user-attachments/assets/f3e9ed58-653e-4866-8a92-7fce0ed5def0" />

How to work:
User/Client (Web App) sends a request to the API.
Amazon API Gateway receives the HTTP request and routes it.
API Gateway triggers the correct AWS Lambda function based on the endpoint and HTTP method.
AWS Lambda executes backend logic (e.g., validation, processing).
Lambda interacts with DynamoDB (read/write/update/delete data).
Lambda returns a response → API Gateway sends it back to the client.
