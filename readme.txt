Eureka service detective component.


1. How to create Eureka server
step1: annotated Main class with @EnableEurekaServer
step2: configure properly in application.yml
server:
  port: 8761                   <-- listen on which port
eureka:
  instance:
    hostname: localhost        <-- eureka server hostname
  client:
    registerWithEureka: false  <-- if need to register to another Eureka, if eureka server is a single node then we need to set it to false explicitly
    fetchRegistry: false       <-- save as above
    serviceUrl:
      defaultZone: http://${eureka.instance.hostname}:${server.port}/eureka/    <-- need to add /eureka/ however we only need http://${eureka.instance.hostname}:${server.port} to access eureka console
      
Outstanding issue
1. how to set eureka server cluster
2. if we set eureka server cluster how to set serviceUrl?
      
Access to eureka server http://localhost:8761/


2. How to create an Eureka Client
step1: annotated Main class with @EnableDiscoveryClient
step2: configure properly in application.yml
server: 
  port: 8762                 <-- service listen on this port
eureka:
  client:
    serviceUrl:
      defautZone: http://localhost:8761/eureka/   <-- eureka sever path
spring:
  application:
    name: service-hi          <-- service name
step3:
expose http rest service using @RestController and @RequestMapping

