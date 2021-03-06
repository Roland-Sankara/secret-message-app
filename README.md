# secret-message-app

>> Here is the link to the Secret message app
### Click here >>> [vercel](https://secret-message-app-nine.vercel.app/)


# EDU LOOKBOOK
> A place where all edu profiles can be stored and accessed.

## Tech Stack

* Node.js
* Express.js
* JSON web token (JWT)
* Bcrypt

## Main Files: Project Structure
```bash
     |-- src',
'        |-- index.js',
'        |-- server',
'            |-- app.js',
'            |-- config',
'            |   |-- connect.js',
'            |-- controllers',
'            |   |-- index.js',
'            |   |-- user.js',
'            |-- helpers',
'            |   |-- auth.js',
'            |   |-- index.js',
'            |   |-- validation.js',
'            |   |-- schemas',
'            |       |-- profile.js',
'            |-- models',
'            |   |-- index.js',
'            |   |-- userModel.js',
'            |   |-- schemas',
'            |       |-- profile.js',
'            |       |-- user.js',
'            |       |-- usersAllowed.js',
'            |-- routers',
'                |-- index.js',
'                |-- userRouter.js'

```


## Environment Variables

* PORT -- `server port number`
* DB_URL -- `database URL`
* SECRET -- `Secret key for verifying the token`
----


## User CRUD Operations


**SignUp User**
----
  Signs in a single user into the Application.

| Endpoint      | Method            | Params       |Data type |
|:------------- |:-----------------:| :-----------:|---------:|
| `/api/users/signup`  | POST        | `None`   |`None`    | 

* **Request Body**
    ```javascript
        {
            "username"    : "me@gmail.com",
            "method"      : "Local-auth",
            "firstName"   : "mefirst",
            "otherName"   : "meOther",
            "password"    : "mePassword",
            "userLevel"   :"1"
        }
    ```  
  

* **Request Headers**

  > None

* **Success Response:**

  **Status:** 200 OK <br />
     **Sample Content:**

   ```javascript
        {
            Message: "Successfully Added A New User",
            Token:"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXV
            CJ9eyJpZCI6IjVmMGYwY2UxZmZjNTQ1MGI
            3YzllMzk4OSIsI"
        }
    ```  
            
 
* **Error Response:**

  * **Status:** 400 BAD REQUEST <br />
    **Content:** `{ "Error": "The User Already Exists" }`

  OR

  * **Status:** 404 NOT FOUND <br />
    **Content:** `{  Error: 'Something went Wrong', err  }`

<br/>
<br/>

**Login User**
----
  Logs in a single user in the application.

| Endpoint      | Method            | Params       |Data type |
|:------------- |:-----------------:| :-----------:|---------:|
| `/api/users/login`  | GET        | `None`   |`None`    | 

* **Request Body**
    ```javascript
        {
            "username"    : "me@gmail.com",
            "method"      : "Local-auth",
            "firstName"   : "mefirst",
            "otherName"   : "meOther",
            "password"    : "mePassword",
            "userLevel"   :"1"
        }
    ```  
  

* **Request Headers**

  > None

* **Success Response:**

  **Status:** 200 OK <br />
     **Sample Content:**

   ```javascript
        {
            Message: "Logged in successfully",
            Token:"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXV
            CJ9eyJpZCI6IjVmMGYwY2UxZmZjNTQ1MGI
            3YzllMzk4OSIsI"
        }
    ```  
            
 
* **Error Response:**

  * **Status:** 400 BAD REQUEST <br />
    **Content:** `{ Error: 'Invalid Password Entered' }`

  OR

  * **Status:** 404 NOT FOUND <br />
    **Content:** `{ Error: 'User doesnot Exist >> Please SignUp first', err }`

<br/>
<br/>

**Get User By ID**
----
  Returns json data about a single user.

| Endpoint      | Method            | Params       |Data type |
|:------------- |:-----------------:| :-----------:|---------:|
| `/api/users/:id`  | GET           | `required`   |string    | 

* **Request Body**

  > None

* **Request Headers**

  > `{ authorization: "Bearer Token" }`

* **Success Response:**

  **Status:** 200 OK <br />
      **Sample Content:**

    ```javascript
        {
            "User": {
                        "userLevel": "1",
                        "canEdit": true,
                        "enabled": true,
                        "_id": "5f0f0ce1ffc5450b7c9e3989",
                        "username": "username@gmail.com",
                        "method": "Local-auth",
                        "firstName": "firstname",
                        "otherName": "",
                        "password": "$2b$10$THygMsPR95Ub55YuJzr
                            pResKVPk.5LPqonAMZHUQ3fre2m0V.SMGS",
                        "__v": 0
                    }
        }
    ```  
            
 
* **Error Response:**

  * **Status:** 404 NOT FOUND <br />
    **Content:** `{ Error: 'No User of given ID was Found' }`

  OR

  * **Status:** 400 BAD REQUEST <br />
    **Content:** `{ Error: 'Token is Invalid >> Enter valid token' }`
<br/>
<br/>

**Update User By ID**
----
  Updates data about a single user in the database.

| Endpoint      | Method            | Params       |Data type |
|:------------- |:-----------------:| :-----------:|---------:|
| `/api/users/:id`  | PATCH           | `required`   |string    | 

*   **Request Body**
    > Fields are not all required since its an update
    ```javascript
        {
            "username"    : "me@gmail.com",
            "method"      : "Local-auth",
            "firstName"   : "mefirst",
            "otherName"   : "meOther",
            "password"    : "mePassword",
            "userLevel"   :"1"
        }
    ```

* **Request Headers**

  > `{ authorization: "Bearer Token" }`

* **Success Response:**

  **Status:** 200 OK <br />
      **Sample Content:**

    ```javascript
        {
            Message: "User has been successfully Updated"
        }
    ```  
            
 
* **Error Response:**

  * **Status:** 404 NOT FOUND <br />
    **Content:** `{ Error: 'Something Went Wrong >>> User of Given ID was Not Found'}`

  OR

  * **Status:** 403 FORBIDDEN <br />
    **Content:** `{ Error: "Username Provided is Already Taken >> Enter Unique username"}`
<br/>
<br/>

**Delete User By ID**
----
  Delets a single user from the Data Base.

| Endpoint      | Method            | Params       |Data type |
|:------------- |:-----------------:| :-----------:|---------:|
| `/api/users/:id`  | DELETE        | `required`   |string    | 

*   **Request Body**
    
    > None

* **Request Headers**

  > `{ authorization: "Bearer Token" }`

* **Success Response:**

  **Status:** 200 OK <br />
      **Sample Content:**

    ```javascript
        {
             "Message": "User has been Deleted Successfully"
        }
    ```  
            
 
* **Error Response:**

  * **Status:** 400 BAD REQUEST <br />
    **Content:** `{ Error: "Something went Wrong >> User OF given ID was not found",err}`


-----

## Contributors

----

## Contributing