# Dokumentasi API F8    

## Host
https://projects.upanastudio.com/f8-api

## Schedule

**Stage**
----
  List data panggung

* **URL**

  `/schedule/stage`

* **Method:**

  `GET`
  
*  **URL Params**

  

   **Required:**
 
  

   **Optional:**
 

* **Data Params**


* **Success Response:**
  

  * **Code:** 200 <br />
    **Content:** 
    ```json
    {
        "status": true,
        "data": [
          {
            "id_stage": "19051273",
            "name": "F8 Fine Art"
          },
          {
            "id_stage": "33617945",
            "name": "F4 Folks"
          },
          {
            "id_stage": "35819726",
            "name": "F2 Food and Fruits"
          },
          {
            "id_stage": "40975168",
            "name": "Main Stage"
          },
          .....
        ]
    }
    ```
 
* **Error Response:**



* **Sample Call:**

    ```shell
    curl --request GET \
        --url http://<host>/schedule/stage
    ```

* **Notes:**



**List event**
----
 List data event

* **URL**

    `/schedule/event`

* **Method:**
  
  `GET`
  
*  **URL Params**

   **Optional:**
 
   `id_stage=[alphanumeric]`
   
   Event berdasarkan stage

* **Data Params**

* **Success Response:**

  * **Code:** 200 <br />
    **Content:**
    ```json
    {
      "status": true,
      "data": [
        {
          "id_schedule": "11740285",
          "id_stage": "19051273",
          "name": "Pantai",
          "day": "1",
          "start": "08:00:00",
          "end": "09:00:00"
        },
        {
          "id_schedule": "62486795",
          "id_stage": "40975168",
          "name": "Dance",
          "day": "2",
          "start": "08:00:00",
          "end": "10:00:00"
        }
      ]
    }
    ```
 
* **Error Response:**


* **Sample Call:**

  ```shell
    curl --request GET \
        --url http://<host>/schedule/event
    ``` 

* **Notes:**


## Merchant

**Login merchant**
----
  

* **URL**

  `/merchant/login`

* **Method:**

  `POST`
  
*  **URL Params**
 

* **Data Params**
  
   **Required:**
    
    `username=[string]`

    `password=[string]`

    contoh:
    ```json
    {
    	"username": "makanan",
    	"password": "qazwsxedc"
    }
    ```

* **Success Response:**
  

  * **Code:** 200 <br />
    **Content:** 
    ```json
    {
      "status": true,
      "data": {
        "token":    "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpZF9tZ   XJjaGFudCI6Ijg5MTgwNDI3In0.  V_XfHJITqzisTO6Mbjx-GGhqZ4InkU2TAMLSbd7R7AU"
      }
    }
    ```
 
* **Error Response:**
  * **Code:** 400 BAD REQUEST <br />

  OR

  * **Code:** 200 <br />
    **Content:** 
    ```json
    {
      "status": false,
      "msg": "Username Salah"
    }
    ```


* **Sample Call:**

    ```shell
    curl --request POST \
      --url http://<host>/merchant/login \
      --header 'content-type: application/json' \
      --data '{
    	"username": "makanan",
    	"password": "qazwsxedc"
    }'
    ```

* **Notes:**



**Buat transaksi**
----
 

* **URL**

    `/merchant/transaction`

* **Method:**
  
  `POST`
  
*  **URL Params**


* **Data Params**
  
  **Required:**
    
  `amount=[integer]`

  `information=[string]`

	`qr_code=[string]`


    contoh:
    ```json
    {
    	"amount": 20,
    	"information": "makanan",
    	"qr_code": "asdadsa"
    }
    ```
* **Headers**

  `Authorization:<token>`

* **Success Response:**

  * **Code:** 200 <br />
    **Content:**
    ```json
    {
      "status": true,
      "data": {
        "transaction": {
          "amount": 20,
          "information": "makanan",
          "qr_code": "asdadsa",
          "id_merchant": "89180427",
          "id_transaction": "30532749"
        }
      }
    }
    ```
 
