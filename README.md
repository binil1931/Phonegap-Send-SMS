Phonegap: InAppBilling 
===================================
Steps
-----
- Add the Plugin to the cordova app
```
cordova plugin add com.smartmobilesoftware.inappbilling --variable BILLING_KEY="< BILLING_KEY >"
```
Automatic Generate
-------------------
-in config.xml 
```
 <feature name="InAppBillingPlugin">
        <param name="android-package" value="com.smartmobilesoftware.inappbilling.InAppBillingPlugin" />
  </feature>
 ``` 
-in AndroidManifest.xml  
``` 
    <uses-permission android:name="com.android.vending.BILLING" />
```
Manual
-----
- if the native code is not generateing by Automatic then add the package from the given code
```
com.android.vending.billing
```
com.smartmobilesoftware.inappbilling
```
com.smartmobilesoftware.util
```

JavaScript
-----------
- Add inappbilling.js from the given source code

Full example
----------------
```html
<html>
<head>
<script type="text/javascript" charset="utf-8">
            function successHandler (result) {
                var strResult = "";
                if(typeof result === 'object') {
                    strResult = JSON.stringify(result);
                } else {
                    strResult = result;
                }
                alert("SUCCESS: \r\n"+strResult );
            }

            function errorHandler (error) {
                alert("ERROR: \r\n"+error );
            }

            // Click on init button
            function init(){
                // Initialize the billing plugin
                inappbilling.init(successHandler, errorHandler, {showLog:true});
            }

            // Click on purchase button
            function buy(){
                // make the purchase
                inappbilling.buy(successHandler, errorHandler,"gas");

            }

            // Click on ownedProducts button
            function ownedProducts(){
                // Initialize the billing plugin
                inappbilling.getPurchases(successHandler, errorHandler);

            }

            // Click on Consume purchase button
            function consumePurchase(){

                inappbilling.consumePurchase(successHandler, errorHandler, "gas");
            }

            // Click on subscribe button
            function subscribe(){
                // make the purchase
                inappbilling.subscribe(successHandler, errorHandler,"infinite_gas");

            }

            // Click on Query Details button
            function getDetails(){
                // Query the store for the product details
                inappbilling.getProductDetails(successHandler, errorHandler, ["gas","infinite_gas"]);

            }

            // Click on Get Available Products button
            function getAvailable(){
                // Get the products available for purchase.
                inappbilling.getAvailableProducts(successHandler, errorHandler);

            }                       

        </script>
</head>

    <body>
        <h1>Hello World</h1>
        <button onclick="init();">Initalize the billing plugin</button>
        <button onclick="buy();">Purchase</button>
        <button onclick="ownedProducts();">Owned products</button>
        <button onclick="consumePurchase();">Consume purchase</button>
        <button onclick="subscribe();">Subscribe</button>
        <button onclick="getDetails();">Query Details</button>
        <button onclick="getAvailable();">Get Available Products</button>

	<script type="text/javascript" src="cordova.js"></script>
	<script type="text/javascript" src="js/index.js"></script>
</body>
 </html>
```

Suuces
-------

* success : The success callback. It provides a json object representing the purchased item as first parameter. Example :

{"orderId":"12999763169054705758.1385463868367493",
"packageName":"com.example.myPackage",
"productId":"example_subscription",
"purchaseTime":1397590291362,
"purchaseState":0,
"purchaseToken":"ndglbpnjmbfccnaocnppjjfa.AO-J1Ozv857LtAk32HbtVNaK5BVnDm9sMyHFJkl-R_hJ7dCSVTazsnPGgnwNOajDm-Q3DvKEXLRWQXvucyW2rrEvAGr3wiG3KnMayn5yprqYCkMNhFl4KgZWt-4-b4Gr29_Lq8kcfKCkI57t5rUmFzTdj5fAdvX5KQ",
"receipt": "{...}",
"signature": "qs54SGHgjGSJHSKJHIU"}  