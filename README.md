# ReqRes API Testing with Postman

This repository contains API tests for the ReqRes API using Postman.

## API Endpoints Tested

| Method | Endpoint               | Description |
|--------|------------------------|-------------|
| GET    | `/api/users?page=2`    | Fetch users list |
| GET    | `/api/users/2`         | Fetch single user |
| POST   | `/api/users`           | Create a user |
| PUT    | `/api/users/2`         | Update a user |
| DELETE | `/api/users/2`         | Delete a user |

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
