# Track Order

##Register a shipment for tracking: [IN]

>POST request. URL:

```
https://www.clickpost.in/api/v2/tracking/awb-register/
Headers: {'Content-type': 'application/json'}
```

>__Sample Payload__

```json
{
  "waybill": "ABCDRESDEFGHIJKL1257679",
  "cp_id": 1,
  "key": "42d42a34-ae09-4693-b20c-ae2624218a329",
  "account_code": "Fedex Domestic",
  
  "consumer_details": {
          "name": "Test Customer",
          "phone": "8080808080",
          "email": "test@clickpost.in"
  },
  "shipment_info": {
          "item": "Shirt",
          "order_type": "COD",
          "invoice_value": 1000,
          "reference_number": "123XYZ",
          "length": 10,
          "height": 10,
          "weight": 10,
          "breadth": 10,
          "drop_pincode": "110001",
          "pickup_pincode": "110001",
          "delivery_type": "FORWARD",
          "cod_amount": 1000.10,
          "drop_address": "Roots hacker Home, R 28, Second Floor, Nehru Enclace, Opposite Nehru Place, New Delhi 110001",
          "additional": {
                    "items": [
                        {
                            "sku": "XYZ1",
                            "description": "item1",
                            "quantity": 1,
                            "price": 200,
                            "images": "<Image URL>",
                            "return_days": 2,
                            "additional": {
                                "length": 10,
                                "height": 10,
                                "breadth": 10,
                                "weight": 100
                            }
                        }
                    ]
                  }
  },
  "additional": {
    "order_date": "2017-02-14T18:00:00+05:30",
    "ship_date": "2017-02-14T23:00:00+05:30",
    "min_edd": 2,
    "max_edd": 4,
    "enable_whatsapp": false,
    "order_id": "ORDER-12"
  }
}

```
>__Response__

```json
{
  "meta": {
    "message": "SUCCESS",
    "status": 200,
    "success": true
  },
  "result": {
    "security_key": "530470b0-8ebd-40c3-9c9e-6ca6bf1d29b8",
    "consumer_details": {
      "id": 1
    },
    "shipment_info": {
      "id": 1
    },
    "tracking_id": 1188264
  }
}
```

Note: All orders are passed a security_key in response. Please store this security key to be used in Customer engagement platform.

###Fields Explanation

####Compulsory:

Parameter | Type | Description
--------- | ---- | -----------
key (required) | character | this is the API Key
waybill (required) | character | this is waybill number [AWB Number or LR Number] that you want to register in Clickpost
cp_id (required) | integer | courier_partner_id as specified on page 1 of this documentation
account_code (required) | string | account code added in Clickpost dashboard while creating courier partner account

####Optional:

####consumer_details (optional): In case you want Clickpost to send notifications to your customers via mail / sms, please pass information in this object:
Parameter | Type | Description
--------- | ---- | ----------- 
name | character (250 chars) | end customer name, who will receive the shipment, this will be used to personalize the SMS / email sent to the customer
phone_number | 10/11 characters | customer phone number on which SMS is to be sent.
email | character (150 chars) | Email address of the customer, on which email is to be sent.

####shipment_info (optional): shipment information for rich analytics on your data:
Parameter | Type | Description
--------- | ---- | ----------- 
item | character (500 chars) | name of item sent to the customer
order_type | character | either COD or PREPAID
invoice_value | float | shipment invoice value
reference_number | character (len: 100) | order_id or reference number to be shared with end customer
length | integer | in cm
breadth | integer | in cm
height | integer | in cm
weight | integer | in grams
drop_pincode | character | 6 digit pincode of drop location
pickup_pincode | character | 6 digit pincode of pickup location
delivery_type | character | either FORWARD / RVP
cod_amount| float field | COD value to be collected from customer, float field
drop_address| character (500 chars) | drop address of the shipment
additional | object | optional field which can have additional information related to items like sku, description, quantity, image, price and return_days for return management solution (easier for end customer to select which product to return)
additional --> items --> return_days | integer | number of days allowed for a product to be accepted as return

####additional (optional): extra information about shipment used to power tracking page:
Parameter | Type | Description
--------- | ---- | ----------- 
order_date | character | timestamp when the order was placed
ship_date | character | timestamp when order was ready to ship 
min_edd | integer | minimum days commited to the customer for 1st delivery attempt
max_edd | integer | maximum days commited to the customer for 1st delivery attempt
enable_whatsapp | boolean | if you have whatsapp for business account, you can pass opt-in information here so Clickpost starts sending out communications to customers
order_id | string (50 characters) | Order ID of the shipment


