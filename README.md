# Order Management App && APIs on Mulesoft 4

  - Objective :
    - To create a mulesoft application managing orders via REST API.
    - App must accept incoming orders and enable order lookups (JSON object).
    - App must persist incoming orders into database.
    - App must translate JSON order input to XML and log payload details to server.
    - App must support ID based lookup and respond with order details like Order ID, Order Date and country. 
    - App must expose order input and order lookup as APIs.
    - App must process request and reply with appropriate responses with specific order details.

API Logic Summary : 

| Method | Path | Payload | HTTP Response Code | Behaviour |
|----------|----------|----------|----------|----------|
| POST  | /orders  | Order Details JSON object| 201 Order Created | Accepts New Order
| GET  | /orders  | Order ID JSON Object | 200 OK (if Order Found) 404 (if Order not found) | Fetch & return Order details|
| PUT | NA | NA | 405 Unsupported Method | Return 405 Unsupported Method |
| DELETE | NA | NA | 405 Unsupported Method | Return 405 Unsupported Method |

Diagram showing Overall processing :

![demo-order-mgmt-3](https://github.com/user-attachments/assets/e65eb43b-62c7-472e-b810-a7603215f6a6)


 # HTTP POST (Order intake)

 Sequence diagram showing low level processing : 

![api-http-post](https://github.com/user-attachments/assets/49f185ec-fe84-411c-8b07-393799db54c8)

# HTTP GET (Order Look up)

Sequence diagram showing low-level processing :

![api-http-get-2](https://github.com/user-attachments/assets/8689d9ea-1d9f-435a-95b9-44dd7ae2e191)

# Some considerations and notes

  - HTTP Method(s) based routing : 
    - Method is evaluated to determine if request is for order submission (POST) or order look up (GET). All other methods are unsupported.
  - Parameterize by Environment 
   - Environment info like db connectivity info are parameterized using Global PROPERTY and configuration
  - Error handling :
    - Dedicated http response codes for success and Unsupported operations.
    - use of TRY to throw and handle errors from DB operations.
  - Testing :
    - Postman collections used to hit api endpoint.
  - Future enhancements : 
    - Modularize with sub-flows.
    - Validate API payload REQUESTS.
    - Implement ORDER listing mode with set fetch limits (/orders?mode=list).
    - Integrate ORDERs with downstream apps via queues or write files to on-prem/cloud Storage
