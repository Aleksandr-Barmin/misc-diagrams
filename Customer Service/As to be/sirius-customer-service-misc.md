# Endpoitns in use and their responsibilities

* GET   +   /customers - get all the customers with pagination
* GET   +   /customers?email={email} - get all the customers by name with pagination
* POST  +   /customers - create a new customer in the Accounts table
* PUT   +   /customers/{customerId} - update an existing customer in the Accounts table
* GET   +   /customers/{customerId}/businesses - get list of business associated with the customer, Business entity
* POST  +   /customers/{customerId}/businesses - add a business to the customer, Business entity
* PATCH +   /businesses/{businessId} - update the business, Business entity
* GET   +   /customers/{customerId}/persons - get a person associated with the given {customerId}, single person, actually, Accounts table
* POST  +   /customers/{customerId}/persons - actually, updates fields in the Accounts table from PersonDTO
* PATCH +   /customers/{customerId}/persons/patch - patch, the same table Accounts, updates from PersonPatchDTO
* PATCH ?   /customers/{customerId}/persons/ddv-review-patch - legacy person service, patch Accounts table
* POST  ?   /customers/{customerId}/check-existing-customer - reads from the Accounts table

# Conclusions

* All the endpoints which are currently in use are dealing with the Accounts table so that one single service in order not to split the data. So that there is no need to have both the controllers. 
* In accordance with the DD, the Customer entity has no own fields but all the data is in the Person entity.
* Organization -> Business. 

In this case, split across controllers is the following: 

* CustomerController
    * GET       /v1/customers/{customerId}          Customer from DD with Person, Organization, etc inside
    * GET       /v1/customers?email={email}       CustomerDTO
    * POST      /v1/customers                   CustomerDTO
    * PATCH     /v1/customers/{customerId} 
    *? PUT      /v1/customers/{customerId}      CustomerDTO

v1/customers/person/{personId}
v1/customers/organization

* OrganizationController

    * GET       /v1/organizations/{organizationId}  Organization from DD
    * POST      /v1/organizations
    * PATCH     /v1/organizations/{organizationId}

# Questions

* Organization can have multiple people

# Tables

* `Customers` with all the necessary dependencies
* `Organizations` with all the necessary dependencies

# On Aleks

* Technical design: controller + services + repos
* DB schema in diagrams
* Migration from as is to as to be - list of actions to be undertaken for migration

# On Catarina

* API definition - endpoints/methods/fields in R/R

# On Deepa

* Sequence diagrams for to be