## BRIGHT APIs V2 Specification

<br>

> ### APIs Requirement List
- [x] POST Login
- [x] POST Register
- [x] POST Forgot Password
- [x] POST Personalize
- [x] GET Personalize
- [x] GET Selection Menu
- [x] GET Insight Data
- [ ] GET Single Chart Data
- [x] GET Prescriptive
- [x] POST Feedback
- [x] GET FAQ
- [x] GET About
- [x] GET Bright Team

<br>

> ### API Base Url
| Google Cloud | Heroku |
| - | - |
| https://telkombright.com/api/v2 | https://telkom-bpp-bright.herokuapp.com/api/v2 |

<br>

> ### POST Login

| Method | Route |
| - | - |
| POST | /login |

#### Request:
```
{
  "nik" : "String or integer",
  "password": "String"
}
```

#### Responses:
```
{
    "error": boolean,
    "message": "String",
    "user": {
        "id": integer,
        "full_name": "String",
        "band": "String",
        "nik": "String",
        "email": "String",
        "is_email_verified": boolean,
        "phone_number": "String",
        "position_name": "String",
        "locker_name": "String",
        "city_name": "String",
        "sub_unit_name": "String",
        "unit_name": "String",
        "witel": "String",
    },
    "token": "token"
}
```

<br>

> ### POST Register

| Method | Route |
| - | - |
| POST | /register |

#### Request:
```
{
  "nik" : "String or integer",
  "phone_number" : "String",
  "email" : "String",
  "password": "String"
}
```

#### Responses:
```
{
    "error": boolean,
    "message": "String",
    "user": {
        "id": integer,
        "full_name": "String",
        "band": "String",
        "nik": "String",
        "email": "String",
        "is_email_verified": boolean,
        "phone_number": "String",
        "position_name": "String",
        "locker_name": "String",
        "city_name": "String",
        "sub_unit_name": "String",
        "unit_name": "String",
        "witel": "String",
    },
    "token": "token"
}
```

<br>

> ### POST Forgot Password

| Method | Route |
| - | - |
| POST | /forgotPassword |

#### Request:
```
{
  "nik" : "String or integer",
  "email" : "String",
}
```

#### Responses:
```
{
    "error": boolean,
    "message": "String",
}
```

<br>

> ### Get Selection Menu

| Method | Route | Parameters |
| - | - | - |
| GET | /menu | <u>Optional</u> regional=String 

#### Header:
```
{
  "Content-Type" : "application/json",
  "Authorization": "Bearer <token>"
}
```

#### Responses:
```
{
    "error": boolean,
    "message": "String",
    "updated_at": "datetime"
    "data": [
        {
            "name": "String",
            "values": [
                {
                    "id": integer,
                    "name": "String",
                },
                ...
            ],
        },
        ...
    ]
}
```

<br>

> ### Post Personalize

| Method | Route |
| - | - |
| POST | /personalize |

#### Request:
```
{
  "user_id" : "String or integer",
  "regional": "String",
  "witel": "String",
  "category": "String",
}
```

#### Responses:
```
{
    "error": boolean,
    "message": "String",
    "data": {
        "user_id" : "String or integer",
        "regional": "String",
        "witel": "String",
        "category": "String",
    },
}
```
<br>

> ### Get Personalize

| Method | Route | Parameter |
| - | - | - |
| GET | /personalize?userId=integer | <u>Required</u> userId=integer |

#### Header:
```
{
  "Content-Type" : "application/json",
  "Authorization": "Bearer <token>"
}
```

#### Responses:
```
{
    "error": boolean,
    "message": "String",
    "updated_at": "datetime"
    "data": {
        "regional": "String",
        "witel": "String",
        "category": "String",
    }
}
```

<br>

> ### Get Insight Data

| Method | Route | Parameters |
| - | - | - |
| GET | /descDiag?regional=String&Optional Parameter | <u>Required</u> regional=String <br> <u>Optional</u> witel=String <br> <u>Optional</u> year=String <br> <u>Optional</u> category=String default is all 

#### Header:
```
{
  "Content-Type" : "application/json",
  "Authorization": "Bearer <token>"
}
```

#### Responses:
```
{
    "error": boolean,
    "message": "String",
    "updated_at": "datetime",
    "requests": {
        "regional": "String",
        "witel": "String",
        "year": "String",
        "category": "String",
    },
    "data": [
        {
            "title": "New Sales",
            "type": "SSL",
            "yoy": {
                "2019": [
                    {
                        "year": "String",
                        "month_number": "String",
                        "total": "String",
                    },
                    ...
                ],
                "2020": [
                    {
                        "year": "String",
                        "month_number": "String",
                        "total": "String",
                    },
                    ...
                ]
            },
            "target": {
                "realisasi": [
                    {
                        "year": "String",
                        "month_number": "String",
                        "total": "String",
                    },
                    ...
                ],
                "target": [
                    {
                        "year": "String",
                        "month_number": "String",
                        "total (tgtbi)": "String",
                        "tgtytd": "String",
                        "tgtthi": "String",
                    },
                    ...
                ]
            },
            "racing": [
                {
                    "witel": "DENPASAR",
                    "ach_ytd": "String",
                },
                ...
            ],
            "diagnostic": {
                "id": 168,
                "year": "2020",
                "month_number": "12",
                "values": [
                    {
                        "label": "String",
                        "value": "String"
                    },
                    ...
                ],
            },
            "detail": {
                "year": "String",
                "month_string": "String",
                "ct0": "String",
                "cabut": "String",
                "aps": "String",
                "dunning": "String",
                "abon": "String",
                "othr": "String"
            }
        },
        ...
    ]
}
```

