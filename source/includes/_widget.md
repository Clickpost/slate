# Tracking Page / Widget

###To integrate with your website:

1. Place widget script in your webpage.
2. Place widget HTML code in your webpage.

Note: It's better to move widget script to as low in the web page as possible.


Tracking Page / Widget is designed to provide exhaustive tracking to end user. 

The widget/page has following features:

1. End to end shipment tracking. Incase you want the tracking page to show Order Placed and Ready to Ship milestone as well, please pass order_date and ship_date in AWB-register API.
2. Failed delivery feedback from customer: During a failed delivery by courier partner, customer can enter his input/concern over a form which will be shared with you as a report daily or same can be fetched via API (Customer Feedback API)
3. In case you want customer to request a delivery preference any time before an attempt for delivery is made, please contact our team to enable the feature. Feedback of the same will be available as for point 2.
4. Design language of the page is customisable as per your website theme. Our team can help you in designing the page.

JS to be included:

`<script type="text/javascript" src="http://track.clickpost.in/clickpost-widget-1.0.3.js"></script>`


##Tracking widget using AWB number and Courier Partner ID

###Fields Explanation:

Parameter | Type | Description
--------- | ---- | -----------
id | string | Your Waybill number
data-cpId | string | Your Courier Partner Id


`<div id="1234567890" class="tracking-widget" data-cpId="11"></div>`


##Tracking widget using Reference Number (Order ID)

###Fields Explanation:

Parameter | Type | Description
--------- | ---- | -----------
id | string | Your order reference number
data-username | string | username provided to you
data-key | string | API Key provided to you

`<div id="1234567890" class="tracking-widget" data-key="123-456-7890" data-username="xyz"></div>`


Note: No need to add more than one script for multiple tracking widgets in a page.