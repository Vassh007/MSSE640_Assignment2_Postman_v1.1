<div align="center" style="margin-bottom: 30px;">
  <img src="https://github.com/user-attachments/assets/12e5a559-e31f-45eb-87ec-1858ff8f6240" alt="Postman Logo" width="90" style="margin-bottom: 10px;" />
  
  <h1 style="font-family: Arial, sans-serif; font-size: 34px; margin: 0;">
    Integration Testing with Postman
  </h1>
  
  <p style="font-size: 18px; font-style: italic; margin-top: 6px; color: #888;">
    MSSE Assignment 2_Postman_v1.1
  </p>
  
  <hr style="width: 60%; margin: 18px auto;" />
  
  <p style="font-size: 16px; margin: 4px 0;">
    ✍️ <strong>Authors:</strong> Jose Gracia Vallejo, Suvash Shrestha
  </p>
  <p style="font-size: 16px; margin: 4px 0;">
    🎓 <strong>Regis University</strong>
  </p>
  <p style="font-size: 16px; margin: 4px 0;">
    🧪 <strong>Software Quality & Test</strong>
  </p>
  <p style="font-size: 16px; margin: 4px 0;">
    📅 <strong>April 4, 2025</strong>
  </p>
</div>



## 📘 Introduction
Integration testing ensures that different software components or services work together as expected. This often involves testing APIs (Application Programming Interfaces) – the bridges that allow different systems to communicate in web development. Dr Lachlan Henderson states in *The Role of APIs in Modern Web and Mobile Applications*, "APIs (Application Programming Interfaces) have revolutionized how web and mobile applications are built, connecting systems and enabling seamless user experiences. They act as intermediaries that allow different software applications to communicate, making them a crucial part of modern app development." 

In this assignment, we will begin by exploring the basic functionality of **HTTP**, including its key components and how it enables communication between clients and servers.

We will also examine:
- 🤖 The role of **APIs** in modern software development  
- 🌍 Five publicly available **open APIs**  
- 🔒 An explanation of **Cross-Origin Resource Sharing (CORS)** and its significance in web security and cross-domain communication

---

  Furthermore, for this project, we employed Postman to interact with and validate the endpoints and data of two public APIs. We selected the Dummy REST API, an online REST service used for prototyping, and the Triangle Classification API created by our classmates Alex Fargo, Yab, and John Mark Kreski. This middleware service determines triangle types. These examples enabled us to illustrate fundamental HTTP principles (requests, responses, methods, status codes, statelessness), the significance of public APIs (including Open APIs), and essential integration testing concepts such as CORS, CRUD operations, error handling, and data persistence.

## 🌐 HTTP

**Hypertext Transfer Protocol (HTTP)** is the foundational protocol for data communication on the web, enabling interactions between clients and servers.

It defines how clients and servers exchange messages. Clients (like a web browser or Postman) send HTTP requests to servers, and servers return HTTP responses. Every request/response has a header (metadata like content type, status, etc.) and often a body (the payload data). As stated by Subhami in *Why is HTTP stateless? 🤔*
“HTTP defines how messages are formatted and transmitted between clients and servers... HTTP messages consist of two types: requests and responses. Requests are sent from clients to servers to ask for a resource or service... Responses are sent from servers to clients to deliver the requested resource or indicate the request's status.”

Each request comprises:
- 🔠 A method (verb)
- 📨 Headers
- 📝 An optional body

Each response includes:
- 📨 Headers  
- ✅ A status code  
- 📄 A body containing data or error details

🧠 Headers carry metadata like content type or authentication, while the body transmits content such as JSON or HTML.

### 🔁 Common HTTP Verbs:
- `GET`: Retrieve data  
- `POST`: Create a resource  
- `PUT`: Update a resource  
- `DELETE`: Remove a resource  

These correspond to web services' CRUD operations (Create, Read, Update, Delete). For example, a GET request fetches data (Read), a POST adds new data (Create), a PUT modifies data (Update), and a DELETE removes data (Delete). Postman makes it easy to execute these verbs and inspect the results. In our testing, we used GET and POST extensively (and also tried PUT/DELETE on the dummy API) to ensure all basic operations worked as expected.

Every HTTP response, known as HTTP Status Codes, has a status code that tells us whether the request succeeded. Status codes are grouped into categories: 2xx means success, 3xx indicates redirection, 4xx means a client-side error (bad request, not found, unauthorized, etc.), and 5xx means a server-side error. For example, 200 OK is returned for a successful GET, 201 Created for a successful resource creation via POST, 404 Not Found if the resource doesn’t exist, or 500 Internal Server Error if something went wrong. In our tests, we observed 200 OK for valid requests, and we intentionally triggered a 404 Not Found by requesting a non-existent record to see the error response.

