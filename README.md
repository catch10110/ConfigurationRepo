# DHX Configuration Repo
In this project we will manage all configuration for all our microservices under DHX project. The Spring Cloud Config server will be configured to read properties from this repo for each microservice at runtime.

## Global Properties
If you would like to add properties that are global in nature, meaning all microservices will be able to inherit automatically, you should add them to `application.properties` file.

## Microservice Properties
All our microservices will support only these four profiles:
  - default
  - integration
  - staging
  - production
  
Default profile is the one Spring Boot will use by default if profile(s) are not provided. Spring will load all properties from `${project_name}.properties` in this repo.

The other three profiles, Spring Boot will try to request `${project_name}-${profile}.properties`. So if the instance is running with profile: `integration`, the `${project_name}-integration.properties` file will be loaded automatically.

## Multiple Profiles
When running Spring Boot microservices, we can specify one or more profiles that we would like to load.

`--spring.profiles.active=default,integration`

With this approach, Spring Boot will make sure to load two property files in this order:

  `${project_name}.properties`
  `${project_name}-integration.properties`
  
This allows us to have a common set of properties under `${project_name}.properties` and only override keys as needed in the other environments, `integration`, `staging`, `production`.
