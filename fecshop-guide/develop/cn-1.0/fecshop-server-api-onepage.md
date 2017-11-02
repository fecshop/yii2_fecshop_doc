Api- Onepage 初始化信息
================

> vue check onepage ，填写订单信息界面，初始化页面信息的api

URL: `/checkout/onepage/index`

格式：`json`

方式：`get`


一：请求部分
---------

#### 1.Request Header


| 参数名称          | 是否必须    |  类型        |  描述     |
| ------------------| -----:      | :----:       |:----:     |
| access-token      | 必须        |   String     | 从localStorage取出来的值，识别用户登录状态的标示，用户登录成功，服务端返回access-token，VUE保存到localStorage中，在下一次请求从localStorage取出来放到request header中   |
| fecshop-uuid      | 必须        |   String     | 从localStorage取出来的值，用户的唯一标示，VUE第一次访问服务端，服务端会返回fecshop-uuid ，VUE将其保存到本地，后面的每一次请求都需要加上fecshop-uuid    |
| fecshop-currency  | 必须        |   String     | 从localStorage取出来的值，当前的货币值  |
| fecshop-lang      | 必须        |   String     | 从localStorage取出来的值，当前的语言code  |


#### 2.Request Body Form-Data：

无

**请求参数示例如下：**

```
无
```

二：返回部分
----------

#### 1.Reponse Header

| 参数名称          | 是否必须    |  类型        |  描述     |
| ------------------| -----:      | :----:       |:----:     |
| access-token      | 选填        |   String     | 用户登录成功，服务端返回access-token，VUE保存到localStorage中，在下一次请求从localStorage取出来放到request header中   |
| fecshop-uuid      | 必须        |   String     | 用户的唯一标示，VUE第一次访问服务端，服务端会返回fecshop-uuid ，VUE将其保存到本地，后面的每一次请求都需要加上fecshop-uuid    |

#### 2.Reponse Body Form-Data：

格式：`json`

| 参数名称        | 是否必须    |  类型       |  描述        |
| ----------------| -----:      | :----:      |:----:        | 
| code            | 必须        |   Number    | 返回状态码，200 代表完成，完整的返回状态码详细参看:[Api- 状态码](fecshop-server-return-code.md) |
| message         | 必须        |   String    | 返回状态字符串描述  |
| data            | 必须        |   Array     | 返回详细数据        |

返回数据举例：