API response: "meta" --> "status": 200 and 303 represents success response

##Register a shipment for tracking: [MENA, SEA, EU, US]

>POST request URL:

```
https://www.clickpost.in/api/v3/tracking/awb-register/?key=<clickpost_api_key>

Headers: {'Content-type': 'application/json'}
```

>__Sample Payload__

```json
{
    "waybill": "ABCDRESDEFGHIJKL",
    "courier_partner": 1,
    "account_code": "Fedex Domestic",

    "shipment_info": {
        "order_type": "COD",
        "invoice_value": "12345",
        "cod_amount": "1000",
        "currency_code": "SAR",
        "reference_number": "123XYZ",
        "order_id": "order_id of the shipment",
        "length": 10,
        "height": 10,
        "weight": 10,
        "breadth": 10,
        "items": [
            {
                "sku": "XYZ1",
                "description": "item1",
                "quantity": 1,
                "price": 200,
                "images": "<Image URL>",
                "return_days": 2,
                "length": 10,
                "height": 10,
                "breadth": 10,
                "weight": 100
            }
        ]
    },

    "pickup_info": {
        "name": "Rashid Alma",
        "email": "warehouse_1@hotmail.com",
        "phone_code": "966",
        "phone": "8001111090",
        "address": "KRAMAT ASEM RAYA N0. 6, UTAN KAYU SELATAN, JAKARTA TIMUR 13120",
        "postal_code": "JK0701",
        "city": "Riyadh",
        "district": "XYZ",
        "state": "Al-Riyadh",
        "country_code": "SA",
        "lat": 10.01,
        "long": 10.2
    },

    "drop_info": {
        "name": "Amal Hisham",
        "email": "a_maal11@hotmail.com",
        "phone_code": "966",
        "phone": "558022554",
        "address": "JALAN PANJANG NO. 08, JAKARTA BARAT",
        "postal_code": "JK0703",
        "city": "JK0703",
        "district": "XYZ",
        "state": "Al-Riyadh",
        "country_code": "AE",
        "lat": 10.01,
        "long": 10.01
    },

    "additional": {
        "enable_whatsapp": false,
        "language_code": "EN",
        "order_date": "2017-02-14",
        "ship_date": "2017-02-14",
        "min_edd": 2,
        "max_edd": 4
    }
}
```

>__Response__

```json
{
  "meta": {
    "message": "SUCCESS",
    "status": 200,
    "success": true
  },
  "result": {
    "security_key": "530470b0-8ebd-40c3-9c9e-6ca6bf1d29b8"
  }
}
```

Note: All orders are passed a security_key in response. Please store this security key. 

API response: "meta" --> "status": 200 and 303 represents success response. All the other status codes represent a failure. Our API will always return HTTP status code 200.

###Fields Explanation

####Compulsory:

Parameter | Type | Description
--------- | ---- | -----------
waybill (required) | character (100 chars) | this is waybill number [AWB Number or LR Number] that you want to register in Clickpost
courier_partner (required) | integer | courier_partner ID of the courier on which you want to track the AWB. List of courier partners: http://track.clickpost.in/courier_partner
account_code (required) | character (100 chars) | account code added in Clickpost dashboard while creating courier partner account

####Optional:

####pickup_info (optional): [pickup location information: all the fields are optional]
Parameter | Type | Description
--------- | ---- | ----------- 
name | character (100 characters) | name of person at pickup location which shall be contacted by courier partner
email | character (100 characters) | email of the person at pickup location
phone_code | character | ISO phone code of the country where the pickup is to be done. Country and their phone codes: https://www.clickpost.in/api/v1/countries/
phone | character (11 characters) | phone number of the person at pickup location
address | character (500 character) | address of pickup location
postal_code | character (50 character) | postal code of the pickup location. For MENA region, this field represents area code
city | character (200 character) | city of the pickup location
district | character (200 character) | district of the pickup location [Required for South East Asian countries]
state | character (200 character) | state of the pickup location
country_code | character | ISO country code of the country where pickup is to be done. Country code list: https://www.clickpost.in/api/v1/countries/
lat | float | latitute of the pickup location
long | float | longitud of the pickup location

####drop_info (optional): [destination location information: all the fields are optional]
Parameter | Type | Description
--------- | ---- | ----------- 
name | character (100 characters) | name of person at destination location who will be contacted by courier partner
email | character (100 characters) | email of the person at destination location
phone_code | character | ISO phone code of the country where the delivery is to be done. Country and their phone codes: https://www.clickpost.in/api/v1/countries/
phone | character (11 characters) | phone number of the person at destination location
address | character (500 character) | address of destination location
postal_code | character (50 character) | postal code of the destination location. For MENA region, this field represents area code
city | character (200 character) | city of the destination location
district | character (200 character) | district of the destination location [Required for South East Asian countries]
state | character (200 character) | state of the destination location
country_code | character | ISO country code of the country where destination is to be done. Country code list: https://www.clickpost.in/api/v1/countries/
lat | float | latitute of the destination location
long | float | longitud of the destination location

