---
title: Enbro Soho HTTP API
language_tabs:
  - json: JSON
  - shell: cURL
---

Enbro Soho HTTP API.

The enbro soho system can find new gas and electricity offers for a customer if it has all the necessary data.
Therefore the API allows you to create customers and provide all the necessary data for them,
including data of their EAN records.

According to customer records you can:

- Create new customers for your organisation through the API.
  The created customers are treated by the system the same way
  as the customers who registered using enbro soho registration forms.
- Get a list of the customers that have been created for the organisation.
- Get attributes of a customer by his ID.

When you have an ID of a customer, you can use it to create EAN records for him.

# Customers

    Allows to manage list of customers of the current organisation.
    Current organisation defined based on a provided API token.
    You can provide an API token using `Authorization` request header.

    For example: `Authorization: Bearer 2453797fc41e0cfa5c7a00f5acfd6915`


## CREATE 201 Created

Creates a customer for the current organisation and returns it's attributes

### Request

#### Endpoint

```plaintext
POST /api/v1/customers
Content-Type: application/json
Authorization: Bearer 7fe408044fc5c0c747e93891d1a917a4
```

`POST /api/v1/customers`

#### Parameters


```json
{
  "customer": {
    "email": "elinore_baumbach@nienow.net",
    "terms_and_conditions": true,
    "privacy_policy": true,
    "registered_from_ip": "107.108.66.61",
    "profile": {
      "first_name": "Danny",
      "last_name": "Ocean",
      "title": "mr",
      "phone": "+3256980144",
      "birth_date": "2000-04-07",
      "city": "Schulistshire",
      "street": "60947 Considine Squares",
      "building": "3057",
      "building_addon": "Apt. 462",
      "postal_code": "22144-5239",
      "language": "en"
    }
  }
}
```


| Name | Description |
|:-----|:------------|
| customer[email] *required* | A customer's email. Serves as an unique identifier of a customer. A customer with the same email must be not registered before. |
| customer[terms_and_conditions] *required* | Type: *boolean*. Flag that terms and conditions is accepted |
| customer[privacy_policy] *required* | Type: *boolean*. Flag that the privacy policy is accepted |
| customer[registered_from_ip] *required* | Customer registered from ip |
| customer[profile] *required* | Attributes for the profile of a customer |
| customer[profile][first_name] *required* | Customer profile first name |
| customer[profile][last_name] *required* | Customer profile last name |
| customer[profile][title] *required* | Values: ["mr", "mrs"]. Example: "mr". Customer profile title |
| customer[profile][phone] *required* | Example: "+3256980144". Customer profile phone |
| customer[profile][birth_date] *required* | Example: "2000-04-06". Customer profile birth date |
| customer[profile][city] *required* | Customer profile city |
| customer[profile][street] *required* | Customer profile street |
| customer[profile][building] *required* | Customer profile building |
| customer[profile][building_addon]  | Customer profile building addon |
| customer[profile][postal_code] *required* | Customer profile postal code |
| customer[profile][language]  | Values: ["nl", "fr", "en"]. Default: "nl". Customer profile language |



### Response

```plaintext
Content-Type: application/json; charset=utf-8
201 Created
```


```json
{
  "id": 5,
  "email": "elinore_baumbach@nienow.net",
  "created_at": "2020-04-07T15:28:31.073Z",
  "updated_at": "2020-04-07T15:28:31.123Z",
  "organisation": {
    "id": 6,
    "name": "Toy LLC",
    "domain": "champlin-monahan-4",
    "created_at": "2020-04-07T15:28:31.025Z"
  },
  "profile": {
    "id": 5,
    "customer_id": 5,
    "title": "mr",
    "first_name": "Danny",
    "last_name": "Ocean",
    "birth_date": "2000-04-07",
    "phone": "+3256980144",
    "city": "Schulistshire",
    "street": "60947 Considine Squares",
    "building": "3057",
    "building_addon": "Apt. 462",
    "postal_code": "22144-5239",
    "language": "en",
    "created_at": "2020-04-07T15:28:31.076Z",
    "updated_at": "2020-04-07T15:28:31.076Z"
  }
}
```



#### Fields

