# ReqRes API Testing with Postman

## Overview
This repository contains API test cases for the ReqRes API, executed using Postman. It covers essential CRUD operations such as retrieving, creating, updating, and deleting users.

## API Endpoints Tested

| Method | Endpoint               | Description        |
|--------|------------------------|--------------------|
| GET    | `/api/users?page=2`    | Fetch users list  |
| GET    | `/api/users/2`         | Fetch single user |
| POST   | `/api/users`           | Create a user     |
| PUT    | `/api/users/2`         | Update a user     |
| DELETE | `/api/users/2`         | Delete a user     |

## Test Cases Implemented

### GET List of Users
- **Request:** `GET https://reqres.in/api/users?page=2`
- **Assertions:**
  - Status Code = `200`
  - Response contains users
- **Postman Test Script:**
  ```javascript
  pm.test("Status code is 200", function () {
      pm.response.to.have.status(200);
  });

  pm.test("Response contains users data", function () {
      var jsonData = pm.response.json();
      pm.expect(jsonData.data).to.be.an('array');
      pm.expect(jsonData.data.length).to.be.greaterThan(0);
  });
  ```

### GET Single User
- **Request:** `GET https://reqres.in/api/users/2`
- **Assertions:**
  - Status Code = `200`
  - Response contains correct user ID
- **Postman Test Script:**
  ```javascript
  pm.test("Status code is 200", function () {
      pm.response.to.have.status(200);
  });

  pm.test("Response contains user details", function () {
      var jsonData = pm.response.json();
      pm.expect(jsonData.data.id).to.eql(2);
  });
  ```

### POST Create User
- **Request:** `POST https://reqres.in/api/users`
- **Body:**
  ```json
  {
      "name": "John Doe",
      "job": "Software Engineer"
  }
  ```
- **Assertions:**
  - Status Code = `201`
  - Response contains correct name
- **Postman Test Script:**
  ```javascript
  pm.test("Status code is 201", function () {
      pm.response.to.have.status(201);
  });

  pm.test("Response contains user name", function () {
      var jsonData = pm.response.json();
      pm.expect(jsonData.name).to.eql("John Doe");
  });
  ```

### PUT Update User
- **Request:** `PUT https://reqres.in/api/users/2`
- **Body:**
  ```json
  {
      "name": "Jane Doe",
      "job": "Product Manager"
  }
  ```
- **Assertions:**
  - Status Code = `200`
  - Response contains updated name
- **Postman Test Script:**
  ```javascript
  pm.test("Status code is 200", function () {
      pm.response.to.have.status(200);
  });

  pm.test("Response contains updated name", function () {
      var jsonData = pm.response.json();
      pm.expect(jsonData.name).to.eql("Jane Doe");
  });
  ```

### DELETE User
- **Request:** `DELETE https://reqres.in/api/users/2`
- **Assertions:**
  - Status Code = `204`
- **Postman Test Script:**
  ```javascript
  pm.test("Status code is 204", function () {
      pm.response.to.have.status(204);
  });
  ```

## Running Tests in Postman

### **1️. Import Collection into Postman**
1. Open **Postman**.
2. Click **Collections** → **Import**.
3. Upload the collection JSON file.

### **2. Run Collection in Postman Runner**
1. Click **Runner** → Select **ReqRes API Testing Collection**.
2. Click **Run** to execute all tests.

## Automating Tests via CLI (Optional)
To run tests using **Newman**, install it via:
```bash
npm install -g newman
```
Then run:
```bash
newman run ReqRes_API_Collection.json
```



