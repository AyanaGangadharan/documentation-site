{
  "title": "HotelSearch",
  "description": "",
  "weight": 1,
  "fields": [
    {
      "typeString": "String",
      "name": "context",
      "url": "/hotel-x/reference/scalars/string",
      "description": null,
      "isDeprecated": false,
      "args": null
    },
    {
      "typeString": "StatsRequest",
      "name": "stats",
      "url": "/hotel-x/reference/objects/statsrequest",
      "description": null,
      "isDeprecated": false,
      "args": [
        {
          "typeString": "String!",
          "name": "token",
          "url": "/hotel-x/reference/scalars/string",
          "description": null
        }
      ]
    },
    {
      "typeString": "AuditData",
      "name": "auditData",
      "url": "/hotel-x/reference/objects/auditdata",
      "description": null,
      "isDeprecated": false,
      "args": null
    },
    {
      "typeString": "CriteriaSearch",
      "name": "requestCriteria",
      "url": "/hotel-x/reference/objects/criteriasearch",
      "description": null,
      "isDeprecated": false,
      "args": null
    },
    {
      "typeString": "[HotelOptionSearch!]",
      "name": "options",
      "url": "/hotel-x/reference/objects/hoteloptionsearch",
      "description": null,
      "isDeprecated": false,
      "args": null
    },
    {
      "typeString": "[Error!]",
      "name": "errors",
      "url": "/hotel-x/reference/objects/error",
      "description": null,
      "isDeprecated": false,
      "args": null
    },
    {
      "typeString": "[Warning!]",
      "name": "warnings",
      "url": "/hotel-x/reference/objects/warning",
      "description": null,
      "isDeprecated": false,
      "args": null
    }
  ],
  "requireby": [
    {
      "name": "HotelXQuery",
      "description": null,
      "url": "/hotel-x/reference/objects/hotelxquery"
    }
  ],
  "enumValues": null,
  "operator": "type",
  "typename": "HotelSearch",
  "hideGithubLink": true
}
## GraphQL schema definition

{{% graphql-schema-type %}}

## Fields

{{% graphql-field %}}

## Required by

{{% graphql-require-by %}}