| Name       | Description         |
|:-----------|:--------------------|
| id | ID of the customer |
| email | Unique email of the customer |
| organisation | Attributes of the organisation to which the customer belongs to |
| organisation[id] | ID of the customer's organisation |
| organisation[name] | Name of the organisation |
| organisation[domain] | Domain of the organisation. Usually it's a subdomain under the parent organisation's domain |
| organisation[created_at] | Date and time when the organisation has been created |
| profile[id] | ID of the customer's profile |
| profile[customer_id] | ID of the customer to whom the profile belongs to |
| profile[title] | Values: ["mr", "mrs"]. Example: "mr". Customer profile title |
| profile[first_name] | The customer's first name |
| profile[last_name] | The customer's last name |
| profile[birth_date] | The customer's birth date |
| profile[phone] | Example: "+32460123456". The phone number (full format - only country code with digits) |
| profile[city] | The customer's address - city |
| profile[street] | The customer's address - street |
| profile[building] | The customer's address - building |
| profile[building_addon] | The customer's address - buildin addon |
| profile[postal_code] | The customer's address - zip code |
| profile[language] | Values: ["nl", "fr", "en"]. Customer profile language |
| profile[created_at] | Date and time when the customer profile has been created |
| profile[updated_at] | Date and time when the customer profile has been updated |


## CREATE 422 Validation Error

          At least one of the specified parameters contains an error.
          Check if all the required parameters have been specified.
          Also the specified email must be unique.
          You can find details about the error in the response.


### Request

#### Endpoint

```plaintext
POST /api/v1/customers
Content-Type: application/json
Authorization: Bearer d112c33c9cb5eecdc3b5b0265b951a04
```

`POST /api/v1/customers`

#### Parameters


```json
{
  "customer": {
    "email": "mellisa@howell.name",
    "terms_and_conditions": true,
    "privacy_policy": true,
    "registered_from_ip": "88.69.49.78",
    "profile": {
      "first_name": null,
      "last_name": "Ocean",
      "title": "mr",
      "phone": "+3256980144",
      "birth_date": "2000-04-07",
      "city": "Lake Edgar",
      "street": "54704 Serafina Row",
      "building": "299",
      "building_addon": "Suite 484",
      "postal_code": "28843-2543",
      "language": "en"
    }
  }
}
```


| Name | Description |
|:-----|:------------|
| customer[email] *required* | A customer's email. Serves as an unique identifier of a customer. A customer with the same email must be not registered before. |
| customer[terms_and_conditions] *required* | Type: *boolean*. Flag that terms and conditions is accepted |
| customer[privacy_policy] *required* | Type: *boolean*. Flag that the privacy policy is accepted |
| customer[registered_from_ip] *required* | Customer registered from ip |
| customer[profile] *required* | Attributes for the profile of a customer |
| customer[profile][first_name] *required* | Customer profile first name |
| customer[profile][last_name] *required* | Customer profile last name |
| customer[profile][title] *required* | Values: ["mr", "mrs"]. Example: "mr". Customer profile title |
| customer[profile][phone] *required* | Example: "+3256980144". Customer profile phone |
| customer[profile][birth_date] *required* | Example: "2000-04-06". Customer profile birth date |
| customer[profile][city] *required* | Customer profile city |
| customer[profile][street] *required* | Customer profile street |
| customer[profile][building] *required* | Customer profile building |
| customer[profile][building_addon]  | Customer profile building addon |
| customer[profile][postal_code] *required* | Customer profile postal code |
| customer[profile][language]  | Values: ["nl", "fr", "en"]. Default: "nl". Customer profile language |



### Response

```plaintext
Content-Type: application/json; charset=utf-8
422 Unprocessable Entity
```


```json
{
  "errors": [
    {
      "path": "customer.profile.first_name",
      "error": "must_be_filled",
      "message": "must be filled",
      "type": "params"
    }
  ]
}
```



#### Fields

| Name       | Description         |
|:-----------|:--------------------|
| errors | Type: *array*. Items type: *object*. Contains a list of occurred errors |
| path | A full name of an erroneous field |
| error | A string identifier of the error |
| message | An error message |
| type | A type of the error |


## LIST 200 OK

Returns customers of the current organisation.
Current organisation defined based on provided API token.


### Request

#### Endpoint

```plaintext
GET /api/v1/customers?page=1&amp;per=2
Content-Type: application/json
Authorization: Bearer 6dfac5049208cfdc904e402e0cda1b29
```

