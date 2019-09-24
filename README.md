# Dokumentasi API F8    


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
    
