Api- Customer address 编辑初始化
================

> vue 分类页面，得到分类信息的api

URL: `/customer/address/edit`

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


| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| address_id      | 必须        |   String     | customer address id    |

**请求参数示例如下：**

```
{
    address_id:118
}
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
        "address": {
            "address_id": 118,
            "first_name": "2121",
            "email": "fdfd@3232.com",
            "last_name": "2121",
            "company": null,
            "telephone": "2121",
            "fax": null,
            "street1": "2121",
            "street2": "2121",
            "city": "2121",
            "state": "NO",
            "zip": "2121",
            "country": "AT",
            "customer_id": 46,
            "created_at": 1506397526,
            "updated_at": 1509158174,
            "is_default": 1,
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
            "stateArr": {
                "WI": "Wien",
                "NO": "Niederösterreich",
                "OO": "Oberösterreich",
                "SB": "Salzburg",
                "KN": "Kärnten",
                "ST": "Steiermark",
                "TI": "Tirol",
                "BL": "Burgenland",
                "VB": "Voralberg"
            },
            "stateIsSelect": 1
        }
    }
}
```