`GET /api/v1/customers`

#### Parameters


```json
page: 1
per: 2
```


| Name | Description |
|:-----|:------------|
| page  |  page |
| per  | Limit of records per page. Max value is 25. |



### Response

```plaintext
Content-Type: application/json; charset=utf-8
200 OK
```


```json
{
  "current_page": 1,
  "limit_value": 2,
  "next_page": 2,
  "prev_page": null,
  "total_pages": 2,
  "records": [
    {
      "id": 8,
      "email": "dara@donnelly.info",
      "created_at": "2020-04-07T15:28:31.384Z",
      "updated_at": "2020-04-07T15:28:31.384Z",
      "organisation": {
        "id": 12,
        "name": "Huel Group",
        "domain": "towne-king-8",
        "created_at": "2020-04-07T15:28:31.380Z"
      },
      "profile": {
        "id": 8,
        "customer_id": 8,
        "title": "mr",
        "first_name": "Xavier",
        "last_name": "Dickinson",
        "birth_date": "1991-01-30",
        "phone": "+32460123456",
        "city": "Lake Helenechester",
        "street": "Wyman Lakes",
        "building": "33968",
        "building_addon": "Suite 596",
        "postal_code": "92412-0701",
        "language": "nl",
        "created_at": "2020-04-07T15:28:31.388Z",
        "updated_at": "2020-04-07T15:28:31.388Z"
      }
    },
    {
      "id": 10,
      "email": "karole@windleranderson.io",
      "created_at": "2020-04-07T15:28:31.414Z",
      "updated_at": "2020-04-07T15:28:31.414Z",
      "organisation": {
        "id": 12,
        "name": "Huel Group",
        "domain": "towne-king-8",
        "created_at": "2020-04-07T15:28:31.380Z"
      },
      "profile": {
        "id": 10,
        "customer_id": 10,
        "title": "mr",
        "first_name": "Landon",
        "last_name": "Runolfsson",
        "birth_date": "1980-08-15",
        "phone": "+32460123456",
        "city": "Lake Kassie",
        "street": "Bruen Lake",
        "building": "8844",
        "building_addon": "Suite 612",
        "postal_code": "43452",
        "language": "fr",
        "created_at": "2020-04-07T15:28:31.423Z",
        "updated_at": "2020-04-07T15:28:31.423Z"
      }
    }
  ]
}
```



#### Fields

| Name       | Description         |
|:-----------|:--------------------|
| current_page | The current page number |
| limit_value | Limit of records on a page |
| next_page | The next page number |
| prev_page | The previous page number |
| total_pages | Total available pages |
| records | The list of found records |
| id | ID of the customer |
| email | Unique email of the customer |
| organisation | Attributes of the organisation to which the customer belongs to |
| organisation[id] | ID of the customer's organisation |
| organisation[name] | Name of the organisation |
| organisation[domain] | Domain of the organisation. Usually it's a subdomain under the parent organisation's domain |
| organisation[created_at] | Date and time when the organisation has been created |
| profile[id] | ID of the customer's profile |
| profile[customer_id] | ID of the customer to whom the profile belongs to |
| profile[title] | Values: ["mr", "mrs"]. Example: "mr". Customer profile title |
| profile[first_name] | The customer's first name |
| profile[last_name] | The customer's last name |
| profile[birth_date] | The customer's birth date |
| profile[phone] | Example: "+32460123456". The phone number (full format - only country code with digits) |
| profile[city] | The customer's address - city |
| profile[street] | The customer's address - street |
| profile[building] | The customer's address - building |
| profile[building_addon] | The customer's address - buildin addon |
| profile[postal_code] | The customer's address - zip code |
| profile[language] | Values: ["nl", "fr", "en"]. Customer profile language |
| profile[created_at] | Date and time when the customer profile has been created |
| profile[updated_at] | Date and time when the customer profile has been updated |


## SHOW 200 OK

          Returns the attributes of the customer with provided ID.
          The customer must belong to the current organisation.


### Request

#### Endpoint

```plaintext
GET /api/v1/customers/23
Content-Type: application/json
Authorization: Bearer 3135e96291614a972d51aa2020198822
```

`GET /api/v1/customers/:id`

#### Parameters



| Name | Description |
|:-----|:------------|
| id *required* | Type: *integer*. ID of a customer |



