# Spring Cloud Microservice Parent

This project aims to contain all the basic dependencies for any Spring based microservice

## Table of Contents
* **[Libraries included](#libraries-included)**  
* **[Dependencies](#dependencies)**
* **[Usage](#usage)**

## Libraries included

- Spring Boot
- Spring Cloud
- Springfox's Swagger 2
- Zuul
- Eureka
- Jacoco
- Docker-plugin

## Dependencies

- Java 8
- Oracle VirtualBox [(https://www.virtualbox.org/wiki/Downloads)](https://www.virtualbox.org/wiki/Downloads)
- Docker Toolbox 1.10.2 - [(https://www.docker.com/products/docker-toolbox)](https://www.docker.com/products/docker-toolbox)
- Maven 3

## Usage

Add the following as the parent of the project:

>     <parent>
>        <groupId>uk.co.whitbread</groupId>
>        <artifactId>spring-cloud-microservice-parent</artifactId>
>        <version>1.0</version>
>     </parent>
