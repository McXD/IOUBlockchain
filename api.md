# REST API for IOU Blockchain

The REST API is secured by Spring Security. Form login is the authentication method.

## Listing

### Registration

**URL**

`api/account/register`

**Method**

`POST`

**Data Params**

The endpoint expects a json request body in the form of:

```Json
{
	"username":"$username",
	"password":"$password"
}

```

Example:
```Json
{
	"username":"alice",
	"password":"alice"
}
```

**Response**

* On success: 
  * Code: 200
  * Body: `{"success":true}`
  
* On failure:
  * Code: 200
  * Body: `{"success":false}`


---

### Login

**URL**

`login`

**Method**

`POST`

**Data Params**

The endpoint expects POST body of `form-data`, whose field includes `username` and `password`

Example:
```text
POST /login HTTP/1.1
Host: 40.83.115.186:8080
Cookie: JSESSIONID=A9420B435D28A7E16C3FC1109B4DE112
Content-Length: 220
Content-Type: multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW

----WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="username"

bob
----WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="password"

bob
----WebKitFormBoundary7MA4YWxkTrZu0gW

```

**Response**

* On success: 
  * Code: 200
  * Body: `{"success":true}`
  
* On failure:
  * Code: 200
  * Body: `{"success":false}`

---

### View Relevant IOUs

**URL**

`api/iou/{username}/all`

**Method**

`GET`

**Data Params**

`None`

**Response**

* Successful retrieval
  * Code: 200
  * Body: a list of ious in json format

* Authentication error
  * Code: 403
  * Body: error message in json format

**Example**

Success:

```json
[
    {
        "lender": "bob",
        "borrower": "ryan",
        "amount": 500,
        "uid": "66decc0d-8fd1-46af-8b2c-148c51686f6c"
    }
]
```

Failure:

```json
{
    "timestamp": "2021-06-17T05:43:57.350+0000",
    "status": 403,
    "error": "Forbidden",
    "message": "Forbidden",
    "path": "/api/iou/bobb/all"
}
```

---

### Issue IOU

**URL**

`api/iou/{username}/issue`

**Method**

`POST`

**Data Params**

Request body is sent in json and expects these fields:

* **borrower**: the username of the borrower
* **amount**: the money amount to be paid

Example:

```json
{
    "borrower":"ryan",
    "amount":500
}
```

**Response**

* On Success:
  * Code: 200
  * Body: the linearId associated with the issued IOU

* Failure:
  * Code: 200
  * Body: empty json dictionary

---

### Pay IOU

**URL**

`api/iou/{username}/pay`

**Method**

`POST`

**Data Param**
Request body is sent in json and expects these fields:

* **uid**: the linearId of the IOU
* **payment**: the money amount to be paid

Example:

```json
{
    "uid":"66decc0d-8fd1-46af-8b2c-148c51686f6c",
    "payment":300
}
```

**Response**

* On success: 
  * Code: 200
  * Body: `{"success":true}`
  
* On failure:
  * Code: 200
  * Body: `{"success":false}`

---

### Delete IOU

**URL**

`api/iou/{username}/delete`

**Method**

`POST`

**Data Param**
Request body is sent in json and expects these fields:

* **uid**: the linearId of the IOU

Example:

```json
{
    "uid":"66decc0d-8fd1-46af-8b2c-148c51686f6c"
}
```

**Response**

* On success: 
  * Code: 200
  * Body: `{"success":true}`
  
* On failure:
  * Code: 200
  * Body: `{"success":false}`

**Note**

An IOU can only be deleted when the amount becomes exactly 0.