### Response

```plaintext
Content-Type: application/json; charset=utf-8
200 OK
```


```json
{
  "id": 23,
  "email": "jarvis.sipes@beiernader.info",
  "created_at": "2020-04-07T15:28:31.764Z",
  "updated_at": "2020-04-07T15:28:31.764Z",
  "organisation": {
    "id": 21,
    "name": "Maggio, Frami and White",
    "domain": "breitenbergsanford-kiehn-14",
    "created_at": "2020-04-07T15:28:31.760Z"
  },
  "profile": {
    "id": 23,
    "customer_id": 23,
    "title": "mr",
    "first_name": "Ester",
    "last_name": "Predovic",
    "birth_date": "1981-05-03",
    "phone": "+3256980144",
    "city": "Lake Janine",
    "street": "Johana Meadow",
    "building": "5241",
    "building_addon": "Suite 520",
    "postal_code": "49319",
    "language": "nl",
    "created_at": "2020-04-07T15:28:31.768Z",
    "updated_at": "2020-04-07T15:28:31.768Z"
  }
}
```



#### Fields

| Name       | Description         |
|:-----------|:--------------------|
| id | ID of the customer |
| email | Unique email of the customer |
| organisation | Attributes of the organisation to which the customer belongs to |
| organisation[id] | ID of the customer's organisation |
| organisation[name] | Name of the organisation |
| organisation[domain] | Domain of the organisation. Usually it's a subdomain under the parent organisation's domain |
| organisation[created_at] | Date and time when the organisation has been created |
| profile[id] | ID of the customer's profile |
| profile[customer_id] | ID of the customer to whom the profile belongs to |
| profile[title] | Values: ["mr", "mrs"]. Example: "mr". Customer profile title |
| profile[first_name] | The customer's first name |
| profile[last_name] | The customer's last name |
| profile[birth_date] | The customer's birth date |
| profile[phone] | Example: "+32460123456". The phone number (full format - only country code with digits) |
| profile[city] | The customer's address - city |
| profile[street] | The customer's address - street |
| profile[building] | The customer's address - building |
| profile[building_addon] | The customer's address - buildin addon |
| profile[postal_code] | The customer's address - zip code |
| profile[language] | Values: ["nl", "fr", "en"]. Customer profile language |
| profile[created_at] | Date and time when the customer profile has been created |
| profile[updated_at] | Date and time when the customer profile has been updated |


## SHOW 404 Not Found

          A customer with specified ID haven't been found.
          The customer must belong to the current organisation.
          Current organisation defined based on provided API token.


### Request

#### Endpoint

```plaintext
GET /api/v1/customers/27
Content-Type: application/json
Authorization: Bearer 4a2716c00738cd43fe833c935087acee
```

`GET /api/v1/customers/:id`

#### Parameters



| Name | Description |
|:-----|:------------|
| id *required* | Type: *integer*. ID of a customer |



### Response

```plaintext
Content-Type: application/json; charset=utf-8
404 Not Found
```


```json
"Not found"
```



# Customers / Eans

    Allows to create an EAN record and get the list of EAN records for a customer.
    While a customer doesn't have any EAN records it's not possible to find an offer for him.

    You must specify an ID of a customer and provide all the necessary data.
    The customer must belong to the current organisation.
    Current organisation defined based on a provided API token.
    You can provide an API token using `Authorization` request header.

    For example: `Authorization: Bearer 2453797fc41e0cfa5c7a00f5acfd6915`


## CREATE 201 Created

Create an EAN record for the specified customer

### Request

#### Endpoint

```plaintext
POST /api/v1/customers/33/eans
Content-Type: application/json
Authorization: Bearer a2bb9af4749473cd43d905c26fbf990c
```

`POST /api/v1/customers/:customer_id/eans`

#### Parameters


```json
{
  "ean": {
    "number": "542170967180397340",
    "product": "electricity",
    "reason": "normal",
    "supplier_id": 4,
    "building": "15",
    "building_addon": "A",
    "street": "street name",
    "city": "Kiev",
    "postal_code": "2443",
    "consumptions": [
      {
        "name": "mono",
        "volume": "22.25",
        "price": "0.15"
      }
    ],
    "recording_period": "february",
    "solar_panels": "true",
    "inverter_max_power": "315",
    "contract_end_date": "2020-10-07",
    "fixed_fee": "1.00",
    "tariff_group": "mono",
    "wkk": "0.00341",
    "gsc": "0.0214"
  }
}
```


