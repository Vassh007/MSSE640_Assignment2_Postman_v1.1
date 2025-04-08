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




---

✍️ **Authors**: Jose Gracia Vallejo, Suvash Shrestha  