### 📊 Example Status Codes:
- `200 OK` – Successful request  
- `201 Created` – Resource created  
- `400 Bad Request` – Invalid client request  
- `404 Not Found` – Resource not found  

 ⚠️ HTTP is **stateless**, meaning each request is independent. It is because it is stateless that the server does not retain information about previous requests. In practice, if you make two separate requests, the server will not remember information from the first request when handling the second. Additional mechanisms like **cookies** or **tokens** are used to maintain sessions.
 
---

## 🔧 APIs

### 🔌 APIs in Modern Applications

**Application Programming Interfaces (APIs)** allow software systems to communicate with one another.

In modern web and mobile apps, APIs:
- Connect the **front-end** to **back-end** services and databases  
- Enable **third-party integrations**  
- Promote **modular, scalable, and flexible** development

---

### 🌐 Open APIs
APIs are the glue of modern applications, allowing different services and client applications to interact. With APIs, developers can integrate functionality from external services instead of building everything from scratch. For instance, using a payment gateway API (like Stripe) to handle payments or a mapping API (like Google Maps) to embed location services. This leads to faster development, more innovation, and rich “mashup” applications that combine multiple services. (Mashup websites leverage multiple APIs – for example, a travel site might combine a Flight API, a Weather API, and Google Maps API to provide a cohesive user experience.) Thus, **Open API** is vital to software engineers as **Open APIs** are accessible to developers and users outside the organization. It is a publicly available endpoint that developers can access with minimal restrictions. They typically come with documentation and do not require special access permissions.

### ✨ Importance of Open APIs:
- 💡 Encourage innovation by enabling developers to build on existing services  
- 🔄 Foster collaboration and integration between systems  
- 🧰 Support app development, automation, and data sharing  

---

### 🗺️ Example: Google Maps Platform API

A modern example of Open API usage is the **Google Maps Platform API**, widely integrated into mobile and web apps for location-based services.

This API allows developers to:
- Embed maps  
- Perform geolocation queries  
- Calculate distances  
- Provide directions

🚖 Apps like **Uber** and **Lyft** rely heavily on Google Maps APIs to:
- Display routes  
- Estimate arrival times  
- Manage real-time driver/passenger locations

By exposing powerful geospatial functionality through an open API, Google empowers third-party developers to build rich, location-aware applications **without maintaining mapping infrastructure**.

---

## 🛡️ Cross-Origin Resource Sharing (CORS)

CORS is a mechanism that allows web applications on one domain to request resources from a server on a different domain despite the web's default same-origin policy. The same-origin policy usually prevents web pages from requesting a different domain for security reasons. For better understanding let provide an example of that we are running a web app on  `https://myapp.com` and want to fetch data from `https://api.someotherdomain.com`, the API server must explicitly permit it via CORS headers (like `Access-Control-Allow-Origin`).

It protects users from:
- 🎭 Cross-site request forgery (CSRF)  
- 🕵️‍♂️ Data leaks and malicious scripts

CORS is essential for **secure cross-origin communication**. It enables:
- Legitimate frontend apps on one domain to securely call APIs hosted on another  
- Protection from common web vulnerabilities

---

## 🔎 Public Open APIs List

Here are five publicly available Open APIs you can explore:

- 🚀 **SpaceX API**:  
  Provides real-time data on launches, rockets, capsules, and launchpads.

- 😂 **JokeAPI**:  
  Returns jokes based on categories like programming, general, or dark humor.

- 💰 **CoinGecko API**:  
  Offers up-to-date cryptocurrency prices, market data, and exchange listings.

- 🎲 **Bored API**:  
  Suggests random activities to fight boredom (e.g., educational, social, recreational).

- 📚 **OpenLibrary API**:  
  Grants access to book metadata from the Open Library project.

---

## 📚 Resources