| Name | Description |
|:-----|:------------|
| customer_id *required* | ID of the customer |
| ean *required* | Attributes for the EAN record |
| ean[number]  | EAN number |
| ean[product]  | Enum: ["gas", "electricity"]. The EAN record's product. Must be a value from the enum |
| ean[reason]  | Enum: ["normal", "new", "reopened", "dropped", "moved"]. The reason why the customer is searching for a new offer. Must be a value from the enum. |
| ean[supplier_id]  | ID of the supplier for the EAN connection |
| ean[building]  | The address for the EAN connection - building addon |
| ean[building_addon]  | The address of the EAN connection - street |
| ean[street]  | The address for the EAN connection - building |
| ean[city]  | The address of the EAN connection - city |
| ean[postal_code]  | The address of the EAN connection - postal_code |
| ean[consumptions]  | The consumptions for the EAN connection |
| ean[consumptions][name]  | Name of the tariff |
| ean[consumptions][volume]  | A consumption volume by the tariff |
| ean[consumptions][price]  | A price for the tariff |
| ean[recording_period]  | Recording period of the EAN. Enum: ["automatic", "monthly", "january", "february", "march", "april", "may", "june", "july", "august", "september", "october", "november", "december"] |
| ean[solar_panels]  | Type: *boolen*. For *electricity* only. A flag that the EAN connection has solar panels.  |
| ean[inverter_max_power]  | Inverter Max Power. Only then solar panels flag is true |
| ean[contract_end_date]  | The date when the contract for the EAN connection ends |
| ean[fixed_fee]  | Fixed fee a year charged per EAN connection |
| ean[tariff_group]  | Values: ["mono", "dual", "monoExclusive", "dualExclusive"]. Tariff group for the EAN connection |
| ean[wkk]  | Ean wkk |
| ean[gsc]  | Ean gsc |



### Response

```plaintext
Content-Type: application/json; charset=utf-8
201 Created
```


```json
{
  "id": 5,
  "customer_id": 33,
  "number": "542170967180397340",
  "product": "electricity",
  "reason": "normal",
  "building": "15",
  "building_addon": "A",
  "street": "street name",
  "city": "Kiev",
  "state": "ready",
  "postal_code": "2443",
  "consumptions": [
    {
      "name": "mono",
      "volume": "22.25",
      "price": "0.15"
    }
  ],
  "solar_panels": true,
  "inverter_max_power": 315,
  "contract_end_date": "2020-10-07",
  "fixed_fee": "1.0",
  "tariff_group": "mono",
  "recording_period": "february",
  "wkk": "0.00341",
  "gsc": "0.0214",
  "created_at": "2020-04-07T15:28:32.131Z",
  "supplier": {
    "id": 4,
    "name": "Rice and Sons 4"
  }
}
```



#### Fields

| Name       | Description         |
|:-----------|:--------------------|
| id | ID of the EAN record |
| customer_id | ID of the customer to whom the EAN record belongs to |
| number | An EAN number of record |
| product | Values: ["gas", "electricity"]. The EAN record's product |
| reason | Values: ["normal", "new", "reopened", "dropped", "moved"]. The reason why the customer is searching for a new offer. |
| state | The current status of the EAN record |
| building | The address of the EAN connection - building |
| building_addon | The address of the EAN connection - building addon |
| street | The address of the EAN connection - street |
| city | The address of the EAN connection - city |
| postal_code | The address of the EAN connection - postal_code |
| consumptions | The consumptions of the EAN connection |
| consumptions | The consumptions of the EAN connection. |
| consumptions[name] | Name of the tariff |
| consumptions[volume] | A consumption volume by the tariff |
| consumptions[price] | A price for the tariff |
| solar_panels | Type: *boolen*. For *electricity* only. A flag that the EAN connection has solar panels. |
| inverter_max_power | Inverter Max Power. Only then solar panels flag is true |
| contract_end_date | The date when the contract for the EAN connection ends |
| fixed_fee | Fixed fee a year charged per EAN connection |
| tariff_group | Values: ["mono", "dual", "monoExclusive", "dualExclusive"]. Tariff group for the EAN connection |
| wkk |  wkk |
| gsc |  gsc |
| created_at | Date and time when the EAN record has been created |
| supplier[id] | ID of the supplier of the EAN connection |
| supplier[name] | Name of the supplier of the EAN connection |


