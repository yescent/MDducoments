# Comm100 API
# Resource List 
|Name|EndPoint|Note| 
|---|---|---| 
|[Contact](#contact)|/api/v2/account/contacts|for contact| 
|[Agent](#agent)|/api/v2/account/agents|for agent|

# Contact
## objects
### contact
| Name | Type | Description |
| - | - | - |
| `id` | integer | id of the contact |
| `name` | string |  the name of the contact |
| `alias` | string |  the alias name of the contact |
| `identities` | [identity](#identity)[] | identity array  |
| `description` | string | a small description of the contact |
| `company` | string | the primary company name to which this contact belongs|
| `title` | string | the title of the contact|
| `phoneNumber` | string | telephone number of the contact|
| `faxNumber` | string | fax number of the contact |
| `address` | string | the address of the contact  |
| `city` | string | the city of the contact  |
| `stateOrProvince` | string | the state or province of the contact |
| `country` | string |  the country of the contact |
| `postcode` | string | the postcode of the contact  |
| `createTime` | datetime | the time the contact was created |
  
### identity
| Name | Type | Description | 
| - | - | - | 
| `id` | integer | the id of identity |
| `type` | string | `email`, `SSOUserId`, `externalId` |
| `value` | string | the value of this identity, should be unique in the|

- Note: We currently only allow one for each type.

### endpoints
#### Get a contact by contact id
`get  /api/v2/account/contacts/{id}`
- Parameters
    - id: integer, id of the contact
- Response
    - [contact object](#contact)

#### Create a contact
`post  /api/v2/account/contacts`
- Parameters 

| Name | Type | Description |
| - | - | - |
| `name` | string |  the name of the contact |
| `alias` | string |  the alias name of the contact |
| `identities` | [identity](#identity)[] | the array of identities |
| `description` | string | a small description of the contact |
| `company` | string | the primary company name to which this contact belongs |
| `title` | string | the title of the contact |
| `phoneNumber` | string | telephone number of the contact|
| `faxNumber` | string | fax number of the contact |
| `address` | string | the address of the contact  |
| `city` | string | the city of the contact  |
| `stateOrProvince` | string | the state or province of the contact |
| `country` | string |  the country of the contact |
| `postcode` | string | the postcode of the contact  |

- Response
    - [contact object](#contact)

#### Search contacts
- Max 50 contacts are responded for each request.
- `get  /api/v2/account/contacts`
- Parameters
    - pageIndex, integer, default 1
    - email, string, optional
    - SSOUserId, string, optional
    - externalId, string, optional
    - alias, string, optional
    - company, string, optional
    - title, string, optional
    - phoneNumber, string, optional
    - faxNumber, string, optional
    - address, string, optional
    - country, string, optional
    - stateOrProvince, string, optional
    - city, string, optional
- Response
    - contacts: [contact object](#contact) list
    - total: int, total number of contacts.
    - previousPage: string, next page uri, the first page return null.
    - nextPage: string, the last page return null.
    - currentPage: string, current page uri.
- Example
    - <code>get  /api/v2/contact/contacts?country=canada&company=test`</code>
- Note
    - Deleted contact will not be included in the results.
    - The query must be URL encoded.
    - Fuzzy search is not supported.

#### Update a contact
`put  /api/v2/account/contacts/{id}`
- Parameters

| Name | Type | Description |
| - | - | - |
| `name` | string |  the name of the contact |
| `alias` | string |  the alias name of the contact |
| `description` | string | a small description of the contact |
| `company` | string | the primary company name to which this contact belongs|
| `title` | string | the title of the contact|
| `phoneNumber` | string | telephone number of the contact|
| `faxNumber` | string | fax number of the contact |
| `address` | string | the address of the contact  |
| `city` | string | the city of the contact  |
| `stateOrProvince` | string | the state or province of the contact |
| `country` | string |  the country of the contact |
| `postcode` | string | the postcode of the contact |

- Response
    - [contact object](#contact)

#### Delete a contact
 `delete  /api/v2/account/contacts/{id}`
- Parameters
    - id: integer, id of the contact
- Response
    - http status code and message

#### Add contact identity
`post  /api/v2/account/contacts/{contactId}/identities`
- Parameters
    - contactId: integer, contact id
    - type: string, identity type
    - value: string, identity value
- Response
    - [identity object](#identity)

#### Update contact identity
`put  /api/v2/account/contacts/{contactId}/identities/{id}`
- Parameters
    - contactId, integer, contact id
    - id, integer, contact identity id
    - value, string, the value of the identity
- Response
    - [identity object](#identity)

#### Delete contact identity
 `delete  /api/v2/account/contacts/{contactId}/identities/{id}`
- Parameters
    - contactId, integer, contact id
    - id, integer, contact identity id
- Response
    - http status code and message

# Agent
[Reference document](https://www.comm100.com/doc/api/introduction.htm#/Account?id=agent-json-format)