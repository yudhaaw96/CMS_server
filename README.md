# CMS_server

## Authors

- **Yudha Arief Wijaya** - _Dev_ - [Github](https://github.com/yudhaaw96)
- Priambodo Kurniawan - Buddy Helper

## Client URL :

https://client-cms-ecommerce-yudhaaw96.firebaseapp.com/ (status : active)

## Server URL :

https://server-cms-ecommerce-yudhaaw96.herokuapp.com/ (status : active)

## SIGNUP USER

Create a new User

- ### URL

  /signup

- ### Method

  POST

- ### URL Params

  none

- ### Header Params

  none

- ### Data Params

  name = [string],<br>
  email = [string],<br>
  password = [string]

- ### Success Response

  - #### Code: 201
  - #### Content:

  ```
    {
        "CreatedUser": {
            "id": 1,
            "name": "admin",
            "email": "admin@admin.admin",
            "password": "$2a$10$ek0NmIkD7Zx4pL1O2pJJdeDLHC3AuDE2xQxdsZ9x2bnSQZVfbN606",
            "updatedAt": "2020-05-15T18:52:31.947Z",
            "createdAt": "2020-05-15T18:52:31.947Z",
            "role": "admin"
        }
    }
  ```

- ### Error Response:

  - #### Code: 400
    Bad Request
  - #### Content:

  ```
    {
        "code": 400,
        "type": "BAD REQUEST",
        "message": [
            {
            "message": "Please insert name"
            },
            {
            "message": "Name at least 3 characters, max 15"
            },
            {
            "message": "Please insert correct email format"
            },
            {
            "message": "Please insert email"
            },
            {
            "message": "Please insert password"
            },
            {
            "message": "Password at least 3 characters, max 15"
            }
        ]
    }
  ```

## SIGNIN USER

Login as a User and generate Access Token that generated by jsonwebtoken

- ### URL

  /signin

- ### Method

  POST

- ### URL Params

  none

- ### Header Params

  none

- ### Data Params

  email = [string],<br>
  password = [string]

- ### Success Response

  - #### Code: 200
  - #### Content:

  ```
    {
        "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6MSwiZW1haWwiOiJhZG1pbkBhZG1pbi5hZG1pbiIsInJvbGUiOiJhZG1pbiIsImlhdCI6MTU4OTU2ODc1Nn0.nkbzJ-0uTD3CD7-nw2Wc-2-gos1C9-eP-DRz705mPH4"
    }
  ```

- ### Error Response:

  - #### Code: 400
    Bad Request
  - #### Content:

  ```
    {
        "code": 400,
        "type": "BAD REQUEST",
        "errors": "Opps!, invalid email / password"
    }
  ```

## CREATE PRODUCT

Create a new Product

- ### URL

  /products

- ### Method

  POST

- ### URL Params

  none

- ### Header Params

  - #### Headers:
    access_token : [ Your Generated JSONWebToken (JWT) ]

- ### Data Params

  - #### Body (form url encoded):
    name = [string],<br>
    image_url = [string],<br>
    price = [integer],<br>
    stock = [integer],<br>

- ### Success Response

  - #### Code: 201

  - #### Content:

  ```
    {
        "CreatedProduct": {
            "id": 12,
            "name": "gorengan",
            "image_url": "http://gambar.url",
            "price": 1111,
            "stock": 2222,
            "UserId": 1,
            "updatedAt": "2020-05-16T05:33:17.460Z",
            "createdAt": "2020-05-16T05:33:17.460Z"
        }
    }
  ```

- ### Error Response:

  - #### Code: 400
    Bad Request
  - #### Content:

  ```
    {
        "code": 400,
        "type": "BAD REQUEST",
        "message": [
            {
            "message": "Please insert name"
            },
            {
            "message": "Please insert image url"
            },
            {
            "message": "Please insert valid url ex:(foo@bar.com)"
            },
            {
            "message": "Please insert price"
            },
            {
            "message": "Please insert stock"
            }
        ]
    }
  ```

  - #### Code: 401
    Unauthorized
  - #### Content:

  ```
    {
        "code": 401,
        "type": "UNAUTHORIZED",
        "message": "Please signin first!"
    }
  ```
  ```
    {
        "code": 401,
        "type": "UNAUTHORIZED",
        "message": "Sorry, not authorized, you are not an admin"
    }
  ```

# READ PRODUCT

Show All Products

- ### URL

  /products

- ### Method

  GET

- ### URL Params

  none

- ### Header Params

  - #### Headers:
    token : [ Your Generated JSONWebToken (JWT) ]

- ### Data Params

  none

- ### Success Response

  - #### Code: 200

  - #### Content:

  ```
    {
    "Products": [
            {
            "id": 1,
            "name": "gorengan",
            "image_url": "http://gambar.url",
            "price": 1111,
            "stock": 2222,
            "createdAt": "2020-05-15T21:38:41.642Z",
            "updatedAt": "2020-05-15T21:38:41.642Z",
            "UserId": 1
            },
            {
            "id": 2,
            "name": "gorengan",
            "image_url": "http://gambar.url",
            "price": 1111,
            "stock": 2222,
            "createdAt": "2020-05-15T21:55:43.203Z",
            "updatedAt": "2020-05-15T21:55:43.203Z",
            "UserId": 1
            }
        ]
    }
  ```

* ### Error Response:

  - #### Code: 401
    Unauthorized
  - #### Content:

  ```
    {
        "code": 401,
        "type": "UNAUTHORIZED",
        "message": "Please signin first!"
    }
  ```

## UPDATE PRODUCT

Update a Product

- ### URL

  /products/:id

- ### Method

  PUT

- ### URL Params

  ### Required:

  id = [integer]

- ### Header Params

  - #### Headers:
    token : [ Your Generated JSONWebToken (JWT) ]

- ### Data Params

  - #### Body (form url encoded):
    name = [string],<br>
    image_url = [string],<br>
    price = [integer],<br>
    stock = [integer],<br>

- ### Success Response

  - #### Code: 201
  - #### Content:

  ```
    {
    "UpdatedProduct": {
            "id": 1,
            "name": "gorengan EDIT",
            "image_url": "http://google.com",
            "price": 1000000,
            "stock": 2000000,
            "createdAt": "2020-05-15T21:38:41.642Z",
            "updatedAt": "2020-05-16T05:43:04.241Z",
            "UserId": 1
        }
    }
  ```

- ### Error Response:

  - #### Code: 401
    Unauthorized
  - #### Content:

  ```
    {
        "code": 401,
        "type": "UNAUTHORIZED",
        "message": "Sorry, not authorized, you are not an admin"
    }
  ```

  - #### Code: 404
    Not Found
  - #### Content:

  ```
    {
        "code": 404,
        "type": "NOT FOUND",
        "errors": "Sorry, not found"
    }
  ```

## DELETE PRODUCT

Delete a Product

- ### URL

  /products/:id

- ### Method

  DELETE

- ### URL Params

  ### Required:

  id = [integer]

- ### Header Params

  - #### Headers:
    token : [ Your Generated JSONWebToken (JWT) ]

- ### Data Params

  none

- ### Success Response

  - #### Code: 200
  - #### Content:

  ```
    {
    "DeletedProduct": {
            "id": 1,
            "name": "gorengan EDIT",
            "image_url": "http://google.com",
            "price": 1000000,
            "stock": 2000000,
            "createdAt": "2020-05-15T21:38:41.642Z",
            "updatedAt": "2020-05-16T05:43:04.241Z",
            "UserId": 1
        }
    }
  ```

- ### Error Response:

  - #### Code: 401
    Unauthorized
  - #### Content:

  ```
    {
        "code": 401,
        "type": "UNAUTHORIZED",
        "message": "Sorry, not authorized, you are not an admin"
    }
  ```

  - #### Code: 404
    Not Found
  - #### Content:

  ```
    {
        "code": 404,
        "type": "NOT FOUND",
        "errors": "Sorry, not found"
    }
  ```