## CREATE 422 Validation Error

          At least one of the specified parameters contains an error.
          Check if all the required parameters have been specified.
          Also the specified EAN number must be unique.
          You can find details about the error in the response.


### Request

#### Endpoint

```plaintext
POST /api/v1/customers/34/eans
Content-Type: application/json
Authorization: Bearer bb6022ef3aab11a97ee899b32503f8bc
```

`POST /api/v1/customers/:customer_id/eans`

#### Parameters


```json
{
  "ean": {
    "number": "542170967180397340",
    "product": "electricity",
    "reason": "normal",
    "supplier_id": 5,
    "building": "15",
    "building_addon": "A",
    "street": "street name",
    "city": "Kiev",
    "postal_code": "2443",
    "consumptions": [
      {
        "name": "mono",
        "volume": "22.25",
        "price": "0.15"
      }
    ],
    "recording_period": "february",
    "solar_panels": "true",
    "inverter_max_power": "315",
    "contract_end_date": "2020-10-07",
    "fixed_fee": "1.00",
    "tariff_group": "mono",
    "wkk": "0.00341",
    "gsc": "0.0214"
  }
}
```


| Name | Description |
|:-----|:------------|
| customer_id *required* | ID of the customer |
| ean *required* | Attributes for the EAN record |
| ean[number]  | EAN number |
| ean[product]  | Enum: ["gas", "electricity"]. The EAN record's product. Must be a value from the enum |
| ean[reason]  | Enum: ["normal", "new", "reopened", "dropped", "moved"]. The reason why the customer is searching for a new offer. Must be a value from the enum. |
| ean[supplier_id]  | ID of the supplier for the EAN connection |
| ean[building]  | The address for the EAN connection - building addon |
| ean[building_addon]  | The address of the EAN connection - street |
| ean[street]  | The address for the EAN connection - building |
| ean[city]  | The address of the EAN connection - city |
| ean[postal_code]  | The address of the EAN connection - postal_code |
| ean[consumptions]  | The consumptions for the EAN connection |
| ean[consumptions][name]  | Name of the tariff |
| ean[consumptions][volume]  | A consumption volume by the tariff |
| ean[consumptions][price]  | A price for the tariff |
| ean[recording_period]  | Recording period of the EAN. Enum: ["automatic", "monthly", "january", "february", "march", "april", "may", "june", "july", "august", "september", "october", "november", "december"] |
| ean[solar_panels]  | Type: *boolen*. For *electricity* only. A flag that the EAN connection has solar panels.  |
| ean[inverter_max_power]  | Inverter Max Power. Only then solar panels flag is true |
| ean[contract_end_date]  | The date when the contract for the EAN connection ends |
| ean[fixed_fee]  | Fixed fee a year charged per EAN connection |
| ean[tariff_group]  | Values: ["mono", "dual", "monoExclusive", "dualExclusive"]. Tariff group for the EAN connection |
| ean[wkk]  | Ean wkk |
| ean[gsc]  | Ean gsc |



### Response

```plaintext
Content-Type: application/json; charset=utf-8
422 Unprocessable Entity
```


```json
{
  "errors": [
    {
      "error": "has_already_been_added_to_customer",
      "message": "has already been added to customer",
      "path": "ean.number",
      "type": "params"
    },
    {
      "error": "has_already_been_taken",
      "message": "has already been taken",
      "path": "ean.number",
      "type": "params"
    }
  ]
}
```



#### Fields

| Name       | Description         |
|:-----------|:--------------------|
| errors | Type: *array*. Items type: *object*. Contains a list of occurred errors |
| path | A full name of an erroneous field |
| error | A string identifier of the error |
| message | An error message |
| type | A type of the error |


## LIST 200 OK

Returns available EAN records for the specified customer

### Request

#### Endpoint

```plaintext
GET /api/v1/customers/29/eans
Content-Type: application/json
Authorization: Bearer cedc7eff3512a209c9c86de882edd440
```

`GET /api/v1/customers/:customer_id/eans`

#### Parameters



| Name | Description |
|:-----|:------------|
| customer_id *required* | ID of the customer |



