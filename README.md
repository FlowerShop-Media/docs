# FlowerShop Media JavaScript Tracking API

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

## Tracking Conversions
Once the code is added, you can use the `_fsm`  global JavaScript function to send conversions to FlowerShop Media.

```javascript
_fsm(event, payload);
```

**Parameters:**

`event` – Name of event. Required. Must be a `String`.

`payload` – Optional data associated with event. Technically, this can be any type of JavaScript value that can be serialized using the `JSON.stringify()` function. However, a plain object is strongly recommended due to its expressiveness. If a payload is not serializable into JSON, it will be ignored (because the `JSON.stringify()` function returns an `undefined`).

This function can be used to send any type of events you wish to track. For tracking page views and purchases, please take a look at the following sections.

### Tracking Page Landings

```javascript
_fsm('landing');
```
### Tracking Purchases

Purchase tracking sends FlowerShop Media information about a purchase made within the website. 
```javascript
_fsm('purchase', purchaseDetails);
```

####  Specification of the `purchaseDetails` JavaScript object
|        **Field**       | **Type** | **Required** |                                                                                                                                                       **Description**                                                                                                                                                      |
|----------------------|-------|------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `totalPrice`             | Number   | YES          | The total amount the customer paid (after shipping, tax, discounts, etc). It can contain a fraction (e.g. a value of 1.5 can describe a price of $1.5)|
| `currency`               | String   | NO           | A three letter ISO-4217 currency code of the currency the prices are in (case insensitive). If provided, it must be in one of our supported currencies (see below), from which it will be converted to the currency you chose in FSM. If omitted, the store currency you set in FSM will be used.|
| `userId`                 | String   | NO           | The identifier of the user that places the order.|
| `storeId`                | String   | NO           | The identifier of the store where the order is placed.|
| `orderId`                | String   | NO           | An order identifier that will be shown in FSM in the future to help you recognize specific purchases and will be used to make sure you don’t count the same purchase multiple times. If you send multiple purchases with the same (non-null) orderId, FSM will only count the first purchase and ignore subsequent ones. |
| `taxPrice`               | Number   | NO           | The tax paid for the purchase (in the same currency as the total price). (Default: 0)|
| `shippingPrice`          | Number   | NO           | The additional price paid for the shipping of the purchased items (in the same currency as the total price). (Default: 0)|
| `discountPrice`          | Number   | NO           | The discount for the purchase, if exists (in the same currency as the total price). (Default: 0)|
| `customField`            | Any      | NO           | Any extra field that need to be added to the purchase|
| `products`               | Array    | NO           | The list of products purchased (see details below)|
| `products.name`          | String   | NO           | The name of the product. Will be used in the future to search or filter purchases.|
| `products.id`            | String   | NO           | The String identifier of the product.|
| `products.price`         | Number   | NO           | The price for a single unit of the product.|
| `products.discountPrice` | Number   | NO           | The discount on specific product.|
| `products.taxPrice`      | Number   | NO           | The tax price on specific product.|
| `products.quantity`      | Number   | NO           | The amount of the product bought in this purchase. (Default: 1)|
| `products.categories`    | Array    | NO           | An array of string categories. Will be used in the future to search and filter purchases.|
| `products.customField`   | Any      | NO           | Any extra fields that need to be added per product. |

#### Example

```javascript
_fsm('purchase', {
    totalPrice: 90.58,
    userId: '41e3788a-8f73-11ec-b909-0242ac120002',
    storeId: 592,
    taxPrice: 10.50,
    products: [
        {
	    name: 'Jenny\'s Flower',
	    price: 19.99,
	    id: 502,
	    quantity: 2,
	    categories: ['edible', 'recreational']
	},
	
	{
	    name: 'Pep-O-Chem Stay Prerolls',
	    price: 40.10,
	    id: 503,
	    quantity: 1,
	    categories: ['fluffy', 'preroll', 'medical']
	},
    ]
});
```


