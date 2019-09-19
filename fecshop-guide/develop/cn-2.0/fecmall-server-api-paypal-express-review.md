Api- Cart Paypal Express Review
==============================

> 购物车页面点击paypal按钮，跳转到paypal登录，然后点击continue跳转回fecshop页面，
> 页面初始化访问的api

URL: `/payment/paypal/express/review`

格式：`json`

方式：`get`


一：请求部分
---------

#### 1.Request Header


| 参数名称          | 是否必须    |  类型        |  描述     |
| ------------------| -----:      | :----:       |:----:     |
| access-token      | 必须        |   String     | 从localStorage取出来的值，识别用户登录状态的标示，用户登录成功，服务端返回access-token，VUE保存到localStorage中，在下一次请求从localStorage取出来放到request header中   |
| fecshop-currency  | 必须        |   String     | 从localStorage取出来的值，当前的货币值  |
| fecshop-lang      | 必须        |   String     | 从localStorage取出来的值，当前的语言code  |


#### 2.Request Body Form-Data：


| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| token           | 必须        |   String     | paypal token     |
| PayerID         | 必须        |   String     | paypal PayerID   |

**请求参数示例如下：**

```
{
    token: "EC-1TN688728J034651L",
    PayerID: "FKL4V7D5GCACY"
}
```

二：返回部分
----------

#### 1.Reponse Header

| 参数名称          | 是否必须    |  类型        |  描述     |
| ------------------| -----:      | :----:       |:----:     |
| access-token      | 选填        |   String     | 用户登录成功，服务端返回access-token，VUE保存到localStorage中，在下一次请求从localStorage取出来放到request header中   |

#### 2.Reponse Body Form-Data：

格式：`json`

| 参数名称        | 是否必须    |  类型       |  描述        |
| ----------------| -----:      | :----:      |:----:        | 
| code            | 必须        |   Number    | 返回状态码，200 代表完成，完整的返回状态码详细参看:[Api- 状态码](fecshop-server-return-code.md) |
| message         | 必须        |   String    | 返回状态字符串描述  |
| data            | 必须        |   Array     | 返回详细数据        |

#### 3.参数code所有返回状态码：（完整的返回状态码详细参看:[Api- 状态码](fecshop-server-return-code.md) ）

| code Value      |        描述                                        |
| ----------------| --------------------------------------------------:| 
| 200             | 成功状态码                                         |  
| 1500007         | Order: 下订单，购物车数据为空                  | 
| 1500003         | Order: 通过paypal express方式支付，获取token失败                 | 
| 1500015         | Order: 通过paypal express方式支付，获取PayerID失败                 | 
| 1500016         | Order: 通过paypal express方式支付，获取address失败                 | 


 
 
#### 4.返回数据举例：

各个字段的具体函数参看[fecshop-server-api-onepage.md](fecshop-server-api-onepage.md)