### Response

```plaintext
Content-Type: application/json; charset=utf-8
200 OK
```


```json
[
  {
    "id": 1,
    "customer_id": 29,
    "number": "545101901013606712",
    "product": "electricity",
    "reason": "normal",
    "building": "186",
    "building_addon": "Apt. 448",
    "street": "Rutherford Pines",
    "city": "Beckerport",
    "state": "ready",
    "postal_code": "58435-6582",
    "solar_panels": true,
    "inverter_max_power": 1761,
    "fixed_fee": "35.0",
    "tariff_group": "mono",
    "recording_period": "january",
    "wkk": "0.00425",
    "gsc": "0.0215",
    "created_at": "2020-04-07T15:28:31.931Z",
    "supplier": {
      "id": 1,
      "name": "Pouros, Stracke and Mraz 1"
    }
  },
  {
    "id": 2,
    "customer_id": 29,
    "number": "548455521062309731",
    "product": "electricity",
    "reason": "normal",
    "building": "94148",
    "building_addon": "Apt. 199",
    "street": "Christa Hill",
    "city": "Lake Karlaton",
    "state": "ready",
    "postal_code": "89107",
    "solar_panels": false,
    "inverter_max_power": 1559,
    "fixed_fee": "40.0",
    "tariff_group": "monoExclusive",
    "recording_period": "automatic",
    "wkk": "0.00425",
    "gsc": "0.0215",
    "created_at": "2020-04-07T15:28:31.937Z",
    "supplier": {
      "id": 1,
      "name": "Pouros, Stracke and Mraz 1"
    }
  }
]
```



#### Fields

| Name       | Description         |
|:-----------|:--------------------|
| id | ID of the EAN record |
| customer_id | ID of the customer to whom the EAN record belongs to |
| number | An EAN number of record |
| product | Values: ["gas", "electricity"]. The EAN record's product |
| reason | Values: ["normal", "new", "reopened", "dropped", "moved"]. The reason why the customer is searching for a new offer. |
| state | The current status of the EAN record |
| building | The address of the EAN connection - building |
| building_addon | The address of the EAN connection - building addon |
| street | The address of the EAN connection - street |
| city | The address of the EAN connection - city |
| postal_code | The address of the EAN connection - postal_code |
| consumptions | The consumptions of the EAN connection |
| consumptions | The consumptions of the EAN connection. |
| consumptions[name] | Name of the tariff |
| consumptions[volume] | A consumption volume by the tariff |
| consumptions[price] | A price for the tariff |
| solar_panels | Type: *boolen*. For *electricity* only. A flag that the EAN connection has solar panels. |
| inverter_max_power | Inverter Max Power. Only then solar panels flag is true |
| contract_end_date | The date when the contract for the EAN connection ends |
| fixed_fee | Fixed fee a year charged per EAN connection |
| tariff_group | Values: ["mono", "dual", "monoExclusive", "dualExclusive"]. Tariff group for the EAN connection |
| wkk |  wkk |
| gsc |  gsc |
| created_at | Date and time when the EAN record has been created |
| supplier[id] | ID of the supplier of the EAN connection |
| supplier[name] | Name of the supplier of the EAN connection |


# Customers / Eans / Bulk

All requests namespaced under /api/v1

## CREATE /eans -&gt; failure

When a customer has already an EAN with the same number

### Request

#### Endpoint

```plaintext
POST /api/v1/customers/36/eans/bulk
Content-Type: application/json
Authorization: Bearer 0d43e53e9b666e5bb7283e6dc3450ee9
```

`POST /api/v1/customers/:customer_id/eans/bulk`

#### Parameters


```json
{
  "eans": [
    {
      "ean": {
        "product": "electricity",
        "number": "542170967180397340",
        "reason": "normal",
        "supplier_id": 8,
        "street": "street name",
        "building": "15",
        "building_addon": "A",
        "postal_code": "2443",
        "city": "Kiev",
        "consumptions": [
          {
            "name": "mono",
            "volume": "22.25",
            "price": "0.15"
          }
        ],
        "fixed_fee": "1.00",
        "solar_panels": "true",
        "recording_period": "february",
        "contract_end_date": "2020-10-07",
        "respect_contract_end_date": true,
        "tariff_group": "mono",
        "gsc": "0.0214",
        "wkk": "0.00341",
        "inverter_max_power": "315"
      }
    }
  ]
}
```