#### Supported Currencies
|CODE | CURRENCY                               |
|-----|----------------------------------------|
| AED | United Arab Emirates Dirham            |
| AFN | Afghan Afghani                         |
| ALL | Albanian Lek                           |
| AMD | Armenian Dram                          |
| ANG | Netherlands Antillean Guilder          |
| AOA | Angolan Kwanza                         |
| ARS | Argentine Peso                         |
| AUD | Australian Dollar                      |
| AWG | Aruban Florin                          |
| AZN | Azerbaijani Manat                      |
| BAM | Bosnia-Herzegovina Convertible Mark    |
| BBD | Barbadian Dollar                       |
| BDT | Bangladeshi Taka                       |
| BGN | Bulgarian Lev                          |
| BHD | Bahraini Dinar                         |
| BIF | Burundian Franc                        |
| BMD | Bermudan Dollar                        |
| BND | Brunei Dollar                          |
| BOB | Bolivian Boliviano                     |
| BRL | Brazilian Real                         |
| BSD | Bahamian Dollar                        |
| BTC | Bitcoin                                |
| BTN | Bhutanese Ngultrum                     |
| BWP | Botswanan Pula                         |
| BYN | Belarusian Ruble                       |
| BZD | Belize Dollar                          |
| CAD | Canadian Dollar                        |
| CDF | Congolese Franc                        |
| CHF | Swiss Franc                            |
| CLF | Chilean Unit of Account (UF)           |
| CLP | Chilean Peso                           |
| CNH | Chinese Yuan (Offshore)                |
| CNY | Chinese Yuan                           |
| COP | Colombian Peso                         |
| CRC | Costa Rican Colón                      |
| CUC | Cuban Convertible Peso                 |
| CUP | Cuban Peso                             |
| CVE | Cape Verdean Escudo                    |
| CZK | Czech Republic Koruna                  |
| DJF | Djiboutian Franc                       |
| DKK | Danish Krone                           |
| DOP | Dominican Peso                         |
| DZD | Algerian Dinar                         |
| EGP | Egyptian Pound                         |
| ERN | Eritrean Nakfa                         |
| ETB | Ethiopian Birr                         |
| EUR | Euro                                   |
| FJD | Fijian Dollar                          |
| FKP | Falkland Islands Pound                 |
| GBP | British Pound Sterling                 |
| GEL | Georgian Lari                          |
| GGP | Guernsey Pound                         |
| GHS | Ghanaian Cedi                          |
| GIP | Gibraltar Pound                        |
| GMD | Gambian Dalasi                         |
| GNF | Guinean Franc                          |
| GTQ | Guatemalan Quetzal                     |
| GYD | Guyanaese Dollar                       |
| HKD | Hong Kong Dollar                       |
| HNL | Honduran Lempira                       |
| HRK | Croatian Kuna                          |
| HTG | Haitian Gourde                         |
| HUF | Hungarian Forint                       |
| IDR | Indonesian Rupiah                      |
| ILS | Israeli New Sheqel                     |
| IMP | Manx pound                             |
| INR | Indian Rupee                           |
| IQD | Iraqi Dinar                            |
| IRR | Iranian Rial                           |
| ISK | Icelandic Króna                        |
| JEP | Jersey Pound                           |
| JMD | Jamaican Dollar                        |
| JOD | Jordanian Dinar                        |
| JPY | Japanese Yen                           |
| KES | Kenyan Shilling                        |
| KGS | Kyrgystani Som                         |
| KHR | Cambodian Riel                         |
| KMF | Comorian Franc                         |
| KPW | North Korean Won                       |
| KRW | South Korean Won                       |
| KWD | Kuwaiti Dinar                          |
| KYD | Cayman Islands Dollar                  |
| KZT | Kazakhstani Tenge                      |
| LAK | Laotian Kip                            |
| LBP | Lebanese Pound                         |
| LKR | Sri Lankan Rupee                       |
| LRD | Liberian Dollar                        |
| LSL | Lesotho Loti                           |
| LYD | Libyan Dinar                           |
| MAD | Moroccan Dirham                        |
| MDL | Moldovan Leu                           |
| MGA | Malagasy Ariary                        |
| MKD | Macedonian Denar                       |
| MMK | Myanma Kyat                            |
| MNT | Mongolian Tugrik                       |
| MOP | Macanese Pataca                        |
| MRO | Mauritanian Ouguiya (pre-2018)         |
| MRU | Mauritanian Ouguiya                    |
| MUR | Mauritian Rupee                        |
| MVR | Maldivian Rufiyaa                      |
| MWK | Malawian Kwacha                        |
| MXN | Mexican Peso                           |
| MYR | Malaysian Ringgit                      |
| MZN | Mozambican Metical                     |
| NAD | Namibian Dollar                        |
| NGN | Nigerian Naira                         |
| NIO | Nicaraguan Córdoba                     |
| NOK | Norwegian Krone                        |
| NPR | Nepalese Rupee                         |
| NZD | New Zealand Dollar                     |
| OMR | Omani Rial                             |
| PAB | Panamanian Balboa                      |
| PEN | Peruvian Nuevo Sol                     |
| PGK | Papua New Guinean Kina                 |
| PHP | Philippine Peso                        |
| PKR | Pakistani Rupee                        |
| PLN | Polish Zloty                           |
| PYG | Paraguayan Guarani                     |
| QAR | Qatari Rial                            |
| RON | Romanian Leu                           |
| RSD | Serbian Dinar                          |
| RUB | Russian Ruble                          |
| RWF | Rwandan Franc                          |
| SAR | Saudi Riyal                            |
| SBD | Solomon Islands Dollar                 |
| SCR | Seychellois Rupee                      |
| SDG | Sudanese Pound                         |
| SEK | Swedish Krona                          |
| SGD | Singapore Dollar                       |
| SHP | Saint Helena Pound                     |
| SLL | Sierra Leonean Leone                   |
| SOS | Somali Shilling                        |
| SRD | Surinamese Dollar                      |
| SSP | South Sudanese Pound                   |
| STD | São Tomé and Príncipe Dobra (pre-2018) |
| STN | São Tomé and Príncipe Dobra            |
| SVC | Salvadoran Colón                       |
| SYP | Syrian Pound                           |
| SZL | Swazi Lilangeni                        |
| THB | Thai Baht                              |
| TJS | Tajikistani Somoni                     |
| TMT | Turkmenistani Manat                    |
| TND | Tunisian Dinar                         |
| TOP | Tongan Paanga                          |
| TRY | Turkish Lira                           |
| TTD | Trinidad and Tobago Dollar             |
| TWD | New Taiwan Dollar                      |
| TZS | Tanzanian Shilling                     |
| UAH | Ukrainian Hryvnia                      |
| UGX | Ugandan Shilling                       |
| USD | United States Dollar                   |
| UYU | Uruguayan Peso                         |
| UZS | Uzbekistan Som                         |
| VEF | Venezuelan Bolívar Fuerte (Old)        |
| VES | Venezuelan Bolívar Soberano            |
| VND | Vietnamese Dong                        |
| VUV | Vanuatu Vatu                           |
| WST | Samoan Tala                            |
| XAF | CFA Franc BEAC                         |
| XAG | Silver Ounce                           |
| XAU | Gold Ounce                             |
| XCD | East Caribbean Dollar                  |
| XDR | Special Drawing Rights                 |
| XOF | CFA Franc BCEAO                        |
| XPD | Palladium Ounce                        |
| XPF | CFP Franc                              |
| XPT | Platinum Ounce                         |
| YER | Yemeni Rial                            |
| ZAR | South African Rand                     |
| ZMW | Zambian Kwacha                         |
| ZWL | Zimbabwean Dollar                      |
