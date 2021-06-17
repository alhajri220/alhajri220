- 👋 Hi, I’m @alhajri220
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
alhajri220/alhajri220 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->











API DOCUMENTS







 
Shipment Tracking API

Table of Contents


S. N	Topic	Page
1	Introduction to API	
2	AWB Tracking API (Track Shipments)	
3	Handling Errors	
4	Questions & Answers	


 

1.	Introduction to API


The API is provided to the clients so that they can handle their job in a no fuss manner and work faster as well as add the shipment easily and directly. This not only reduces the efforts of the Customer but also helps the Ejack by reducing the pain of constant updating and requirement of a staff dedicated to this particular task.
Ejack will be responsible for providing the Customer with authentication credentials in terms of username as well as password, so that the authorized person can access the system.
This manual will help and guide you through the process of using API and also you will find help with issue concerning exceptions and error handling.
 
2.	AWB Number Tracking API (Track Shipments) 

This API guide will be used for tracking shipment using AWB’s on Ejack System to collect shipment data values for clients.
Test AWB_NO (E8419861002) to get the shipment details

API Details:
URL:  https://ejack.fastcoo-solutions.com/lm/shipmentBookingApi_lm.php

Example:
https://ejack.fastcoo-solutions.com/lm/shipmentBookingApi_lm.php?awb_no=E5444665412

Table 1. API Details

Parameter	Type	Description	Mandatory	Error Code
awb_no	Varchar (20)	AWB Number is shipment unique number	Yes	136,138




















Table 2. Response

{
"shipment_data":{ "awb_no":"E8419861002", "entry_date":"2018-04-18 13:41:55",
"payment_method":"COD", "weight":"2",
"status":"Booked", "product_type":"PARCEL", "code":"B", "service_name":"Express Service", "origin":"Quweya ", "destination":"Quweya "
},
"sender_info":{ "name":"mandeep", "mobile":"5656565656",
"address":"test"
},
"receiver_info":{ "name":"ytry", "mobile":"9876543210",
"address":"yryrhf"
},
"travel_history":[
{
"new_location":"Quweya ", "new_status":"Booked", "Activites":"Booked", "code":"B",
"comment":"",
"entry_date":"2018-04-18 13:41:55"
}
]
}


Errors Response:
For invalid-	
{"status":138,"awb_no":"awb_no is invalid."}
For empty-	
{"status":"136","message":"AWB No is required."}


3.	Handling Errors

•	If AWB number is blank you will get this message (AWB number is required, code: 136)
•	If AWB number is wrong you will get this message (AWB number is invalid, code: 138)
 
4.	Questions & Answers


Question 1: When we call Ejack track shipment API, the response that we receive has shipment_data and travel_history object. What are those?
Answer: shipment_data shows shipment details such as awb_no, entry_date which is the date on which the shipment was generated, payment_method which tells about the mode of payment (either COD or CC), weight of the shipment, status of the shipment, product_type i.e. Parcel, service_name which selects services from the above list as well as destination and origin. While travel_history shows events that occur with shipment as it proceeds. new_location and new_status is updated every time it arrives at a new destination and Activities shows the status changes.
Example:
i.e., travel_history is record of events happened with shipment with respect to status. It has new_status instead of status field but the purpose is same to show status where entry_date shows date and time when status is changed.

Question 2: What about testing environment to check API integration. Can you provide it?
Answer: No, we don't have testing environment. But yes you can check API integration using test account on live environment. You can request for a test account via mail.
Example:
i.e., using this test account you can create test shipments to confirm your API integration.

Question 3: What is productType?
Answer: productType is to define types of products i.e., whether it is Parcel or Document, etc.
"KVAIMI" is the code for productType. Just pass this word.
Example: 
"productType": "KVAIMI"

Question 4: Unit of Weight is Kg?
Answer: Yes
Example:
"weight": "20Kg"

Question 5: What about my production/Actual Account?
Answers: Your Account Manager will sort this issue for you.

Question 6: After calling Ejack Add Shipment API what will we receive?
Answer: You will receive AWB No. and URL to print the label so that you can get .pdf file.
Example:
{"awb":"E6865173565","awb_print_url":"https:\/\/ejack.fastcoo-solutions.com\/lm\/p\/oXlWC_p_G_p_RQ0K6R87UXuWJg_e__e_"}
Copy and paste this link in browser to check example AWB label.

Question 7: What is refrence_id? Will it print on AWB (Airway bill) label?
Answer: reference_id is equivalent of AWB number of our system. The API doesn’t generate this number. Instead your client will provide you with this number. And yes, I will be printed on the AWB Label.
Example:
The unique bar code with corresponding to the unique Reference Id is displayed on the AWB print Label.

Question 8: What is COD value and what is product_price? What is the difference?
Answer: COD stands for Cash On Delivery, this value should be collected from customer. If Booking Mode is COD (Cash On Delivery) you have put value in Cod Value parameter. If Booking Mode is CC (Cash Collected) then you have to put 0 in Cod Value parameter.
While product_price is actual price of the product.

Question 9: What about currency? It should be SAR?
Answer: Yes
Example:
"Currency" : "SAR"


Question 10: What is POD? It means delivered?
Answer: Yes, its stands for Proof Of Delivery.
Example:
If you track Shipment using Ejack API you should notice "travel_history" Object. In it when new_status code is POD it means it’s delivered and it always comes first. But when new_status is POD and code is closed it means COD value is received from customer it always comes second.

Question 11: What and where is cities_list? What is it for?
Answer: While calling Add shipment API in sender/receiver city you have to mention city from our cities_list. Otherwise shipment can't be added in our system.
Example:
Suppose for Jeddah try selecting it from the list.

Question 12: In AWB print Product price is not shown. Why?
Answer: If your Booking Mode is CC then in AWB label product price will be shown, if not contact with us via email we will add it for you only. In case of Booking Mode COD only COD price will be shown on AWB label.


