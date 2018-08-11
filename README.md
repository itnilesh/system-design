# system-design

Want to list aspects when you start to design system as architect.

Lets list aspects for designing new system from scratch it may be chat server or e-commerence site or uber like system or anything you wish.

Some good points need to keep in mind while desining any system please refer 
https://12factor.net/ 

1. Do requirement analysis  
  - What are major functional use-cases?
  - What are minimum functional use cases are required for minimum viable prpduct?
  - Throughput and latency requirements for api requests 
  - Whether api is piblic or internal 
  - What will happen in case of failure
  - Understand SLAs
  - Whether it is real time communication/batch job /streaming etc.
  - Creating POCs
  - discussing with team 
  - creating architecture design docs
  - Understanding assumptions and underlaying limitations of requitements and system.

 
2. Micro-services 
  - Segregate independent functionality and wrap it inside micro-service.
  - So identity key components which can become micro-services 
  
2. Client/User
 
  Identify what is client whether it browser/app/custom client etc.
  - HTTP based widely apis are quite generic which could be consumed by browse/app/client etc.
  - TCP/WebSocket/GRPC/RPC based protocol may use their own serialization/de-serilizaton method for sending and recieving messgae so common client like browsers might not able to handle it. It needs some app/client to use it.
  
  
 3. API communication type
 
 Decide protocol type based on requirement like bi-directional communication/streaming/nature of data/efficiency 
 
  - tcp - This is most basic as other protocols are built on top of it.Is there need to use such lower level of network ?
  
  - websocket - This is bi-directional protocol means server-client can talk to each other. example RabbitMQ to access over internet we can use websocket based protocol or for chat server to hold  bidirectional connection.
  
 - HTTP/HTTPS - This is wellknow protocol with wide acceptance
  - HTTP/1.1 - This protocol supports one directional communication like request -response based stateless protocol.
  - HTTP/2.0 - refer https://http2.akamai.com/demo HTTP/2.0 can be configured to use websockets. GRPC needs HTTP/2.0 as it is built above it.
  
  
 #### HTTP Polling  
    Using HTTP based rest api have certain challenges in case of async/bi-directional/streaming communication.
    We have to choose following technique on client side based on need like whether it is real time/batch job/stream etc.
    - Short polling 
    - Long polling 
    - Periodic polling 
    
 - API format
 - REST based 
   - Most widely used format to implement API. Mostly stateless public apis build over http.
    - swagger API spec/open api specs 
   
 - GRPC based  
 - This is  google's remote procedure call used to invoke remote method. This can be also configured for bi-directional 
 - Need to publish api defination in proto file format if protobuf is used.
 
 Communicating clear error messages on which client can act is crucial while desining any of above API.

  
 4. Load balancer (Exposing server as API through single end-point)
 
 - decide which level incase of http/https L7 etc. you want to do load balancing. Example if you have to support both http and grpc then you might need tcp based L4 load balancer.
 - Whether it is state oriented requirement means you have to manage sessions like sticky sessions.
 As far as we have to avoid this as it will bite us back while scaling but some cases like chat server we might not able to avoid it.
 - SSL/TLS terminaton at load balancer level.
 - Check load balancer support fot tcp or http1.1 or http/2.0
 
5. Distributed Computation Unit
 - We can have several nodes/containers/dockers etc to do computation for each request.
 - We can choose CPU/GPU + memory based computation unit as per need
 - Example - kubernettes based pods


6. Programming language 
   You can choose language based on many factors like performance/learning curve/maturity of libraries/ecosystem.
   You can choose like C++/Java/Python/Golang/Ruby  etc. There though other languages like haskel/lua etc could be 
   chosen with own discretion based on special need.
   
5. Distributed Storage

 Choose one or more based on your requirement
 - Relational Databases 
 - Key value store like etcd/Redis
 - Document store like mongoDB
 - Columnar Database like cassandra
 - Graph database like neo4j
 - Full text search engine like elastic search
 - NFS if you need large file storage 
 - Blob/Object store if you need to store binary data like in AWS S3 based store etc.
 - Local storage which comes with container/instance
 
 
 6. Metrics Collection and Autoscaling 
 - Instance/Container sizing 
 
 
 7. Logging and Distributed Request tracing  
 
 8. Authentication and Authorization 
 
 9. Async Processing 
 
 10. Lambda Architecture (stream+batch processing)
 
 11. Circuit Breaker 
 
 12. Distributed Queue(Kafka/FRabbitMQ)
 
 13. Caching 
 
  You can cache result in layers like network/application/container level.
  
 14. Distributed Transactions/Locks
  If there is special use case then we can use distributed locks but it will slow us down for throughput and latency.
 
 13. Automated Deployments/Infrastructure as code
  Choose tools for automated deployments 
  - Example terraform can deploy application to multiple clouds like AWS/GCP/AZURE/private cloud like Cloud 
  foundry or kubernettes etc.

 14. CI/CD pipeline (Jenkins)

  - Developement stage
  - Integration Stage
  - Acceptance Stage
  - Performance Stage
  - Preproduction stage
  - Production stage
 
 15. Design Documents 
 

 
 
 References 
 http://highscalability.com/all-time-favorites/
 
 
                  
