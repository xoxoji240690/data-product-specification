# Data Product Example

A data product consists of six different entities: product, service, price plan, condition, quality and connector. The properties that belong to them are described in more detail in each of the sections.

Below is the example of DataProduct. Entitites definitions can be found in respective subpages.

```json
{
   "condition":[
      {
         "name":"Reselling limitation",
         "descriptionGeneral":"Information cannot be sold further. Only to be used within buying organization",
         "categorizationLocal":"usage",
         "categorizationPoT":"dataProduct"
      }
   ],
   "priceplan":[
      {
         "name":"Organization contact information - Finland",
         "currency":"euro",
         "unit":"monthly, quantity",
         "unitGroup":"subscription, transaction",
         "vatIncluded":"",
         "vatPercentge":""
      }
   ],
   "quality":[
      {
         "name":"Information updating",
         "categorizationLocal":"Update frequancy",
         "categorizationPoT":"dataProduct",
         "descriptionGeneral":"Information is updated once per day"
      }
   ],
   "service":[
      {
         "name":"Phone support hours",
         "descriptionGeneral":"Support is available between 08-16 weekdays.",
         "categorizationLocal":"Support",
         "categorizationPoT":"dataProduct"
      }
   ],
   "product":{
      "categorizationPoT":"dataProduct",
      "descriptionGeneral":"xxxxxxxxxxx",
      "name":"Organization contact information",
      "ontologyDefinition":{
         "version":"2.0",
         "versionHistory":[
            "1.2",
            "2.0"
         ],
         "requestContext":"https://standards-ontotest.oftrust.net/v2/Context/DataProductParameters/ProductCatalog/",
         "responseContext":"https://standards-ontotest.oftrust.net/v2/Context/DataProductOutput/ProductCatalog/"
      },
      "visibility":"organisation, public",
      "validFrom":"2020-01-01",
      "validTo":"2020-12-31"
   },
   "connector":[
      {
         "name":"Connector",
		 "description": "Connector for organization contact information.",
         "version":"2.0",
         "uri":"https://connector.com/api/methodname",
         "supportedOntologyVersion":[
            "1.0",
            "2.0"
         ]
      },
      {
         "name":"Connector2",
		 "description": "Connector for organization contact information 2."
         "version":"3.0",
         "uri":"https://connector.com/api/methodname",
         "supportedOntologyVersion":[
            "1.0"
         ]
      }
   ]
}
```