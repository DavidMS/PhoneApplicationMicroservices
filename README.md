# PhoneApplicationMicroservices

Repository with two microservices (Phone Catalog and Order Service), a Zuul Server and an Eureka Server configured to work together.

# Phone Catalog
The phone catalog service represents a phone catalog. It uses an H2 in memory database with an initial load of two phones with ids 1 and 2. The phone catalog api exposes two services:
  - ValidateOrder (/phone/validateOrder) that recieves a list of phones ids and validates if all the phones exists in the database. Returns true if so and false if not.
  - GetTotalPrice (/phone/getTotalPrice) that recieves a list of phones ids and returns the sum of all its prices.

# Order Service
The order service uses the phone catalog service to validate a given order and calculate the total price of the order. The Order Service exposes two services:
 - ValidateOrder (/order/validateOrder) that recieves an Order object and validates it using the Phone Catalog service. An order is considered valid if all the phones in it exists in the Phone Catalog database.
  - CalculateOrder (/order/calculateOrder) that recieves an Order object and calculates its total price using the Phone Catalog service, then logs it in the Console (info) and returns the order as a JSON.
    
# Common Features
- The microservices are meant to use Eureka Server, so for them to work Eureka Server must be up and running. In order to avoid this Step, eureka dependencies and annotations must be removed.
- The microservices are meant to communicate to each other using zuul gateway server. In order to avoid this step, propertie zuul.url must be overwritten in orderService application.properties
- Both microservices come with Swagger integration. Using zuul and eureka, swagger can be accessed through respective address:
    - http://localhost:8008/order-service/swagger-ui.html (order service)
    - http://localhost:8080/phonecatalog/swagger-ui.html (phone catalog)

# Integration Testing
- Order Service: in order to run Integration Tests for Order Service: Eureka Server, Zuul Server and PhoneCatalog service must be up and running.
- Phone Catalog: in order to run Integration Tests for Phone Catalog: Eureka Server must be up and running.

# Future Features
Due to a lack of time and resources the following features/tests hasn't been yet implemented/executed:
- Cloud Configuration Service.
- Docker Testing (I haven't been able to test docker images on my computer).
- Kubernettes Testing (I haven't been able to test the system using kubernettes).
- Securing RestApis
- Testing RestTemplate
- Order Service Database (optional since there is no need for the required functionality)
