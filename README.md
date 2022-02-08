# FlowerShop JavaScript API

## Add FlowerShop Media JavaScript API to Your Website

Similar to adding a Google Analytics tracking code or a Facebook pixel, the first step to using the FSM Tracking API is to add your unique tracking code to the website you want to track. It is easy and takes only a few minutes. You only need to add the code once and there is no need to update it for future versions.

The FlowerShop Media JavaScript API was designed to not affect your site or its performance in any way, including your site's loading time. The process remains the same regardless of which platform your site is built with. The FlowerShop Media JavaScript API is compatible with all platforms including React.js, Angular.js, Vue.js, and HTML with Vanilla JavaScript.

Simply paste the code that the FSM team has provided you with inside the `<head>` tag in any HTML pages you wish to track.

```html
<!--- Your Page Script -->
<!DOCTYPE html>
<html>
<head>
	...
	<meta charset="UTF-8">
	
	<!-- FlowerShop Media Tags -->
	<script>
	(function(t,r,a,c,k){t[k]=t['']=t['']||(function(){
	s=r.createElement(a);s.async=s.defer=!0;
	s.src='https://tracking.flowershop.media/tags/'+c;
	h=r.querySelector(a);h.parentNode.insertBefore(s,h);
	return function(){(t[''].q=t[''].q||[]).push(arguments);}})()
	})(window,document,'script','XXXXXXXXXXXXXXXXXX','_fsm');
	</script>
	<!-- End of FlowerShop Media Tags -->
	
	<!-- Followed by your CSS/JavaScript files-->
	<script src="your-page-script.js"></script>
	...
</head>
...
</html>
```
Once the code is added, you can use the `_fsm`  global JavaScript function to send conversions to FlowerShop Media.

## Track Purchases

Purchase tracking sends FlowerShop Media information about a purchase made within the website. 
```javascript
// Tracks the purchase event in Oribi
_fsm('purchase', purchaseDetails);
```

###  Anatomy of the `purchaseDetails` JavaScript object
| Field                    | Type   | Required | Description                                                                                                                                                                                                                                                                                                                |   |
|--------------------------|--------|----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---|
| `totalPrice`             | Number | REQUIRED | The total amount the customer paid (after shipping, tax, discounts, etc). It can contain a fraction (e.g. a value of 1.5 can describe a price of $1.5)                                                                                                                                                                     |   |
| `currency`               | String | OPTIONAL | A three letter ISO-4217 currency code of the currency the prices are in (case insensitive). If provided, it must be in one of our supported currencies (see below), from which it will be converted to the currency you chose in FSM. If omitted, the store currency you set in FSM will be used.                          |   |
| `orderId`                | String | OPTIONAL | An order identifier that will be shown in FSM in the future to help you recognize specific purchases and will be used to make sure you don’t count the same purchase multiple times. If you send multiple purchases with the same (non-null) orderId, Oribi will only count the first purchase and ignore subsequent ones. |   |
| `taxPrice`               | Number | OPTIONAL | The tax paid for the purchase (in the same currency as the total price). (Default: 0)                                                                                                                                                                                                                                      |   |
| `shippingPrice`          | Number | OPTIONAL | The additional price paid for the shipping of the purchased items (in the same currency as the total price). (Default: 0)                                                                                                                                                                                                  |   |
| `discountPrice`          | Number | OPTIONAL | The discount for the purchase, if exists (in the same currency as the total price). (Default: 0)                                                                                                                                                                                                                           |   |
| `products`               | Array  | OPTIONAL | The list of products purchased (see details below)                                                                                                                                                                                                                                                                         |   |
| `products.name`          | String | OPTIONAL | The name of the product. Will be used in the future to search or filter purchases.                                                                                                                                                                                                                                         |   |
| `products.id`            | String | OPTIONAL | The String identifier of the product.                                                                                                                                                                                                                                                                                      |   |
| `products.price`         | Number | OPTIONAL | The price for a single unit of the product.                                                                                                                                                                                                                                                                                |   |
| `products.discountPrice` | Number | OPTIONAL | The discount on specific product.                                                                                                                                                                                                                                                                                          |   |
| `products.taxPrice`      | Number | OPTIONAL | The tax price on specific product.                                                                                                                                                                                                                                                                                         |   |
| `products.quantity`      | Number | OPTIONAL | The amount of the product bought in this purchase. (Default: 1)                                                                                                                                                                                                                                                            |   |
| `products.categories`    | Array  | OPTIONAL | An array of string categories. Will be used in the future to search and filter purchases.                                                                                                                                                                                                                                  |   |