```
{
    "code": 200,
    "message": "process success",
    "data": {
        "payments": {  // 支付信息
            "check_money": {
                "label": "Check / Money Order",
                "imageUrl": "",
                "supplement": "Off-line Money Payments"
            },
            "paypal_standard": {
                "label": "PayPal Express Payments",
                "imageUrl": "",
                "supplement": null
            },
            "alipay_standard": {
                "label": "支付宝支付",
                "imageUrl": "",
                "supplement": null,
                "checked": true
            }
        },
        "shippings": [  // 货运快递信息
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
        "current_shipping_method": "fast_shipping",  // 当前的货运方式
        "current_payment_method": "alipay_standard", // 当前的支付方式
        "cart_info": {  // 购物车信息
            "store": "fecshop.appserver.fancyecommerce.com", // store
            "items_count": 18,    // 购物车产品总数
            "coupon_code": null,   // 优惠券
            "shipping_method": "fast_shipping",     // 购物车中的货运方式
            "payment_method": "alipay_standard",    // 购物车中的支付方式
            "grand_total": "240.93",                // 购物车总额（当前货币）
            "shipping_cost": "120.90",              // 购物车运费（当前货币）
            "coupon_cost": "0.00",                  // 购物车优惠券折扣（当前货币）
            "product_total": "120.03",              // 购物车产品总额（当前货币）
            "base_grand_total": "259.00",           // 购物车总额（基础货币）
            "base_shipping_cost": "130.00",         // 购物车运费（基础货币）
            "base_coupon_cost": "0.00",             // 购物车优惠券折扣（基础货币）
            "base_product_total": "129.00",         // 购物车产品总额（基础货币）
            "products": [  // 购物车产品信息
                {
                    "item_id": 274,
                    "product_id": "580835d0f656f240742f0b7c",
                    "sku": "p10001-kahaki-xl",
                    "name": "Raglan Sleeves Letter Printed Crew Neck Sweatshirt kahaki-xl",
                     // 产品个数
                    "qty": 15,
                    // 产品custom_option_sku
                    "custom_option_sku": "",
                    // 产品单价（当前货币）
                    "product_price": 3.91,
                    // 产品总价（当前货币）
                    "product_row_price": 58.650000000000006,
                    // 产品单价（基础货币）
                    "base_product_price": 4.2,
                    // 产品总价（基础货币）
                    "base_product_row_price": 63,
                    // 产品name（全部）
                    "product_name": {
                        "name_en": "Raglan Sleeves Letter Printed Crew Neck Sweatshirt kahaki-xl",
                        "name_fr": "",
                        "name_de": "",
                        "name_es": "",
                        "name_ru": "",
                        "name_pt": "",
                        "name_zh": "袖子信件印刷船员颈部运动衫kahaki xl"
                    },
                    // 产品的单重
                    "product_weight": 55,
                    // 产品的总重
                    "product_row_weight": 825,
                    // 产品url， vue不用这个，这是appfront  apphtml5部分用的
                    "product_url": "/raglan-sleeves-letter-printed-crew-neck-sweatshirt-53386451-77774122",
                    "product_image": {
                        // 细节图
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
                        // 主图
                        "main": {
                            "image": "/2/01/20160905101021_28071.jpg",
                            "label": "",
                            "sort_order": "",
                            "is_thumbnails": "1",
                            "is_detail": "1"
                        }
                    },
                    "custom_option": [],
                    // spu类的信息
                    "spu_options": {
                        "color": "khaki",
                        "size": "XL",
                        "test3": "t_1"
                    },
                    "imgUrl": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/100/100/2/01/20160905101021_28071.jpg",
                    // 颜色尺码等用户自定义属性
                    "custom_option_info": {
                        "color": "khaki",
                        "size": "XL",
                        "test3": "t_1"
                    }
                },
                {
                    "item_id": 411,
                    "product_id": "57bac59ef656f24f123bf56e",
                    "sku": "32332",
                    "name": "Bell Sleeve Off The Shoulder Lace Splicing Blouse",
                    "qty": 3,
                    "custom_option_sku": "",
                    "product_price": 20.46,
                    "product_row_price": 61.38,
                    "base_product_price": 22,
                    "base_product_row_price": 66,
                    "product_name": {
                        "name_en": "Bell Sleeve Off The Shoulder Lace Splicing Blouse",
                        "name_fr": "",
                        "name_de": "",
                        "name_es": "",
                        "name_ru": "",
                        "name_pt": "",
                        "name_zh": "贝尔袖脱下肩带花边拼接女衬衫"
                    },
                    "product_weight": 0,
                    "product_row_weight": 0,
                    "product_url": "/3232",
                    "product_image": {
                        "main": {
                            "image": "/1/14/11471858072718.jpg",
                            "label": "",
                            "sort_order": "",
                            "is_thumbnails": "1",
                            "is_detail": "1"
                        }
                    },
                    "custom_option": [],
                    "spu_options": {
                        "color": "black",
                        "size": "M"
                    },
                    "imgUrl": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/100/100/1/14/11471858072718.jpg",
                    "custom_option_info": {
                        "color": "black",
                        "size": "M"
                    }
                }
            ],
            "product_weight": 825
        },
        "currency_info": {
            "code": "EUR",
            "rate": 0.93,
            "symbol": "€"
        },
        "isGuest": 0,
        "address_list": {
            "117": {
                "address": "111 222 34343@3232.com 3232 3232 3232 BJ China ewewew 3232",
                "is_default": "2"
            },
            "118": {
                "address": "2121 2121 fdfd@3232.com 2121 2121 2121 NO Austria 2121 2121",
                "is_default": "1"
            }
        },
        "cart_address": {
            "email": "fdfd@3232.com",
            "first_name": "2121",
            "last_name": "2121",
            "telephone": "2121",
            "country": "AT",
            "state": "NO",
            "city": "2121",
            "zip": "2121",
            "street1": "2121",
            "street2": "2121"
        },
        "cart_address_id": 118,
        "countryArr": {
            "AF": "Afghanistan",
            "AX": "Åland Islands",
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
            "CI": "Côte d’Ivoire",
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
            "RE": "R¨¦union",
            "RO": "Romania",
            "RU": "Russia",
            "RW": "Rwanda",
            "BL": "Saint Barth¨¦lemy",
            "SH": "Saint Helena",
            "KN": "Saint Kitts and Nevis",
            "LC": "Saint Lucia",
            "MF": "Saint Martin",
            "PM": "Saint Pierre and Miquelon",
            "VC": "Saint Vincent and the Grenadines",
            "WS": "Samoa",
            "SM": "San Marino",
            "ST": "São Tomé and Príncipe",
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