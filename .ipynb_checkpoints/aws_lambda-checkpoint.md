# Source - [Currency Rate Rate API](https://github.com/fawazahmed0/currency-api#readme)

Features:

1. Free
2. Daily Updated
3. 150+ Currencies, Including Common Cryptocurrencies
4. No limits
---
## Get the currency list with AUD as base currency:

`/currencies/{currencyCode}`

(https://cdn.jsdelivr.net/gh/fawazahmed0/currency-api@1/latest/currencies/aud.json)

import **requests** and **json** to extract `date` and `rate` 

![jason_format](Images/fx_api_json.png)

---

# AWS Lambda

Modify lambda codes to get real-time data :

1. Add slot

![add slot](Images/new_slot_value.png)

2. Get data from API

![extract_value](Images/extract_value_from slot.png)