| Name | Description |
|:-----|:------------|
| eans *required* |  eans |



### Response

```plaintext
Content-Type: application/json; charset=utf-8
422 Unprocessable Entity
```


```json
{
  "errors": [
    {
      "error": "has_already_been_added_to_customer",
      "message": "has already been added to customer",
      "path": "ean.number",
      "type": "params",
      "index": 0
    },
    {
      "error": "has_already_been_taken",
      "message": "has already been taken",
      "path": "ean.number",
      "type": "params",
      "index": 0
    }
  ]
}
```



## CREATE /eans -&gt; failure

when another customer already has EAN with same number

### Request

#### Endpoint

```plaintext
POST /api/v1/customers/37/eans/bulk
Content-Type: application/json
Authorization: Bearer cfbdd41a088ac6d0ab3b6c4091909486
```

`POST /api/v1/customers/:customer_id/eans/bulk`

#### Parameters


```json
{
  "eans": [
    {
      "ean": {
        "product": "electricity",
        "number": "542170967180397340",
        "reason": "normal",
        "supplier_id": 10,
        "street": "street name",
        "building": "15",
        "building_addon": "A",
        "postal_code": "2443",
        "city": "Kiev",
        "consumptions": [
          {
            "name": "mono",
            "volume": "22.25",
            "price": "0.15"
          }
        ],
        "fixed_fee": "1.00",
        "solar_panels": "true",
        "recording_period": "february",
        "contract_end_date": "2020-10-07",
        "respect_contract_end_date": true,
        "tariff_group": "mono",
        "gsc": "0.0214",
        "wkk": "0.00341",
        "inverter_max_power": "315"
      }
    }
  ]
}
```


| Name | Description |
|:-----|:------------|
| eans *required* |  eans |



### Response

```plaintext
Content-Type: application/json; charset=utf-8
422 Unprocessable Entity
```


```json
{
  "errors": [
    {
      "error": "has_already_been_taken",
      "message": "has already been taken",
      "path": "ean.number",
      "type": "params",
      "index": 0
    }
  ]
}
```



## CREATE /eans -&gt; success

Create EAN batch

### Request

#### Endpoint

```plaintext
POST /api/v1/customers/35/eans/bulk
Content-Type: application/json
Authorization: Bearer 51b3d886b405e2aa55de7134853734af
```

`POST /api/v1/customers/:customer_id/eans/bulk`

#### Parameters


```json
{
  "eans": [
    {
      "ean": {
        "product": "electricity",
        "number": "542170967180397340",
        "reason": "normal",
        "supplier_id": 7,
        "street": "street name",
        "building": "15",
        "building_addon": "A",
        "postal_code": "2443",
        "city": "Kiev",
        "consumptions": [
          {
            "name": "mono",
            "volume": "22.25",
            "price": "0.15"
          }
        ],
        "fixed_fee": "1.00",
        "solar_panels": "true",
        "recording_period": "february",
        "contract_end_date": "2020-10-07",
        "respect_contract_end_date": true,
        "tariff_group": "mono",
        "gsc": "0.0214",
        "wkk": "0.00341",
        "inverter_max_power": "315"
      }
    }
  ]
}
```


| Name | Description |
|:-----|:------------|
| eans *required* |  eans |



### Response

```plaintext
Content-Type: application/json; charset=utf-8
201 Created
```


```json
[
  {
    "id": 7,
    "customer_id": 35,
    "number": "542170967180397340",
    "product": "electricity",
    "reason": "normal",
    "building": "15",
    "building_addon": "A",
    "street": "street name",
    "city": "Kiev",
    "state": "ready",
    "postal_code": "2443",
    "consumptions": [
      {
        "name": "mono",
        "volume": "22.25",
        "price": "0.15"
      }
    ],
    "solar_panels": true,
    "inverter_max_power": 315,
    "contract_end_date": "2020-10-07",
    "fixed_fee": "1.0",
    "tariff_group": "mono",
    "recording_period": "february",
    "wkk": "0.00341",
    "gsc": "0.0214",
    "created_at": "2020-04-07T15:28:32.287Z",
    "supplier": {
      "id": 7,
      "name": "Runte Group 7"
    }
  }
]
```



