# API Testing - Restful Booker

This repository contains a complete API testing project for the Restful-Booker application using Postman.

## 📘 Project Name

**API-Testing-Restful-Booker**

## 📄 Project Description

A simple Node booking form for testing RESTful web services.

## 🔗 API Documentation

[Restful-Booker API Docs](https://restful-booker.herokuapp.com/apidoc/index.html)

## 📁 Project Repository

[Original Repository](https://github.com/mwinteringham/restful-booker.git)

---

## ✅ Main Features Tested

- Create Booking
- Get Booking
- Update Booking
- Delete Booking
- Auth
- Verify Update

## 🧪 Methods Used

- `GET`
- `POST`
- `PUT`
- `DELETE`

## 🧾 Total Requests

**17** requests

## 🛠️ Data Generator

Used Postman’s dynamic variables like `{{$random...}}`

## 👤 Token Used

**Both** Environment and Global variables

## 🧪 Tools & Techniques

- **Postman**: API request handling
- **JavaScript (Pre-Request & Tests)**: Dynamic data, status validation
- **{{$random...}}**: For generating unique test data
- **Moment.js**: For dynamic check-in/check-out dates

---

## 🛠 Pre-request Script Example

```javascript
var firstName = pm.variables.replaceIn("{{$randomFirstName}}")
pm.environment.set("firstName", firstName)

var lastName = pm.variables.replaceIn("{{$randomLastName}}")
pm.environment.set("lastName", lastName)

var totalPrice = pm.variables.replaceIn("{{$randomInt}}")
pm.environment.set("totalPrice", totalPrice)

var depositPaid = pm.variables.replaceIn("{{$randomBoolean}}")
pm.environment.set("depositPaid", depositPaid)

const moment = require('moment')
const today = moment()

var checkIn = today.add(5, 'd').format('YYYY-MM-DD')
pm.environment.set("checkIn", checkIn)

var checkOut = today.add(10, 'd').format('YYYY-MM-DD')
pm.environment.set("checkOut", checkOut)

var additionalNeeds = pm.variables.replaceIn("{{$randomProduct}}")
pm.environment.set("additionalNeeds", additionalNeeds)
````

---

## ✅ Response Test Script Example

```javascript
var statuscode = pm.response.code;
console.log(statuscode);

if (statuscode === 200) {
    var jsonData = pm.response.json();
    pm.environment.set("id", jsonData.bookingid);
    pm.test("Request successful - 200 OK");
}
// ...Other status code conditions (201, 204, 400, 401, etc.)
else {
    pm.test("Unexpected status code received: " + statuscode);
}
```

---

## 📤 Sample POST Request

**URL**:

```
https://restful-booker.herokuapp.com/booking
```

**Method**:

```
POST
```

**Body**:

```json
{
    "firstname": "{{firstName}}",
    "lastname": "{{lastName}}",
    "totalprice": {{totalPrice}},
    "depositpaid": {{depositPaid}},
    "bookingdates": {
        "checkin": "{{checkIn}}",
        "checkout": "{{checkOut}}"
    },
    "additionalneeds": "{{additionalNeeds}}"
}
```

---

## 🧾 Sample API Documentation (Reference)

### ➕ Create Booking

**Method**: POST  
**Endpoint**: `/booking`

**Example**:

```bash
curl -X POST https://restful-booker.herokuapp.com/booking \
-H 'Content-Type: application/json' \
-d '{
    "firstname": "Jim",
    "lastname": "Brown",
    "totalprice": 111,
    "depositpaid": true,
    "bookingdates": {
        "checkin": "2018-01-01",
        "checkout": "2019-01-01"
    },
    "additionalneeds": "Breakfast"
}'
```

---
### 📊 Newman Report Sample


![Summary](https://drive.google.com/uc?export=view&id=1_EGc-QwXt5-2jiszfC7HyvE6tdJJffRv)
![Total Requests](https://drive.google.com/uc?export=view&id=12WOuGGar-hMDsLFSAQnSLl72iONxaZH3)
![Failed](https://drive.google.com/uc?export=view&id=1-7DbH5QJoMRhbhDAYxVm40J7Qm4ITRqg)
![Skipped](https://drive.google.com/uc?export=view&id=1Go7AYbHfUqSilBV-vT07RhOR5cR5rvEN)
