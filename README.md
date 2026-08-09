# OSTAD-API-Automation-Assignment

This project contains automated API test scenarios for the **ReqRes API** using **Postman** and **Newman**. The collection is fully executable from the **command line locally**, as required in the ostad api automation assignment(batch 17).

---

## Author

**Ankan Das**  
📧 hello@ankandas.me  
🌐 https://ankandas.me

---


## Assignment Scenarios

### Q3 — Login with Registered Credentials
- Send `POST /login` request
- Verify **HTTP 200** response
- Capture and store **authToken** in the environment variable

### Q4 — GET User by userId
- Send `GET /users/{{userId}}` request
- Verify **HTTP 200** response
- Validate **first name**, **last name**, and **email**

### Q5 — PUT Updated Profile
- Send `PUT /users/{{userId}}` request
- Verify **HTTP 200** response
- Validate `updatedAt` timestamp exists and is a valid ISO timestamp

### Q6 — PATCH Single Field
- Send `PATCH /users/{{userId}}` request
- Verify **HTTP 200** response
- Validate only the target field is updated

### Q8 — Bad Request / Negative Scenarios
- Login without email → **400 Bad Request**
- Login without password → **400 Bad Request**
- Register without password → **400 Bad Request**
- Invalid user request → **404 Not Found**

---

## Project Structure

```text
OSTAD-API-Automation-Assignment/
├── collections/
│   └── OSTAD_API_Automation_Assignment.postman_collection.json
├── environments/
│   └── OSTAD_API_Assignment_Environment.postman_environment.json
├── reports/ 
│   └── api-report.html
└── README.md
```

---

## Prerequisites

Install the following tools:

- **Node.js** (v18+ recommended)
- **Postman**
- **Newman**

Check installation:

```bash
node -v
npm -v
```

---

## use this to Clone
```bash
git clone https://github.com/ankandas101/OSTAD-API-Automation-Assignment.git

cd OSTAD-API-Automation-Assignment
```

## Install Newman

```bash
npm install -g newman
```

Install the HTML reporter:

```bash
npm install -g newman-reporter-htmlextra
```

---

## Import Files into Postman

1. Open **Postman**
2. Click **Import**
3. Import the following files:


### Collection

```text
collections/OSTAD_API_Automation_Assignment.postman_collection.json
```

### Environment

```text
environments/OSTAD_API_Assignment_Environment.postman_environment.json
```

---

## Environment Variables

Configure these variables in Postman before exporting the environment file:

| Variable | Example Value |
|----------|---------------|
| `baseUrl` | `https://reqres.in/api` |
| `apiKey` | `YOUR_REQRES_API_KEY` |
| `userId` | `10` |
| `authToken` | *(auto-generated after login in Q3)* |
---

## API Key Setup

ReqRes requires an API key for `/api/*` endpoints.

1. Visit: **https://app.reqres.in/api-keys**
2. Create or copy your API key
3. Save it in the `apiKey` environment variable

All requests use this header:

```http
x-api-key: {{apiKey}}
```

---

## Run Collection in Postman

1. Select the imported environment
2. Open the collection
3. Click **Run Collection**
4. Execute all requests sequentially

---
## Command Line Execution (****)

Run the Postman collection locally using **Newman**:

```bash
npx newman run collections/OSTAD_API_Automation_Assignment.postman_collection.json \
  -e environments/OSTAD_API_Assignment_Environment.postman_environment.json
```

This command executes the exported Postman collection directly from the terminal, satisfying the assignment requirement that the collection JSON must be executable from the command line locally.

## Generate HTML Report

```bash
mkdir -p reports

npx newman run collections/OSTAD_API_Automation_Assignment.postman_collection.json \
  -e environments/OSTAD_API_Assignment_Environment.postman_environment.json \
  -r cli,htmlextra \
  --reporter-htmlextra-export reports/api-report.html
```

After execution, open the generated report:

```bash
xdg-open reports/api-report.html
```

---

## Expected Results

| Scenario | Expected Status |
|---------|----------------|
| Login with valid credentials | **200** |
| Get user by ID | **200** |
| PUT update profile | **200** |
| PATCH single field | **200** |
| Login without email | **400** |
| Login without password | **400** |
| Register without password | **400** |
| Invalid user lookup | **404** |

---

## Local Execution Verification 

Successful execution (09/08/2026) should show output similar to:

```text
requests ............... 8
test-scripts ........... 16
prerequest-scripts ..... 13
assertions ............. 24
failed ................. 0
```
<img width="1920" height="1185" alt="report screenshot" src="https://github.com/user-attachments/assets/f2177855-a911-41e8-9d7a-d9a4d5f113c2" />


All requests and assertions pass successfully when executed with Newman.
---

## Notes
- The project is for OSTAD API Automation assignment.
- This project uses the **public ReqRes demo API**.
- `PUT` and `PATCH` endpoints return **mocked responses** for testing purposes.
- All requests include automated **status code validation**, which is mandatory according to the assignment requirements.

---