- [📖 HTTP | MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP)  
- [🔐 What is CORS? | Web Security Academy](https://portswigger.net/web-security/cors)  
- [🧰 What is an API? | MuleSoft](https://www.mulesoft.com/api/what-is-an-api)  
- [📘 API Use Cases & Benefits | Kong](https://konghq.com/blog/learning-center/what-is-api)  
- [🗺️ Google Maps Platform Documentation](https://developers.google.com/maps/documentation)  
- [💡 API Examples | Netguru](https://www.netguru.com/blog/api-examples#:~:text=Public%20APIs%20are%20open%20for,work%20with%20specific%20business%20partners)
- [🌐 Why Is HTTP Stateless? | DEV.to](https://dev.to/codexam/why-is-http-stateless-2m3p#:~:text=HTTP%20stands%20for%20Hypertext%20Transfer,for%20a%20resource%20or%20a)  
- [🌐 The Role of APIs in Modern Web & Mobile Apps | DEV.to](https://dev.to/dr_lachlanhenderson_4dfa/the-role-of-apis-in-modern-web-and-mobile-applications-2coa#:~:text=APIs%20,part%20of%20modern%20app%20development)
-  [🧪 REST API Testing Best Practices | QAlified](https://qalified.com/blog/rest-api-testing/#:~:text=HTTP%20status%20codes%3A)
-  https://triangle-middleware-app-production.up.railway.app/swagger-ui/index.html#/quad-controller/deleteDefaults
-  https://dummy.restapiexample.com/

## 📸 Screenshots
![image](https://github.com/user-attachments/assets/32d85e22-bfa2-4fec-aa5d-2947cbfa7a41)
![image](https://github.com/user-attachments/assets/c70ce703-4861-4caf-a1c5-6cea16419981)
![image](https://github.com/user-attachments/assets/c3d583e7-88db-4bf7-b9aa-074f154942d7)
![image](https://github.com/user-attachments/assets/92f5e706-2d5a-4a33-bbf8-89477b9dfb69)
![image](https://github.com/user-attachments/assets/b462db74-df0c-4975-8121-7313e423ce69)
![image](https://github.com/user-attachments/assets/83cae643-f8ad-41d7-b477-cdea90d65b59)
![image](https://github.com/user-attachments/assets/bf0723a5-ca85-4a4a-8235-28321dabfdbc)
![image](https://github.com/user-attachments/assets/7ae8f49a-6990-442d-b519-7a1bea41a1c5)
![image](https://github.com/user-attachments/assets/53a06ae6-ac6a-4a3e-a7d3-ee3861036053)
![image](https://github.com/user-attachments/assets/b81abede-bedc-4bcb-97cb-a6ad330028ab)
![image](https://github.com/user-attachments/assets/bb54ba29-6fa7-461a-bc8c-14e5add64362)
![image](https://github.com/user-attachments/assets/d106f6b9-f6a2-4aca-bfb7-a9fed73a0303)
![image](https://github.com/user-attachments/assets/ba17db72-2c58-41bc-88b0-5173b34cd710)
![image](https://github.com/user-attachments/assets/2606adc7-3d23-4e0e-9a80-f675e821e0b1)
![image](https://github.com/user-attachments/assets/d692ad96-a328-49fa-9089-90f17514302c)
![image](https://github.com/user-attachments/assets/59266651-91ad-4892-93ea-a894f1932c58)
![image](https://github.com/user-attachments/assets/f7c659ad-d51c-4816-85e9-c878cc373853)
![image](https://github.com/user-attachments/assets/1cc52183-359d-4fba-b46f-e47342ed0a87)
![image](https://github.com/user-attachments/assets/ba45e88c-a958-4607-85cc-5950945ccff5)
![image](https://github.com/user-attachments/assets/b6466e61-61af-4323-a2c2-620ffd1603c3)
![image](https://github.com/user-attachments/assets/f2619e77-37d7-4696-8f3a-61a33b8ac16c)
![image](https://github.com/user-attachments/assets/9b4e96c7-1e74-42de-8a3b-8e804db30d1e)
![image](https://github.com/user-attachments/assets/c1fa09cc-1e31-4d39-a1b4-f54736d7f5b1)
![image](https://github.com/user-attachments/assets/d682eff1-795c-46f9-9909-1d60ebee6f77)
![image](https://github.com/user-attachments/assets/c78131a9-be4a-4cf3-854a-611b0a6b739e)
![image](https://github.com/user-attachments/assets/93717d17-1593-431f-ac20-ce8bb0a9f348)
![image](https://github.com/user-attachments/assets/e6d9223f-92de-44cd-b702-e44efff43437)
![image](https://github.com/user-attachments/assets/a68f12da-e344-4e70-b6f7-8380eff7f914)
![image](https://github.com/user-attachments/assets/d2a5ec7e-abcd-4ae6-9d03-75d87f636300)
![image](https://github.com/user-attachments/assets/a5766f9f-6027-4392-be20-731dc79c448f)
![image](https://github.com/user-attachments/assets/e598fe21-b293-42f8-a70d-79237e8fb187)
![image](https://github.com/user-attachments/assets/58efe199-ddf8-4048-a99b-c31b7e07c2df)
![image](https://github.com/user-attachments/assets/10aa00d3-d293-493e-b5d2-5dc9fecfad83)
![image](https://github.com/user-attachments/assets/397fad65-cfca-44a3-b72c-25bc29ddc749)
![image](https://github.com/user-attachments/assets/7648e9f2-e190-4798-9023-693447e92586)
![image](https://github.com/user-attachments/assets/5111a1b8-8ff0-4478-9055-26f831d69cbf)



## 🚀 Dummy REST API & 🔺 Triangle API Testing
### Dummy REST API & Geometrical API Testing  – Data Persistence
In this experiment, Dummy REST API responses are used and do not persist changes. A subsequent GET request returns the original static dataset after adding, updating, or deleting an employee. For example, the Dummy API always returns the same list of 24 employees (IDs 1–24) on each GET call, even after a new employee has been POSTed. The screenshot above shows that a follow-up GET for all employees did not include the new entry after creating a new employee, confirming that the API’s data is not saved between requests. In short, Dummy REST API is stateless regarding data storage: any write operations do not affect the results of future read requests. Example: After a successful DELETE operation (id:2), the employee list still included the supposedly deleted record.

Alternatively, we could store data for testing Triangles and Quadrilaterals using Swagger and the Git Bash CLI, as illustrated in the above image. However, this method only retrieves the most recently posted Quadrilateral, rather than any geometric shape created prior to the latest post. This indicates that the system does not fully retain information and operates in a stateless manner, as it relies on the most recent session to recall the data.

## Successful Request Examples (Dummy API)
- **GET All Employees:** A GET request to the /employees endpoint returns a JSON list of all employees with their details. The response includes a status ("success"), the data array (each with id, employee_name, employee_salary, etc.), and a message (e.g. “Successfully! All records has been fetched.”). In the screenshot, the API returned the full list of employees, demonstrating a successful READ request with the expected data and message.
  
- **GET Employee by ID:** Requesting a specific employee (e.g. /employee/1) returns just that one record. The API responds with "status": "success", a data object for the employee, and a message “Record has been fetched.” For example, getting employee ID 1 yields the record for “Tiger Nixon” with his salary and age. (Screenshot shows a single JSON object for the requested ID, confirming the GET-by-ID functionality.)

- **POST Request Issue with Dummy REST API (405 Method Not Allowed)**
While testing the Dummy REST API, we attempted to create a new employee by sending a POST request to the /create endpoint. Despite following the correct JSON format—providing a name, salary, and age—the API consistently responded with an error. The response returned was a 405 Method Not Allowed, accompanied by the following HTML-formatted error message:

                            ````html
                            Copy
                            Edit
                            Oops! An Error Occurred
                            The server returned a "405 Method Not Allowed".
                            Something is broken. Please let us know what you were doing when this error occurred.
                            We will fix it as soon as possible. Sorry for any inconvenience caused. ````
  This behavior was consistently observed across multiple attempts, with different payload variations (as shown in the screenshots). Each attempt to perform a POST request to create new   records failed identically. However, this issue arose only during the use of Postman, and we could make an employee through the CLI command in Git Bash.
- **PUT request to /update/1:**
Successfully returned "status": "success" along with a confirmation message, "Successfully! Record has been updated." This indicates that the API simulates successful updates without persisting them. In addition, CLI and Swagger with GUI were also able to perform this action successfully.

- **DELETE request to /delete/2:**
Returned "status": "success" and a confirmation message "Successfully! Record has been deleted". Again, this deletion was not persistent as subsequent GET requests still returned the same original data. Finally, it was also a success with Swagger and Git Bash.

##Advantages of cURL Over Postman:
- cURL successfully executed POST requests when Postman encountered unexplained 405 errors.

- Ideal for quick, repeatable, command-line-based testing, automation, and debugging API endpoints.

- Clearly demonstrates HTTP responses and error codes directly, without the overhead of a GUI.

##Summary of Observations:
- Persistence: Dummy API simulates CRUD operations without persistent storage. Each GET request returns static data.

- Error Handling: Consistent handling of invalid requests (405, 429, 404) across Postman and cURL, indicating robust error response handling.

- Tool Comparison: Postman provides an intuitive GUI, yet encountered unexplained method issues. cURL proved reliable for quick API interaction and debugging purposes.




---

✍️ **Authors**: Jose Gracia Vallejo, Suvash Shrestha  