* **Error Response:**
  * **Code:** 400 BAD REQUEST <br />
  * **Code:** 401 UNAUTHORIZED <br />

  OR

  * **Code:** 200 <br />
    **Content:** 
    ```json
    {
      "status": false,
      "msg": "Jumlah point tidak mencukupi"
    }
    ```
    * **Code:** 200 <br />
    **Content:** 
    ```json
    {
      "status": false,
      "msg": "Qr Code tidak valid"
    }
    ```

* **Sample Call:**

  ```shell
    curl --request POST \
      --url http://<host>/merchant/   transaction \
      --header 'authorization:eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpZF9tZXJjaGFudCI6Ijg5MTgwNDI3In0.V_XfHJITqzisTO6Mbjx-GGhqZ4InkU2TAMLSbd7R7AU' \
      --header 'content-type: application/json' \
      --data '{
    	"amount": 20,
    	"information": "makanan",
    	"qr_code": "asdadsa"
    }'
  ``` 

* **Notes:**

**History transaksi**
----
 

* **URL**

    `/merchant/transaction`

* **Method:**
  
  `GET`
  
*  **URL Params**


* **Data Params**
  
 
* **Headers**

  `Authorization:<token>`

* **Success Response:**

  * **Code:** 200 <br />
    **Content:**
    ```json
    {
      "status": true,
      "data": {
        "transactions": [
          {
            "qr_code": "asdadsa",
            "information": "makanan",
            "amount": "20",
            "date": "2019-09-27 11:59:50"
          },
          {
            "qr_code": "dfjlkjkdf",
            "information": "makanan",
            "amount": "20",
            "date": "2019-09-26 16:58:41"
          },
          .....
        ]
      }
    }
    ```
 
* **Error Response:**
  * **Code:** 401 UNAUTHORIZED <br />


* **Sample Call:**

  ```shell
    curl --request GET \
      --url http://localhost/f8_api/merchant/   transaction \
      --header 'authorization:eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpZF9tZXJjaGFudCI6Ijg5MTgwNDI3In0.V_XfHJITqzisTO6Mbjx-GGhqZ4InkU2TAMLSbd7R7AU'
  ``` 

* **Notes:**


## Player

**Register Player**
----
  

* **URL**

  `/player/register`

* **Method:**

  `POST`
  
*  **URL Params**
 

* **Data Params**
  
   **Required:**
    
    `qr_code=[string]`

    `player_id=[string]`

    contoh:
    ```json
    {
    	"qr_code": "dfjlkjkdf",
    	"player_id": "nursan"
    }
    ```

* **Success Response:**
  

  * **Code:** 200 <br />
    **Content:** 
    ```json
    {
      "status": true,
      "data": {
        "token":    "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpZF9tZXJjaGFudCI6Ijg5MTgwNDI3In0.V_XfHJITqzisTO6Mbjx-GGhqZ4InkU2TAMLSbd7R7AU"
      }
    }
    ```
 
* **Error Response:**
  * **Code:** 400 BAD REQUEST <br />

  OR

  * **Code:** 200 <br />
    **Content:** 
    ```json
    {
      "status": false,
      "msg": "ID Player tidak teredia"
    }
    ```


* **Sample Call:**

    ```shell
    curl --request POST \
      --url http://<host>/player/register \
      --header 'content-type: application/json' \
      --data '{
    	"qr_code": "dfjlkjkdf",
    	"player_id": "nursan"
    }'
    ```

* **Notes:**



**Player Finish**
----
 

* **URL**

    `/player/finish`

* **Method:**
  
  `GET`
  
*  **URL Params**


* **Data Params**
  
* **Headers**

  `Authorization:<token>`

* **Success Response:**

  * **Code:** 200 <br />
    **Content:**
    ```json
    {
      "status": true,
      "data": {
        "end": "2019-09-26 12:49:48"
      }
    }
    ```
 
* **Error Response:**
  * **Code:** 401 UNAUTHORIZED <br />

  
* **Sample Call:**

  ```shell
    curl --request GET \
  --url http://<host>/player/finish \
  --header 'authorization: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJxcl9jb2RlIjoiZGZqbGtqa2RmIiwibmFtZSI6Im51cnNhbiIsImlkX3BsYXllciI6IjgyODUzNjQ3In0.atCryfXgmGfXAc-WskpsM5IJQCVZaQcS6XS9dDeQg4U'
  ``` 

* **Notes:**