####shipment_info (optional): shipment information for rich analytics on your data:
Parameter | Type | Description
--------- | ---- | ----------- 
order_type | string | type of shipment based on payment mode [Possible values: "COD", "PREPAID"] 
invoice_value | float | declared value of the shipment
cod_amount | float | cash on delivery amount, that courier has to collect while delivering the shipment
currency_code | string (3 characters) | ISO currency code of currency selected by customer for placing the order: Currency codes in Clickpost https://www.clickpost.in/api/v1/countries/ [https://en.wikipedia.org/wiki/ISO_4217]
reference_number | string (50 characters) | unique shipment ID for the shipment. (You can perform search on this parameter on Clickpost dashboard)
order_id | string (50 characters) | Order ID of the shipment
length | int | length in cms
height | int | height in cms
breadth | int | breadth in cms
weight | int | weight in grams

Clickpost also accepts item (SKU: Stock Keeping Unit) level information with the shipment information, which enables you to use Clickpost's returns platform. Please pass following attributes of item [SKU]:

Parameter | Type | Description
--------- | ---- | ----------- 
sku | string (50 character) | SKU (Stock Keeping Unit) ID of the item
description | string (500 characters) | SKU description
quantity | int | quantity of SKU ordered by customer
price | float | price of 1 unit
images | string (1000 character) | image URL of the SKU
return_days | int | eligible days for return from the date, shipment was delivered to customer

####additional (optional): extra information about shipment used to power tracking page:
Parameter | Type | Description
--------- | ---- | ----------- 
order_date | character | timestamp when the order was placed in yyyy-mm-dd format
ship_date | character | timestamp when order was ready to ship in yyyy-mm-dd format
min_edd | integer | minimum days commited to the customer for 1st delivery attempt
max_edd | integer | maximum days commited to the customer for 1st delivery attempt
enable_whatsapp | boolean | if you have whatsapp for business account, you can pass opt-in information here so Clickpost starts sending out communications to customers


## Un-Track an Order or Mark a shipment expired

You have to be registered for tracking service to use this api, if you have not, please check Registering for Tracking Service Section.

>POST request. URL:

```
https://www.clickpost.in/api/v1/tracking/awb-unregister/
Headers: {'Content-type': 'application/json'}
```

>__Sample Payload__

```json
{
    "cp_id": 1,
    "waybill": "786000454820",
    "key": "8341db95-a25d-4825-9b83-c62c20284b21"
}

```
>__Response__

```json
{
    "meta": {
        "success": true,
        "status": 200,
        "message": "SUCCESS"
    },
    "result": {
        "awb": "786000454820"
    }
}
```

###Fields Explanation

####Compulsory:

Parameter | Type | Description
--------- | ---- | -----------
key (required) | character | this is the API Key
waybill (required) | character | this is/are comma separated waybill numbers for which the status is required
cp_id (required) | integer | courier_partner_id [List of courier partners is present at:
<a href="http://track.clickpost.in/courier_partner" target="_blank">http://track.clickpost.in/courier_partner</a>]

###Response Explanation:

1. "meta" stores information about the API, success or failure
  - success: true/false, true if the API worked fine, else false
  - message: SUCCESS if everything is fine, else the error message c. status: 200, if the API data was fine, 400 in case of a bad request
2. "result" is an array of records. Each record holds information of comma-separated waybill entered in the request parameter


##Fetch updated-orders list
>__URL__

```
https://api.clickpost.in/api/v1/updated-order?username=<clickpost-username>&key=<clickpost-api-key>&start_date=1531980785&end_date=1531984399

Headers: {'Content-type': 'application/json'}
```

>__Response__

```json
{
    "result": [
        {
            "created_at": "2019-04-15T14:52:45.304018Z",
            "timestamp": "2019-04-15 20:22:43",
            "clickpost_status_description": "OrderPlaced",
            "clickpost_status_code": 1,
            "courier_partner": 9,
            "waybill": "SF41917204SCR",
            "updated_at": "2019-04-15T15:00:04.672388Z",
            "account_code": "test",
            "reference_number": "CP-35416108",
            "status": "001",
            "location": "Mumbai Hub",
            "remark": "Order Manifested in Courier System"
        },
        {
            "created_at": "2019-04-15T14:47:26.614788Z",
            "timestamp": "2019-04-15 20:17:25",
            "clickpost_status_description": "OrderPlaced",
            "clickpost_status_code": 1,
            "courier_partner": 9,
            "waybill": "SF41917199SCR",
            "updated_at": "2019-04-15T15:00:07.132808Z",
            "account_code": "test",
            "reference_number": "CP-35416108",
            "status": "Data Received Successfully",
            "location": "Bangalore Hub",
            "remark": "Order Manifested in Courier System"
        },
        {
            "created_at": "2019-04-15T13:58:34.822899Z",
            "timestamp": "2019-04-15 19:28:33",
            "clickpost_status_description": "OrderPlaced",
            "clickpost_status_code": 1,
            "courier_partner": 9,
            "waybill": "SF41917168SCR",
            "updated_at": "2019-04-15T15:00:42.625536Z",
            "account_code": "test",
            "reference_number": "CP-35416108",
            "status": "001",
            "location": "New Delhi",
            "remark": "Order Manifested in Courier System"
        }
    ],
    "meta": {
        "message": "SUCCESS",
        "status": 200,
        "success": true
    }
}
```

The updated-order API retrieves the shipments which are updated between specified start and end time.

The API is a HTTP GET request to:
`https://api.clickpost.in/api/v1/updated-order` 

[earlier it was `https://www.clickpost.in/api/v1/updated-order`, which will deprecate by Nov 2020]

where output is json

Listed below are the parameters:

Parameter | Type | Description
--------- | ---- | -----------
key (required) | character | this is the API Key
username (required) | character | user name, provided to you
start_date (required) | integer | start time for the query to run. To be passed in epoch time
end_date (required) | integer | end time for the query to run. To be passed in epoch time

Note: The difference between start_date and end_date cannot be more than 30 minutes. If you plan to use polling, Its highly recommended to 1st run updated-order API, get list of updated shipments and then request the status details if required for those shipments using polling.

###Response Explanation:

1. "meta" stores information about the API, success or failure
  - success: true/false, true if the API worked fine, else false
  - message: SUCCESS if everything is fine, else the error message c. status: 200, if the API data was fine, 400 in case of a bad request
2. "result" is an array of records. Each record holds information of comma-separated waybill entered in the request parameter.


##Tracking AWB Using Polling

>__URL__

```
https://api.clickpost.in/api/v2/track-order/?username=testuser&key=2e9b19ac-8e1f- 41ac-a35b-4cd23f41ae17&waybill=3515341&cp_id=10

Headers: {'Content-type': 'application/json'}
```

>__Response__

```json
{
    "meta": {
        "message": "SUCCESS",
        "status": 200,
        "success": true
    },
    "result": {
        "SF18399217NER": {
            "latest_status": {
                "clickpost_status_description": "Delivered",
                "clickpost_status_code": 8,
                "clickpost_status_bucket": 6,
                "status": "Delivered successfully",
                "location": "",
                "remark": "Delivered successfully",
                "timestamp": "2018-07-07 19:34:46"
            },
            "additional": {
                "is_stuck": false,
                "dest_hub_inscan": false,
                "order_detail": [],
                "courier_partner_edd": "2020-03-20",
                "rto_intransit_timestamp": "2020-05-30 20:59:00",
                "ndr": {
                    "ndr_bucket_code": 1,
                    "ndr_description": "Customer unavailable"
                },
                "edd": {
                    "min_sla": 2,
                    "max_sla": 5
                }
            },
            "scans": [
                {
                    "clickpost_status_description": "Delivered",
                    "clickpost_status_code": 8,
                    "clickpost_status_bucket": 6,
                    "status": "Delivered successfully",
                    "location": "",
                    "remark": "Delivered successfully",
                    "tracking_id": 12087859,
                    "timestamp": "2018-07-07 19:34:46",
                    "checkpoint_id": 163921399
                },
                {
                    "clickpost_status_description": "FailedDelivery",
                    "clickpost_status_code": 9,
                    "clickpost_status_bucket": 5,
                    "status": "Delivery attempted: customer not available",
                    "location": "",
                    "remark": "Delivery attempted: customer not available",
                    "tracking_id": 12087879,
                    "timestamp": "2018-07-07 10:53:01",
                    "checkpoint_id": 163496679
                },
                {
                    "clickpost_status_description": "OutForDelivery",
                    "clickpost_status_code": 6,
                    "clickpost_status_bucket": 4,
                    "status": "Out for Delivery",
                    "location": "",
                    "remark": "Out for Delivery",
                    "tracking_id": 12087859,
                    "timestamp": "2018-07-07 08:53:01",
                    "checkpoint_id": 163496669
                },
                {
                    "clickpost_status_description": "InTransit",
                    "clickpost_status_code": 5,
                    "clickpost_status_bucket": 3,
                    "status": "Assigned to a Shadowfax Rider",
                    "location": "",
                    "remark": "Assigned to a Shadowfax Rider",
                    "tracking_id": 12087859,
                    "timestamp": "2018-07-07 08:52:51",
                    "checkpoint_id": 163496670
                },
                {
                    "clickpost_status_description": "InTransit",
                    "clickpost_status_code": 5,
                    "clickpost_status_bucket": 3,
                    "status": "Reached the nearest hub",
                    "location": "",
                    "remark": "Reached the nearest hub",
                    "tracking_id": 12087859,
                    "timestamp": "2018-07-07 08:02:08",
                    "checkpoint_id": 163496671
                },
                {
                    "clickpost_status_description": "OrderPlaced",
                    "clickpost_status_code": 1,
                    "clickpost_status_bucket": 1,
                    "status": "In Manifest",
                    "location": "GUNJAN ",
                    "remark": "In Manifest",
                    "tracking_id": 12087859,
                    "timestamp": "2018-07-07 02:47:21",
                    "checkpoint_id": 163419110
                },
                {
                    "clickpost_status_description": "InTransit",
                    "clickpost_status_code": 5,
                    "clickpost_status_bucket": 3,
                    "status": "Collected by Shadowfax",
                    "location": "GUNJAN ",
                    "remark": "Collected by Shadowfax",
                    "tracking_id": 12087859,
                    "timestamp": "2018-07-07 02:25:34",
                    "checkpoint_id": 163419111
                },
                {
                    "clickpost_status_description": "OrderPlaced",
                    "clickpost_status_code": 1,
                    "clickpost_status_bucket": 1,
                    "status": "Assigned to Shadowfax",
                    "location": "",
                    "remark": "Assigned to Shadowfax",
                    "tracking_id": 12087859,
                    "timestamp": "2018-07-06 05:41:13",
                    "checkpoint_id": 162947643
                }
            ],
            "valid": true
        }
    }
}
```

The track-order API retrieves the historic statuses and the current status of the package.

The API is a HTTP GET request to:
`https://api.clickpost.in/api/v2/track-order/` 

[earlier it was `https://www.clickpost.in/api/v2/track-order/`, which will deprecate by Nov 2020]

where output is json

Listed below are the parameters:

Parameter | Type | Description
--------- | ---- | -----------
key (required) | character | this is the API Key
username (required) | character | user name, provided to you
waybill (required) | character | this is/are comma separated waybill numbers for which the status is required
cp_id (required) | integer | courier_partner_id as specified on page 1 of this documentation

Note: You can query upto 15 waybills [AWBs] status in 1 API request

###Response Explanation:

1. "meta" stores information about the API, success or failure
  - success: true/false, true if the API worked fine, else false
  - message: SUCCESS if everything is fine, else the error message c. status: 200, if the API data was fine, 400 in case of a bad request
2. "result" is an array of records. Each record holds information of comma-separated waybill entered in the request parameter.
3. Each record has following objects:
  - "valid": (true / false) in case a wrong AWB / AWB which is not yet registered on Clickpost; is entered to track a shipment, “valid” field will be false. If the AWB is correct, “valid” will be true
  - "waybill": AWB provided in the API. Is the key of each object. The value is a dictionary storing information about shipment:
        1. scans: Stores all scans that happened for shipment. Has following keys:
            + status: status of the shipment at that time
            + remarks: remark given by courier partner
        3. location: location of shipment at the time of the scan
        4. timestamp: date/time in ISO format when the scan was done
        5. clickpost_status_code: clickpost generated status code for particular
        status. Clickpost has mapped various statuses of different courier companies into few status codes, which helps customers understand and take action on statuses in preemptive manner. (Explained on last page of this document)
        6. clickpost_status_description: description of clickpost_status_code (Specified on last page of this document)
  - "additional": gives additional information about the shipment:
        1. courier_partner_edd: Expected delivery date as given by courier partner over APIs
        2. rto_intransit_timestamp: timestamp of 1st RTO Intransit scan received by Clickpost systems from courier partner
  - "latest_status": Stores information about the latest status of shipment, has following fields:
        1. status: status of the shipment at that time
        2. remarks: remark given by courier partner
        3. location: location of shipment at the time of the scan
        4. timestamp: date/time in ISO format when the scan was done
        5. clickpost_status_code: clickpost generated status code for particular
        status. Clickpost has mapped various statuses of different courier companies into few status codes, which helps customers understand and take action on statuses in preemptive manner (Explained on last page of this document)
        6. clickpost_status_description: description of clickpost_status_code (Specified on last page of this document)
        7. clickpost_status_bucket: this is a consolidated id built on top of clickpost_status_codes, that can be used to show status to the customer on your track orders page. It has following distinct values:

clickpost_status_bucket | Meaning | clickpost_status_code clubbed in the bucket
--------- | ---- | -----------
1 | Order Placed by Customer | [1, 2, 3, 28, 25, 10]
2 | Dispatched | [4]
3 | In Transit | [5, 18, 19, 20]
4 | Out For Delivery | [6]
5 | Failed Delivery | [7, 9]
6 | Delivered | [8] 
7 | Returned: When shipment is in return journey due to customer rejection | [11, 12, 13, 14, 15, 21, 26, 27]
8 | Lost | [16]
9 | Damaged | [17]


6, 7, 8: These are terminal buckets in shipment journey


##Tracking AWB Using Webhooks


###Clickpost exposes webhooks for status updates in 2 ways:

1. For all events/status: This will trigger status updates for all the scans done by courier partner for the shipment. You can opt in for these webhooks using "Webhooks: All Status" on the dashboard. From tech perspective, apply check on clickpost_status_code in latest_status to update the status in your system.

2. For selected events/status: This will trigger status updates only for selected checkpoints opted by you on the Clickpost dashboard. You can opt in for these webhooks using "Webhooks: Selected Status" on the dashboard. From tech perspective, apply check on notification_event_id in the webhook object to update the status in your system. The checkpoints available for Selected webhooks are as mentioned on the dashboard.


>__Webhook Payload Header__

```json
{
  "Content-Type": "application/json",
  "webhook_key": "webhook_key_given_during_webhooks_register"
}
```

>__Webhook Payload__

```json

{
    "additional": {
        "latest_status": {
            "remark": "Shipment is Out for Delivery",
            "clickpost_status_code": 6,
            "reference_number": "WERA-9616974",
            "timestamp": "2019-05-06T10:04:20Z",
            "clickpost_status_bucket_description": "Out for delivery",
            "location": "DEL_GeetaColony",
            "clickpost_status_description": "OutForDelivery",
            "clickpost_status_bucket": 4,
            "status": "OFD"
        },
        "is_rvp": false,
        "courier_partner_edd": "2020-03-25",
        "order_id":"ABC123",
    },
    "remark": "Shipment is Out for Delivery",
    "clickpost_status_description": "OutForDelivery",
    "timestamp": "2019-05-06T10:04:20Z",
    "location": "DEL_GeetaColony",
    "status": "OFD",
    "cp_id": 9,
    "clickpost_status_code": 6,
    "waybill": "SF49245NER"
}
```

>__NDR(Non delivery report) details in Webhook, send when the status_code = 9 (Failed Delivery)__

```json
{
  "status": "When forward shipment is not accepted by end customer",
  "remark": "Failed Delivery",
  "waybill": "XYZABC",
  "location": "Bengaluru_Koramangala_Dc (Karnataka)",
  "timestamp": "2016-07-12T17:12:36Z",
  "clickpost_status_code": 9,
  "clickpost_status_description": "FailedDelivery",
  "cp_id": 1,

  "additional": {
    "latest_status": {
      "reference_number": "WERA-9616974",
      "clickpost_status_code": 9,
      "location": "Bengaluru_Koramangala_Dc (Karnataka)",
      "status": "When forward shipment is not accepted by end customer",
      "clickpost_status_description": "FailedDelivery",
      "timestamp": "2016-07-12T17:12:36Z",
      "remark": "Failed Delivery"
    },
    "ndr_status_code": 1,
    "ndr_status_description": "Customer Unavailable",
    "is_rvp": false,
    "courier_partner_edd": null
  }
}
```

###Activating Webhooks:

1. Visit Clickpost dashboard: *Settings* Tab on the left and Click notification section
2. Select webhooks and activate Selected Events webhooks configuration or All Events Webhooks configuration as per your need.
3. Selected webhooks configuration: trigger webhooks only when shipment reaches certain checkpoints in its journey.
4. All webhooks configuration: trigger webhooks for all shipment statuses as they come.

We generally recommend customers to use selected webhooks configuration as all webhooks will trigger too many status messages on your system.

####Note:
If you wish to configure the basic token auth also along with the webhooks the headers will change as reflected on the right:

>__Headers with basic token auth__

```json
{
  "Content-Type": "application/json",
  "Authorization": "<value entered on the dashboard for the token under basic token auth section>"
}
```


###Important Notes and special data in Webhooks (Examples are present on the right):

1. Webhooks do not guarantee the order of data send to Client servers. 
latest_status indicates the latest status for the shipment at the time when the webhook is sent. This is sent with all webhooks
2. In case of Failed Delivery, Clickpost unified NDR status code and NDR status description is sent in additional
3. Please make your API end point idempotent
4. Since webhooks are transactional in nature, To insure minimal API data loss, we have retries in place if we do not get http 200 response from your server
5. If you opt for selected events webhook notification, in case clickpost receives multiple notification from courier partner at the same time, only the latest notification will be sent to you
6. While consuming the webhooks do not apply strict JSON check in the code as you might have new keys in the payload as we enhance the services.


###Webhook data POST on Client Server for all events:

Every time courier partner updates tracking of the shipment, We will post data to your server using the url you registered while registering for webhooks.

###Payload Explanation:

1. waybill: AWB number for which data is posted.
2. status: status of the shipment at that time
3. remarks: remark given by courier partner
4. location: location of shipment at the time of the scan
5. timestamp: date/time in IST format when the scan was done
6. clickpost_status_code: clickpost status code for particular status. Clickpost has mapped various statuses of different courier companies into few status codes, which helps customers understand and take action on statuses in preemptive manner. [Visit "Tracking Status Codes" section]
7. clickpost_status_description: description of clickpost_status_code [Visit "Tracking Status Codes" section]
8. courier_partner_edd: Expected delivery date as given by courier partner over APIs

###NDR Status Codes

ndr_status_code | ndr_status_description
--------------|------------------------
0 | "Unknown Exception"
1 | "Customer Unavailable"
2 | "Rejected by Customer"
3 | "Delivery Rescheduled"
4 | "No Attempt"
5 | "Customer Unreachable"
6 | "Address Issue"
7 | "Payment Issue"
8 | "Out Of Delivery Area"
9 | "Order Already Cancelled"
10| "Self Collect"
11| "Shipment Seized By Customer"
12| "Customer wants open delivery"
13| "Shipment Misrouted by logistics partner"

---

###Webhook data POST on Client Server for selected events:

>__Selected event subscribed webhook: Failed delivery Payload__

```json

{
  "waybill": "2614010163240",
  "remark": "Customer escalation received",
  "clickpost_status_code": 9,
  "status": "Pending",
  "clickpost_status_description": "FailedDelivery",
  "location": "Lucknow_Aliganj (Uttar Pradesh)",
  "timestamp": "2019-05-01T00:55:06Z",
  "cp_id": 4,
  "additional": {
    
    "ndr_status_code": 1,
    "ndr_status_description": "Customer unavailable",

    "notification_event_id": 4,

    "is_rvp": false,
    "courier_partner_edd": "2020-03-25",
    "order_id":"ABC123",

    "latest_status": {
      "reference_number": "WERA-NMS1908MSO2",
      "remark": "Customer escalation received",
      "clickpost_status_code": 9,
      "status": "Pending",
      "location": "Lucknow_Aliganj (Uttar Pradesh)",
      "clickpost_status_bucket_description": "Failed delivery",
      "clickpost_status_description": "FailedDelivery",
      "timestamp": "2019-05-01T00:55:06Z",
      "clickpost_status_bucket": 5
    }
  }
}

```
>__Selected event subscribed webhook: Delivered Payload__

```json
{
    "status": "Delivered",
    "clickpost_status_code": 8,
    "waybill": "12527345",
    "clickpost_status_description": "Delivered",
    "location": "Nayagarh_Durgprsd_D (Orissa)",
    "cp_id": 4,
    "remark": "Delivered to consignee",
    "timestamp": "2019-05-06T15:01:00Z",

    "additional": {

        "notification_event_id": 5,
        "is_rvp": false,
        "courier_partner_edd": "2020-03-25",
        "order_id":"ABC123",

        "latest_status": {
            "status": "Delivered",
            "reference_number": "WERA-NMS1908MSO2",
            "clickpost_status_bucket_description": "Delivered",
            "clickpost_status_description": "Delivered",
            "clickpost_status_code": 8,
            "location": "Nayagarh_Durgprsd_D (Orissa)",
            "clickpost_status_bucket": 6,
            "remark": "Delivered to consignee",
            "timestamp": "2019-05-06T15:01:00Z"
        }

    }
}

```

In case customer wants to recieve notifications only for certain events, Clickpost provides funtionality for the same.

If customer opts for this service, we add: "notification_event_id" key in additional object of the payload. This will inform you the current status of shipment.

####Possible values:

Value | Description
--------- | -----------
1 | Out For Pickup
2 | Shipped
3 | Out For Delivery
4 | Failed Delivery
5 | Delivered
6 | RTO
10 | Order Cancelled
12 | RTO-Delivered
14 | Exchange Pickup
15 | Exchange Delivered
16 | Pickup Cancelled
17 | Shipment Stuck
18 | SLA breached
19 | Lost
20 | Damaged

Following notification_event_id are useful for customers using Clickpost's managed returns service which accepts return requests from end user:

Value | Description
--------- | -----------
9 | AWB Generated: As soon as an AWB is generated in Clickpost for a return request
11 | Return Request placed: As soon as a return request is placed by the end user using Clickpost's return UI


###NDR Status Codes

ndr_status_code | ndr_status_description
--------------|------------------------
0 | "Unknown Exception"
1 | "Customer Unavailable"
2 | "Rejected by Customer"
3 | "Delivery Rescheduled"
4 | "No Attempt"
5 | "Customer Unreachable"
6 | "Address Issue"
7 | "Payment Issue"
8 | "Out Of Delivery Area"
9 | "Order Already Cancelled"
10| "Self Collect"
11| "Shipment Seized By Customer"
12| "Customer wants open delivery"
13| "Shipment Misrouted by logistics partner"

Please see the sample payload on the right.


*Clickpost recommends that the mapping of NDR be done strictly on ndr_status_code and not on ndr_status_description.*


------


## Return Order Placed Webhook

>__Webhook Payload Header__

```json
{
  "Content-Type": "application/json",
  "webhook_key": "webhook_key_given_during_webhooks_registeration"
}
```

>__Webhook Payload__

```json

{
        "location": "",
        "remark": "Return Order Placed",
        "notification_event": 11,
        "timestamp": "2019-04-29 07:47:07.161221",
        "clickpost_status_code": 101,
        "cp_id": -1,
        "clickpost_status_bucket_description": "Return Order Placed",
        "waybill": "",
        "clickpost_status_bucket": 8,
        "status": "Return Order Placed",
        "clickpost_status_description": "Return Order Placed",
        "additional": {
            "latest_status": {
                "clickpost_status_bucket_description": "Return Order Placed",
                "clickpost_status_description": "Return Order Placed",
                "clickpost_status_bucket": 8,
                "remark": "Return Order Placed",
                "status": "Return Order Placed",
                "location": "",
                "timestamp": "2019-04-29 07:47:07.161252",
                "clickpost_status_code": 101
            },
            "is_rvp": true,
            "notification_event_id": 11,
            "forward_awb": "5522110373319",
            "self_shipped": false,
            "forward_reference_number": "1405277",
            "item_info": [{
              "sku": "120667",
              "quantity": 1
          }, {
              "sku": "9649",
              "quantity": 1
          }, {
              "sku": "46457",
              "quantity": 1
          }, {
              "sku": "10924",
              "quantity": 1
          }],
        }
    }
```

This webhook is only useful for customers using Clickpost's managed returns platform to accept customer returns on their website.

###Activating Return order placed webhook:

1. Visit Clickpost dashboard: *Settings* Tab on the right and Click notification section
2. Select webhooks and activate Selected webhooks configuration --> "Return Order Placed". 

###Payload Explanation:

1. waybill: AWB number for which data is posted (Will be blank for return order placed).
2. status: status of the shipment at that time
3. remarks: remark given by courier partner
4. location: location of shipment at the time of the scan
5. timestamp: date/time in IST format when the scan was done
6. clickpost_status_code: clickpost generated status code for particular status. Clickpost has mapped various statuses of different courier companies into few status codes, which helps customers understand and take action on statuses in preemptive manner.
7. clickpost_status_description: description of clickpost_status_code
8. is_rvp inside additional object tells the payload is for reverse orders. 
9. forward_awb field contain the forward awb number for which return order has been placed 
10. forward_reference_number will have the corresponding reference number.
12. waybill number will be blank as order is not yet created on courier partner (not manifested yet) 
13. clickpost_status_code will have 101 value which is Return Order Placed.
14. self_shipped: Either True or False depending upon how the return shipment is shipped, if shipped by customer, then self_shipped is True else False.
15. item_info: represents the item details for which return request is raised by the customer

---

Logic to be applied on webhook endpoint to detect returns webhook: In all reverse pickup order webhooks, is_rvp will be true. If its true, check the forward_awb or forward_reference_number in the payload, verify it with the same in your system and update the sku(s) present in item_info.

------