# 📮 Postman API Testing Collections + Newman

![Postman](https://img.shields.io/badge/Postman-FF6C37?style=for-the-badge&logo=postman&logoColor=white)
![Newman](https://img.shields.io/badge/Newman-CLI-FF6C37?style=for-the-badge)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![GraphQL](https://img.shields.io/badge/GraphQL-E10098?style=for-the-badge&logo=graphql&logoColor=white)
![SOAP](https://img.shields.io/badge/SOAP-XML-0057B7?style=for-the-badge)

A set of **Postman collections** for manual and automated API testing of **REST, GraphQL and SOAP** services. The collections use JavaScript test scripts, pre-request scripts, environment and global variables, request chaining, data-driven runs from CSV, mock servers and OAuth 2.0. They are run from the command line with **Newman**, which produces HTML reports.

---

## 📚 Collections

| Collection | API type | Requests | Highlights |
|---|---|---|---|
| **Library** | REST | AddBook, GetBook, DeleteBook | Data-driven runs from `test.csv`; random ISBN in a pre-request script; response time, header and ID checks; self-cleaning with `pm.execution.setNextRequest()` when a book already exists |
| **GoogleAPI (Place)** | REST | AddPlace, GETPlace, UpdatePlace, DeletePlace | Full CRUD chain; `place_id` saved to a variable and reused by later requests |
| **ECommerceSite** | REST | Login, AddProduct, CreateOrder, ViewOrder, DeleteProduct | Token-based auth: the login token is saved and sent with later requests; multipart (form-data) product image upload |
| **OAuth2** | REST | GetAuthCode, ExchangeCode, ActualRequest | Google OAuth 2.0 authorization-code flow; deep JSON assertions (find, sum, map) on the course response |
| **OAuthCourses** | REST | AuthorizationRequest, GetCourseDetails | OAuth 2.0 token request and use of the access token |
| **GraphQL** | GraphQL | CreateLocation, CreateMutations, Query, DeleteMutations | Queries and mutations with variables; IDs chained between requests |
| **JIRAAPI** | REST | CreateBug, AddAttachment, DeleteIssue | Jira Cloud REST API v3: create an issue, attach a file, clean up |
| **MockAPITestingCourses** | REST (mock) | getapitestingcourses, GetCourseDetails | Tests against a **Postman mock server**; the course category found in the first response becomes the query parameter of the next |
| **SoapService** | SOAP | NumberToWord | SOAP XML request; response parsed with `xml2js` and checked against the expected value |

## ✨ Techniques used

- **Test scripts:** status code, response time, headers, body properties, and array searches with `pm.expect` and Chai assertions
- **Pre-request scripts:** dynamic test data with `{{$randomInt}}` and collection variables
- **Request chaining:** IDs and tokens saved with `pm.environment.set` / `pm.collectionVariables.set` and reused by later requests
- **Workflow control:** `pm.execution.setNextRequest()` to branch or clean up during a run
- **Data-driven testing:** iteration data from `test.csv` read with `pm.iterationData`
- **Environments:** separate **QA** and **UAT** environments plus a mock environment and globals, so the same collection runs against different targets
- **Mock servers:** contract-style testing before the real API exists
- **Protocols:** REST (JSON, form-data, multipart), GraphQL and SOAP (XML)

## 📁 Repository structure

```
Postman/
├── Collections/              # 9 exported Postman collections (v2.1)
├── environments/
│   ├── QA.postman_environment.json
│   ├── UAT.postman_environment.json
│   └── MockAPITestingCourses.postman_environment.json
├── global/API_Testing.postman_globals.json
├── newman/                   # Sample Newman HTML reports
├── test.csv                  # Data file for data-driven runs
└── shirts.png                # Sample file for upload requests
```

## 🚀 Running with Newman

**Prerequisites:** Node.js and Newman.

```bash
npm install -g newman newman-reporter-htmlextra
git clone https://github.com/nancyabcec1058/Postman.git
cd Postman
```

```bash
# Library collection against UAT, data-driven from CSV, with an HTML report
newman run Collections/Library.postman_collection.json \
  -e environments/UAT.postman_environment.json \
  -g global/API_Testing.postman_globals.json \
  -d test.csv \
  -r cli,htmlextra --reporter-htmlextra-export newman/

# Place API CRUD chain
newman run Collections/GoogleAPI.postman_collection.json -e environments/UAT.postman_environment.json
```

You can also import any collection and environment into the Postman app and run it with the **Collection Runner**.

> **Note:** the Jira, OAuth and e-commerce collections need your own credentials or tokens. Add them as environment variables before running.

## 👩‍💻 Author

**Nancy**, SDET / Senior QA Automation Engineer
[GitHub](https://github.com/nancyabcec1058) · [LinkedIn](https://www.linkedin.com/in/nancy1912)
