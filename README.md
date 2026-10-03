# CST8915 Lab 2 - 12-Factor App and Azure Deployment

## Demo Video

YouTube Demo: [https://youtu.be/-CJsd2BWZ_I]

## Service Repositories

- Order Service: https://github.com/Justin-algonquin/order-service
- Product Service: https://github.com/Justin-algonquin/product-service
- Store Front: https://github.com/Justin-algonquin/store-front

## Reflection Questions

### 1. What changes did you make to the order-service and product-service to comply with the Configurations and Backing Services factors of the 12-Factor App methodology?

I moved the configuration values outside of the application code and used environment variables. The order-service uses an environment variable for the RabbitMQ connection string and the port. The product-service also uses an environment variable for its port. RabbitMQ runs on a separate Azure VM and the order-service connects to it as an external backing service. The local .env files are ignored by Git so that configuration and sensitive information are not stored in the repositories.

### 2. Why is it important to use environment variables instead of hard-coding configurations in your application?

Environment variables make the application easier and safer to configure. The same code can run in different environments without changing the source code. For example, the IP addresses, ports, and RabbitMQ connection information can be changed without modifying the application. It also helps to keep sensitive information such as passwords out of the GitHub repository.

### 3. Why is it important to have separate repositories for each microservice? How does this help maintain independence and scalability of each service?

Separate repositories allow each microservice to be developed, updated, and deployed independently. A change in one service does not require changing the other services. It also makes it easier to manage dependencies and scale only the service that needs more resources. In this lab, the order-service, product-service, and store-front each have their own repository and can run independently on separate Azure VMs.

## Deployment

The application is deployed across four separate Azure virtual machines:

- Store Front VM
- Order Service VM
- Product Service VM
- RabbitMQ VM

The Store Front communicates with the Order Service and Product Service using environment variables. The Order Service connects to RabbitMQ running on its dedicated VM.
