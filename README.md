# Data Product Specification (DPS)

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL"
in this document are to be interpreted as described in [RFC 2119](http://www.ietf.org/rfc/rfc2119.txt).


## Revision History

|Version  | Date         | Notes                  |
|:------- |:------------ |:---------------------- |
| 0.1     | 2019-11-22   | Initial draft.         |

## 1. Introduction
**Data Product Specification (DPS)** is an open source standard for describing Data Products.

This DPS definition in a vendor neutral and intented to fostering innovation in the area where data is exposed for internal or public use as data products. Open data movemment began the data exposure, but it lacks the commercial aspects of data products. Since a specification for the data product has been missing, Platform of Trust decided to ignite open process to define one shared specification and understanding of what is data product.  

## 2. DPS Document Schema

Top level attributes and objects. The root level objects are defined under separate chapters after the main level.   

Implementation of the specification might include namespaces which are included in the examples below. 


| Field Name     | Type                                                                 | Description  |
| :------------- | :------------------------------------------------------------------- | :----------- |
| identityId             | `string`                                                             | **Required** The identification of the Data Product context. Generated by the platform |
| type        | `string`                                                             | **Required** Options: `DataProduct`, `StandardDataProduct`  |
| version        | `string`                                                             | **Required** Indicates the version of the data product format `='1.0'`. |
| connector            | `object`                                                                | **Required** Define the service component which handles the data requests and data transformations |
| provider       | `object`                                                             | **Required** Provider information: data about the owner/host of the data product. |
| SLA            | `object`                                                             | **Required** SLA levels and details |
| imageUrl       | `uri`                                                             | **Required** Logo URL (absolute) of the data product. |
| description      | `string`                                                             | **Required** Description of the data product. |


```
{
  "product": {
    "type": "StandardDataProduct",
    "id": "31b5b971-dc50-4c9c-992a-57c0bf016186",
    "description: "Free text, long text, define max length in specification",
    "version": 1,
    "infrastructure": {
      ...
    },
    "provider": {
      ...
    },
    "SLA": {
      ...
    }
  }
}
```

### 2.4. SlaObject

SLA Object
The SLA Object must conform to the following constraints.

| Field Name     | Type                                                                 | Description  |
| :------------- | :------------------------------------------------------------------- | :----------- |
| infrastructure | [`InfrastructureObject`](#524-infrastructureobject)  | **Required** Provides information about tooling used for SLA storage, calculation, governance, etc. |
| pricing        | [`PricingObject`](#525-pricingobject)                | **Optional** Global pricing data. |
| metrics        | [`MetricsObject`](#526-metricsobject)                | **Required** A list of metrics to use in the context of the SLA. |
| plans          | [`PlansObject`](#528-plansobject)                    | **Optional** A set of plans to define different service levels per plan. |
| quotas         | [`QuotasObject`](#5210-quotasobject)                  | **Optional** Global quotas, these are the default quotas, but they could be overridden by each plan later. |


### 2.1. ProviderObject

Object element. 


| Field Name     | Type                                                                 | Description  |
| :------------- | :------------------------------------------------------------------- | :----------- |
| identityId             | `string`                                                             | **Required** The identification of the Data Product context. Generated by the platform |

JSON example: 

```
{
  "dataproduct": {
    
  }
}
```


### 2.5. InfrastructureObject

The infrastructure object describes the operational tooling to use in the service execution.

| Field Name     | Type          | Description  |
| :------------- | :------------:| :------------|
| supervisor     | `uri`         | **Required** Location of the SLA Check service accordingly to the [Basic SLA Management Service](./operationalServices.md) spec. |
| monitor        | `uri`         | **Required** Location of the SLA Metrics endpoint accordingly to the [Basic SLA Management Service](./operationalServices.md) spec. |
| connectors        | `object`         | **Required** Connector component. |

**Example:**

```
{
   "infrastructure":{
      "supervisor": "http://supervisor.sla4oai.governify.io/v1/",
      "monitor": "http://platformoftrust.statuspage.io"
      "connectors: {
      ...
      }
   }
}
```

### 2.5. ConnectorsObject

The connectors object describes the needed connector component details.

| Field Name     | Type          | Description  |
| :------------- | :------------:| :------------|
| connectorId     | `string`         | **Required** Global Unique Identitifer within platform |
| connectorUrl        | `uri`         | **Required** Location of the connector API endpoint  |


**Example:**

```
{
   "infrastructure":{
      "connector": {
        "connectorId": "31b5b971-dc50-4c9c-992a-57c0bf016186",
        "connectorUrl": "https..."
      }
   }
}
```



### 2.2. PlansObject

Contains a list of plans describing different levels of service and prices.

| Field Name  | Type                                            | Description  |
| :------------- | :---------------------------------------------- | :----------- |
| planType     | `string`                                          | Describes higher level type of plan, subscribe or pay as you go |
| planName     | `string`                                          | Sub type of plan |

**Example:**

```
plans:
  subscription:
    freemium:
      pricing:
      quotas:
        requests:
          - max: 50 000
          - period: monthly
    pro:
      pricing:
      quotas:
        cost: 50
           requests:
             - max: 200 0000
             - period: monthly
  pay-as-you-go:
    single:
      pricing:
      quotas:
        requests:
          - max: 1
```

### 2.3. PricingObject
Describes the general information of the pricing of the Data Product.

| Field Name     | Type          | Description  |
| :------------- | :------------:| :------------|
| cost           | `number`      | **Optional** Cost associated with this service. Defaults to `0` if unspecified. |
| currency       | `string`      | **Optional** Currency used to express the cost. Supported currency values are expressed in ISO 4217 format. Samples: `USD`, `EUR`, or `BTC` for US dollar, euro, or bitcoin, respectively. Defaults to `EUR` if unspecified. |
| billing        | `string`      | **Optional** Period used for billing. Supported values are: - `onepay` Unique payment before start using the service. - `daily` Billing at end of the day. - `weekly` Billing at end of the week. - `monthly` Billing at end of the month. - `quarterly` Billing at end of the quarter. -  `yearly` Billing at end of the year. Default to `monthly` if unspecified. |

**Example:**

```
{
   "pricing":{
      "cost": 0,
      "currency": "euro",
      "billing": "monthly"
   }
}
```

```
pricing:
  cost: 0
  currency: "euro"
  billing: "monthly"
```



## Samples