<br>

> ### Get Single Chart Data

| Method | Route | Parameters |
| - | - | - |
| GET | /descDiag?regional=String&Optional Parameter | <u>Required</u> regional=String <br> <u>Required</u> type={yoy, target, racing} <br> <u>Optional</u> witel=String <br> <u>Optional</u> year=String <br> <u>Optional</u> category=String default is all 

#### Header:
```
{
  "Content-Type" : "application/json",
  "Authorization": "Bearer <token>"
}
```

#### Responses:
```
{
    "error": boolean,
    "message": "String",
    "updated_at": "datetime",
    "requests": {
        "regional": "String",
        "witel": "String",
        "year": "String",
        "category": "String",
        "type": "String",
    },
    "data": <dynamic responses>
}
```

#### Dynamic responses

#### YoY responses

```
{
    "2019": [
        {
            "year": "String",
            "month_number": "String",
            "total": "String",
        },
        ...
    ],
    "2020": [
        {
            "year": "String",
            "month_number": "String",
            "total": "String",
        },
        ...
    ]
}
```

##### Target Responses

```
{
    "realisasi": [
        {
            "year": "String",
            "month_number": "String",
            "total": "String",
        },
        ...
    ],
    "target": [
        {
            "year": "String",
            "month_number": "String",
            "total (tgtbi)": "String",
            "tgtytd": "String",
            "tgtthi": "String",
        },
        ...
    ]
}
```

#### Racing Responses

```
[
    {
        "witel": "DENPASAR",
        "ach_ytd": "String",
    },
    ...
]
```

<br>

> ### Get Prescriptive Data

| Method | Route | Parameters |
| - | - | - |
| GET | /precriptive?regional=String&Optional Parameter | <u>Required</u> regional=String <br> <u>Optional</u> witel=String <br> <u>Optional</u> year=String <br> <u>Required if year is not null</u> month=String

#### Header:
```
{
  "Content-Type" : "application/json",
  "Authorization": "Bearer <token>"
}
```

#### Responses:
```
{
    "error": boolean,
    "message": "String",
    "updated_at": "datetime",
    "data": {
        "year": "String",
        "month_number": "String",
        "month_string": "String",
        "summary": [
            {
                "label": "String",
                "value": integer
            },
            ...
        ],
        "recommendation": [
            {
                "value": "String"
            },
            ...
        ]
    }
}
```


<br>

> ### Get About

| Method | Route |
| - | - |
| GET | /about |

<br>

#### Header:
```
{
  "Content-Type" : "application/json",
  "Authorization": "Bearer <token>"
}
```

#### Responses:
```
{
    "error": boolean,
    "message": "String",
    "updated_at": "datetime",
    "data": {
        "about": "String",
    }
}
```

<br>

> ### Post Feedback

| Method | Route |
| - | - |
| POST | /feedback |

#### Request:
```
{
  "user_id" : "String or integer",
  "regional" : "String",
  "witel" : "String",
  "subject": "String"
  "message": "String"
}
```

#### Responses:
```
{
    "error": boolean,
    "message": "String",
    "data": {
        "user_id" : "String or integer",
        "regional" : "String",
        "witel" : "String",
        "subject": "String"
        "message": "String"
    }
}
```

<br>

> ### Get FAQ

| Method | Route |
| - | - |
| GET | /faqs |

#### Header:
```
{
  "Content-Type" : "application/json",
  "Authorization": "Bearer <token>"
}
```

#### Responses:
```
{
    "error": boolean,
    "message": "String",
    "data": [
        {
            "question": "String",
            "answers": [
                {
                    "value": "String",
                    "child": [
                        {
                            "value": "String",
                        }
                    ],
                },
                ...
            ],
        },
        ...
    ],
}
```

<br>

> ### Get Bright Team

| Method | Route |
| - | - |
| GET | /teams |

#### Header:
```
{
  "Content-Type" : "application/json",
  "Authorization": "Bearer <token>"
}
```

#### Responses:
```
{
    "error": boolean,
    "message": "String",
    "data": [
        {
            "name": "String",
            "team_position": "String",
            "telkom_position": "String",
            "image_url": "String",
        },
        ...
    ],
}
```