```
{
    "code": 200,
    "message": "process success",
    "data": {
        "payments": {
            "check_money": {
                "label": "Check / Money Order",
                "imageUrl": "",
                "supplement": "Off-line Money Payments"
            },
            "paypal_standard": {
                "label": "PayPal Express Payments",
                "imageUrl": "",
                "supplement": null,
                "checked": true
            },
            "alipay_standard": {
                "label": "支付宝支付",
                "imageUrl": "",
                "supplement": null
            }
        },
        "shippings": [
            {
                "method": "free_shipping",
                "label": "Free shipping( 7-20 work days)",
                "name": "HKBRAM",
                "cost": "0.00",
                "symbol": "€",
                "checked": "",
                "shipping_i": 1
            },
            {
                "method": "fast_shipping",
                "label": "Fast Shipping( 5-10 work days)",
                "name": "HKDHL",
                "cost": 120.9,
                "symbol": "€",
                "checked": true,
                "shipping_i": 2
            }
        ],
        "current_payment_method": "paypal_standard",
        "current_shipping_method": "fast_shipping",
        "cart_info": {
            "store": "fecshop.appserver.fancyecommerce.com",
            "items_count": 1,
            "coupon_code": null,
            "shipping_method": "fast_shipping",
            "payment_method": "paypal_standard",
            "grand_total": "125.60",
            "shipping_cost": "120.90",
            "coupon_cost": "0.00",
            "product_total": "4.70",
            "base_grand_total": "135.05",
            "base_shipping_cost": "130.00",
            "base_coupon_cost": "0.00",
            "base_product_total": "5.05",
            "products": [
                {
                    "item_id": 447,
                    "product_id": "580835d0f656f240742f0b7c",
                    "sku": "p10001-kahaki-xl",
                    "name": "Raglan Sleeves Letter Printed Crew Neck Sweatshirt kahaki-xl",
                    "qty": 1,
                    "custom_option_sku": "",
                    "product_price": 4.7,
                    "product_row_price": 4.7,
                    "base_product_price": 5.05,
                    "base_product_row_price": 5.05,
                    "product_name": {
                        "name_en": "Raglan Sleeves Letter Printed Crew Neck Sweatshirt kahaki-xl",
                        "name_fr": "",
                        "name_de": "",
                        "name_es": "",
                        "name_ru": "",
                        "name_pt": "",
                        "name_zh": "袖子信件印刷船员颈部运动衫kahaki xl"
                    },
                    "product_weight": 55,
                    "product_row_weight": 55,
                    "product_url": "/raglan-sleeves-letter-printed-crew-neck-sweatshirt-53386451-77774122",
                    "product_image": {
                        "gallery": [
                            {
                                "image": "/2/01/20160905101021_56532.jpg",
                                "label": "",
                                "sort_order": "",
                                "is_thumbnails": "1",
                                "is_detail": "1"
                            },
                            {
                                "image": "/2/01/20160905101022_25969.jpg",
                                "label": "",
                                "sort_order": "",
                                "is_thumbnails": "1",
                                "is_detail": "1"
                            },
                            {
                                "image": "/2/01/20160905101022_79159.jpg",
                                "label": "",
                                "sort_order": "",
                                "is_thumbnails": "1",
                                "is_detail": "1"
                            },
                            {
                                "image": "/2/01/20160905101021_28071147710702992998.jpg",
                                "label": "",
                                "sort_order": "",
                                "is_thumbnails": "1",
                                "is_detail": "1"
                            },
                            {
                                "image": "/2/01/20160905101021_28071147710703579813.jpg",
                                "label": "",
                                "sort_order": "",
                                "is_thumbnails": "1",
                                "is_detail": "1"
                            }
                        ],
                        "main": {
                            "image": "/2/01/20160905101021_28071.jpg",
                            "label": "",
                            "sort_order": "",
                            "is_thumbnails": "1",
                            "is_detail": "1"
                        }
                    },
                    "custom_option": [],
                    "spu_options": {
                        "color": "khaki",
                        "size": "XL",
                        "test3": "t_1"
                    },
                    "imgUrl": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/100/100/2/01/20160905101021_28071.jpg",
                    "custom_option_info": {
                        "color": "khaki",
                        "size": "XL",
                        "test3": "t_1"
                    }
                }
            ],
            "product_weight": 55
        },
        "currency_info": {
            "code": "EUR",
            "rate": 0.93,
            "symbol": "€"
        },
        "isGuest": 0,
        "address_list": {
            "118": {
                "address": "2121 2121 fdfd@3232.com 2121 2121 2121 NO Austria 2121 2121",
                "is_default": "1"
            }
        },
        "cart_address": {
            "country": "US",
            "state": "NY",
            "first_name": "test",
            "last_name": "facilitator",
            "email": "zqy234api1-facilitator-1@126.com",
            "telephone": "2121",
            "street1": "4114 Sepulveda Blvd.",
            "street2": "4114 Sepulveda Blvd.",
            "city": "New York",
            "zip": "10021"
        },
        "cart_address_id": 118,
        "countryArr": {
            "AF": "Afghanistan",
            "AX": "?land Islands",
            "AL": "Albania",
            "DZ": "Algeria",
            "AS": "American Samoa",
            "AD": "Andorra",
            "AO": "Angola",
            "AI": "Anguilla",
            "AQ": "Antarctica",
            "AG": "Antigua and Barbuda",
            "AR": "Argentina",
            "AM": "Armenia",
            "AW": "Aruba",
            "AU": "Australia",
            "AT": "Austria",
            "AZ": "Azerbaijan",
            "BS": "Bahamas",
            "BH": "Bahrain",
            "BD": "Bangladesh",
            "BB": "Barbados",
            "BY": "Belarus",
            "BE": "Belgium",
            "BZ": "Belize",
            "BJ": "Benin",
            "BM": "Bermuda",
            "BT": "Bhutan",
            "BO": "Bolivia",
            "BA": "Bosnia and Herzegovina",
            "BW": "Botswana",
            "BV": "Bouvet Island",
            "BR": "Brazil",
            "IO": "British Indian Ocean Territory",
            "VG": "British Virgin Islands",
            "BN": "Brunei",
            "BG": "Bulgaria",
            "BF": "Burkina Faso",
            "BI": "Burundi",
            "KH": "Cambodia",
            "CM": "Cameroon",
            "CA": "Canada",
            "CV": "Cape Verde",
            "KY": "Cayman Islands",
            "CF": "Central African Republic",
            "TD": "Chad",
            "CL": "Chile",
            "CN": "China",
            "CX": "Christmas Island",
            "CC": "Cocos [Keeling] Islands",
            "CO": "Colombia",
            "KM": "Comoros",
            "CG": "Congo - Brazzaville",
            "CD": "Congo - Kinshasa",
            "CK": "Cook Islands",
            "CR": "Costa Rica",
            "CI": "C?te d’Ivoire",
            "HR": "Croatia",
            "CU": "Cuba",
            "CY": "Cyprus",
            "CZ": "Czech Republic",
            "DK": "Denmark",
            "DJ": "Djibouti",
            "DM": "Dominica",
            "DO": "Dominican Republic",
            "EC": "Ecuador",
            "EG": "Egypt",
            "SV": "El Salvador",
            "GQ": "Equatorial Guinea",
            "ER": "Eritrea",
            "EE": "Estonia",
            "ET": "Ethiopia",
            "FK": "Falkland Islands",
            "FO": "Faroe Islands",
            "FJ": "Fiji",
            "FI": "Finland",
            "FR": "France",
            "GF": "French Guiana",
            "PF": "French Polynesia",
            "TF": "French Southern Territories",
            "GA": "Gabon",
            "GM": "Gambia",
            "GE": "Georgia",
            "DE": "Germany",
            "GH": "Ghana",
            "GI": "Gibraltar",
            "GR": "Greece",
            "GL": "Greenland",
            "GD": "Grenada",
            "GP": "Guadeloupe",
            "GU": "Guam",
            "GT": "Guatemala",
            "GG": "Guernsey",
            "GN": "Guinea",
            "GW": "Guinea-Bissau",
            "GY": "Guyana",
            "HT": "Haiti",
            "HM": "Heard Island and McDonald Islands",
            "HN": "Honduras",
            "HK": "Hong Kong SAR China",
            "HU": "Hungary",
            "IS": "Iceland",
            "IN": "India",
            "ID": "Indonesia",
            "IR": "Iran",
            "IQ": "Iraq",
            "IE": "Ireland",
            "IM": "Isle of Man",
            "IL": "Israel",
            "IT": "Italy",
            "JM": "Jamaica",
            "JP": "Japan",
            "JE": "Jersey",
            "JO": "Jordan",
            "KZ": "Kazakhstan",
            "KE": "Kenya",
            "KI": "Kiribati",
            "KW": "Kuwait",
            "KG": "Kyrgyzstan",
            "LA": "Laos",
            "LV": "Latvia",
            "LB": "Lebanon",
            "LS": "Lesotho",
            "LR": "Liberia",
            "LY": "Libya",
            "LI": "Liechtenstein",
            "LT": "Lithuania",
            "LU": "Luxembourg",
            "MO": "Macau SAR China",
            "MK": "Macedonia",
            "MG": "Madagascar",
            "MW": "Malawi",
            "MY": "Malaysia",
            "MV": "Maldives",
            "ML": "Mali",
            "MT": "Malta",
            "MH": "Marshall Islands",
            "MQ": "Martinique",
            "MR": "Mauritania",
            "MU": "Mauritius",
            "YT": "Mayotte",
            "MX": "Mexico",
            "FM": "Micronesia",
            "MD": "Moldova",
            "MC": "Monaco",
            "MN": "Mongolia",
            "ME": "Montenegro",
            "MS": "Montserrat",
            "MA": "Morocco",
            "MZ": "Mozambique",
            "MM": "Myanmar [Burma]",
            "NA": "Namibia",
            "NR": "Nauru",
            "NP": "Nepal",
            "NL": "Netherlands",
            "AN": "Netherlands Antilles",
            "NC": "New Caledonia",
            "NZ": "New Zealand",
            "NI": "Nicaragua",
            "NE": "Niger",
            "NG": "Nigeria",
            "NU": "Niue",
            "NF": "Norfolk Island",
            "MP": "Northern Mariana Islands",
            "KP": "North Korea",
            "NO": "Norway",
            "OM": "Oman",
            "PK": "Pakistan",
            "PW": "Palau",
            "PS": "Palestinian Territories",
            "PA": "Panama",
            "PG": "Papua New Guinea",
            "PY": "Paraguay",
            "PE": "Peru",
            "PH": "Philippines",
            "PN": "Pitcairn Islands",
            "PL": "Poland",
            "PT": "Portugal",
            "PR": "Puerto Rico",
            "QA": "Qatar",
            "RE": "R¨|union",
            "RO": "Romania",
            "RU": "Russia",
            "RW": "Rwanda",
            "BL": "Saint Barth¨|lemy",
            "SH": "Saint Helena",
            "KN": "Saint Kitts and Nevis",
            "LC": "Saint Lucia",
            "MF": "Saint Martin",
            "PM": "Saint Pierre and Miquelon",
            "VC": "Saint Vincent and the Grenadines",
            "WS": "Samoa",
            "SM": "San Marino",
            "ST": "S?o Tomé and Príncipe",
            "SA": "Saudi Arabia",
            "SN": "Senegal",
            "RS": "Serbia",
            "SC": "Seychelles",
            "SL": "Sierra Leone",
            "SG": "Singapore",
            "SK": "Slovakia",
            "SI": "Slovenia",
            "SB": "Solomon Islands",
            "SO": "Somalia",
            "ZA": "South Africa",
            "GS": "South Georgia and the South Sandwich Islands",
            "KR": "South Korea",
            "ES": "Spain",
            "LK": "Sri Lanka",
            "SD": "Sudan",
            "SR": "Suriname",
            "SJ": "Svalbard and Jan Mayen",
            "SZ": "Swaziland",
            "SE": "Sweden",
            "CH": "Switzerland",
            "SY": "Syria",
            "TW": "Taiwan",
            "TJ": "Tajikistan",
            "TZ": "Tanzania",
            "TH": "Thailand",
            "TL": "Timor-Leste",
            "TG": "Togo",
            "TK": "Tokelau",
            "TO": "Tonga",
            "TT": "Trinidad and Tobago",
            "TN": "Tunisia",
            "TR": "Turkey",
            "TM": "Turkmenistan",
            "TC": "Turks and Caicos Islands",
            "TV": "Tuvalu",
            "UG": "Uganda",
            "UA": "Ukraine",
            "AE": "United Arab Emirates",
            "GB": "United Kingdom",
            "US": "United States",
            "UY": "Uruguay",
            "UM": "U.S. Minor Outlying Islands",
            "VI": "U.S. Virgin Islands",
            "UZ": "Uzbekistan",
            "VU": "Vanuatu",
            "VA": "Vatican City",
            "VE": "Venezuela",
            "VN": "Vietnam",
            "WF": "Wallis and Futuna",
            "EH": "Western Sahara",
            "YE": "Yemen",
            "ZM": "Zambia",
            "ZW": "Zimbabwe"
        },
        "country": "AT"
    }
}
```