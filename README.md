# Essential Insurance's lead integration guide

> :warning: **Before following the guide, you need a**:

- Source code

- Endpoint

- API key

> :clipboard: **Before following the guide, you need to provide**:

- A list of IPv4 addresses to whitelist

___

## Info

Requests are sent via HTTP/1.1 encoded as JSON. We have the capacity to support other protocols and encoding and this can be discussed with your contact.

You can see example requests and responses in the examples directory.

___

### Possible response messages

| Message                | HTTP status code | Resolution                                                                                              |
|------------------------|------------------|---------------------------------------------------------------------------------------------------------|
| Invalid request body.  |        404       | Check the Content-Type header is set to ```application/json```. If so, check the format of your values. |
| Unauthorized.          |        401       | Check the ```'api_key'``` field is in the request body.                                                 |
| Forbidden.             |        403       | Get in touch with your account manager.                                                                 |
| {field}: invalid       |        404       | Check that the ```{field}``` in the message is valid and formatted correctly.                           |
| Unable to handle lead. |        500       | Something has gone wrong on our end. Your request was ok.                                               |

___

### Response fields

| Field   | Type     | Description |
|----------|---------|------------------------------------------------------|
| status   | int     | The status code (also mapped into HTTP status code). |
| accepted | boolean | If the lead was accepted.                            |
| id       | string  | The unique ID (uuid v4) of the lead.                 |
| message       | string  | A message describing the error if there was one.                 |

___

### Field list

| Field                    | Type                                                                                                                                          | Description                                                               | Required           |
|--------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------|--------------------|
| api_key                  |                                                                     string                                                                    | The API key provided by your account manager.                             | :white_check_mark: |
| provider.source          |                                                                      int                                                                      | The source code provided by your account manager.                         | :white_check_mark: |
| provider.reference       |                                                                     string                                                                    | Your unique lead identifier.                                              | :x:                |
| provider.created         |                                                              timestamp (rfc3339)                                                              | The timestamp of when you created the lead. Example: 2021-08-09T21:13:00Z | :white_check_mark: |
| provider.note            |                                                                     string                                                                    | A note for the lead you're sending.                                       | :x:                |
| applicant.title          | string (enum) Mr     Mrs     Miss     Ms     Dr     Prof     Rev     Sgt     LCpl     CPL     Major     Sir     Lady     Lord     Drm     Drf | The title of the applicant.                                               | :white_check_mark: |
| applicant.first_name     | string                                                                                                                                        | The first name of the applicant.                                          | :white_check_mark: |
| applicant.last_name      | string                                                                                                                                        | The last name of the applicant.                                           | :white_check_mark: |
| applicant.dob            | timestamp (rfc3339)                                                                                                                           | The dob of the applicant.                                                 | :white_check_mark: |
| term                     | int                                                                                                                                           | The requested policy term.                                                | :white_check_mark: |
| cover.type               | string                                                                                                                                        | The type of cover.                                                        | :white_check_mark: |
| cover.amount             | string                                                                                                                                        | The requested cover amount.                                               | :white_check_mark: |
| contact.address_line_one | string                                                                                                                                        | The first line of the address.                                            | :white_check_mark: |
| contact.postcode         | string                                                                                                                                        | The postcode of the address.                                              | :white_check_mark: |
| contact.numbers.home | string | The home telephone number of the lead. | :x: |
| contact.numbers.mobile | string | The mobile telephone number of the lead. | :x:                |
| contact.numbers.work   | string | The work telephone number of the lead.   | :x:                |
| contact.email_address  | string | The email address of the lead.           | :white_check_mark: |