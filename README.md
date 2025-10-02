# Service Main

Módulo do projeto [microservices-demo](https://github.com/Lucas-319/microservices-demo) que hospeda o Spring Cloud Config Server (prefixo `/config`) e o Service Discovery Eureka (dashboard em `/`).

## Tecnologias
- Java 21
- Maven
- Spring Boot
- Spring Cloud: Config Server, Netflix Eureka
- Docker

## Porta e Endpoints
- Porta: `8888`
- Config Server (exemplos):
  - `GET /config/service-task/default`
  - `GET /config/service-notification/default`
- Eureka Dashboard (UI):
  - `GET /`
- Eureka REST API (base) e registro de clientes:
  - `GET /eureka` (ex.: `/eureka/apps`)
  - Clientes devem usar `eureka.client.service-url.defaultZone=http://service-main:8888/eureka/`

## Como se integra no projeto
- Provedor central de configuração e descoberta:
  - Expõe o Config Server consumido por [service-task](https://github.com/Lucas-319/service-task) e [service-notification](https://github.com/Lucas-319/service-notification) via `spring.config.import=configserver:http://service-main:8888/config`.
  - Hospeda o Eureka, onde os serviços se registram e se descobrem por nome lógico.