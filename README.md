### Adidas Backend Assignment

```

      _           _    __       _                             ___                   _                
     /.\       ___FJ   LJ    ___FJ     ___ _     ____       ,"___".    ____      ___FJ     ____      
    //_\\     F __  L       F __  L   F __` L   F ___J      FJ---L]   F __ J    F __  L   F __ J     
   / ___ \   | |--| |  FJ  | |--| |  | |--| |  | '----_    J |   LJ  | |--| |  | |--| |  | _____J    
  / L___J \  F L__J J J  L F L__J J  F L__J J  )-____  L   | \___--. F L__J J  F L__J J  F L___--.   
 J__L   J__LJ\____,__LJ__LJ\____,__LJ\____,__LJ\______/F   J\_____/FJ\______/FJ\____,__LJ\______/F   
 |__L   J__| J____,__F|__| J____,__F J____,__F J______F     J_____F  J______F  J____,__F J______F    
              ___      _                 __  __                                                      
            ,"___".   FJ___      ___ _   LJ  LJ    ____     _ ___      ___ _     ____                
            FJ---L]  J  __ `.   F __` L  FJ  FJ   F __ J   J '__ J    F __` L   F __ J               
           J |   LJ  | |--| |  | |--| | J  LJ  L | _____J  | |__| |  | |--| |  | _____J              
           | \___--. F L  J J  F L__J J J  LJ  L F L___--. F L  J J  F L__J J  F L___--.             
           J\_____/FJ__L  J__LJ\____,__LJ__LJ__LJ\______/FJ__L  J__L )-____  LJ\______/F             
            J_____F |__L  J__| J____,__F|__||__| J______F |__L  J__|J\______/F J______F              
                  ___      _                __            __    _    J______F                        
                ,"___".   FJ___     _ ___   LJ   _ ___    LJ   FJ __      ____                       
                FJ---L]  J  __ `.  J '__ ",     J '__ J       J |/ /L    F __ J                      
               J |   LJ  | |--| |  | |__|-J FJ  | |__| |  FJ  |    \    | |--| |                     
               | \___--. F L  J J  F L  `-'J  L F L  J J J  L F L:\ J   F L__J J                     
               J\_____/FJ__L  J__LJ__L     J__LJ__L  J__LJ__LJ__L \\_J.J\______/F                    
                J_____F |__L  J__||__L     |__||__L  J__||__||__L  \L_| J______F                     
                                                                                                     
```

##### Assignee: Nikolaos Christidis (nick.christidis@yahoo.com)

#### Microservices

* [Itineraries Lookup Service](https://github.com/chriniko13/itineraries-lookup-service) which provides itinerary lookup operation
    * Operation sample:
        * Post at: `http://localhost:8181/api/itinerary-info?allItinerariesInfo=false&allItinerariesInfoDetailed=false` with body:
        ```json
              {
                "name":"Huelva",
                "country":"Spain"
              }
        ```
        
        Response:
          
      ```json
          {
                "itinerariesInfoByProcessingCriteria": {
                    "less-connections-and-less-time" : [...],
                    "less-connections" : [...],
                    "less-time" : [...]
                }
          }
    
      ```
          

* [Routes Service](https://github.com/chriniko13/routes-service) which exposes routes information via CRUD operations.
    * Sample records: 
        ```
        origin_city_name    origin_country      destiny_city_name   destiny_country     departure_time          arrival_time
        ---------------------------------------------------------------------------------------------------------------------------
        Valencia	        Spain	            Badajoz	            Spain	            2019-03-11 19:16:40	    2019-03-11 20:16:40
        Valencia	        Spain	            Jaen	            Spain	            2019-03-11 19:16:40	    2019-03-11 22:16:40
        Valencia	        Spain	            Salamanca	        Spain	            2019-03-11 19:16:40	    2019-03-11 20:16:40
        Valencia	        Spain	            Gijon	            Spain	            2019-03-11 19:16:40	    2019-03-11 20:16:40
        Valencia	        Spain	            Arrecife	        Spain	            2019-03-11 19:16:40	    2019-03-11 21:16:40
        Valencia	        Spain	            Vitoria	            Spain	            2019-03-11 19:16:40	    2019-03-11 22:16:40

        ```
        
        
#### Infrastructure
* MySQL
* Redis
* Redis Commander
* Kafka


#### Prerequisites
* Docker and Docker Compose


#### How to run it?

1) Git clone/Download [Routes Service](https://github.com/chriniko13/routes-service) 
   go in project folder and execute: `mvn clean install -DskipUTs=true -DskipITs && docker build -t chriniko/routes-service:1.0.0 .`

2) Git clone/Download [Itineraries Lookup Service](https://github.com/chriniko13/itineraries-lookup-service)
   go in project folder and execute: `mvn clean install -DskipUTs=true -DskipITs && docker build -t chriniko/itineraries-lookup-service:1.0.0 .`

3) Now in this project folder execute: `docker-compose up -d`

4) Wait for 10 seconds

5) Execute: `docker ps`, you should see something like the following:
   ```
   CONTAINER ID        IMAGE                                       COMMAND                  CREATED             STATUS              PORTS                                        NAMES
   36e78af4a27d        chriniko/itineraries-lookup-service:1.0.0   "java -Dspring.profi…"   10 seconds ago      Up 9 seconds        0.0.0.0:8181->8181/tcp                       adidascodechallenge_itineraries-lookup-service_1
   488e074ceba4        chriniko/routes-service:1.0.0               "java -Dspring.profi…"   11 seconds ago      Up 10 seconds       0.0.0.0:8080->8080/tcp                       adidascodechallenge_routes-service_1
   00d422566600        rediscommander/redis-commander:latest       "/usr/bin/dumb-init …"   12 seconds ago      Up 11 seconds       0.0.0.0:8081->8081/tcp                       adidascodechallenge_redis-commander_1
   51e22e94a975        confluentinc/cp-kafka:latest                "/etc/confluent/dock…"   12 seconds ago      Up 11 seconds       0.0.0.0:9092->9092/tcp                       adidascodechallenge_kafka_1
   ea74285cc719        redis                                       "docker-entrypoint.s…"   13 seconds ago      Up 12 seconds       0.0.0.0:6379->6379/tcp                       adidascodechallenge_redis_1
   655cf7691d55        confluentinc/cp-zookeeper:latest            "/etc/confluent/dock…"   13 seconds ago      Up 12 seconds       2888/tcp, 0.0.0.0:2181->2181/tcp, 3888/tcp   adidascodechallenge_zookeeper_1
   b1192bc50b6d        mysql:5.7                                   "docker-entrypoint.s…"   13 seconds ago      Up 11 seconds       0.0.0.0:3306->3306/tcp, 33060/tcp            adidascodechallenge_mysql_1

   ```
   
   We can see that our Infrastructure and Microservices are up and running

6) Execute: `docker-compose logs routes-service` to see that we do not have any error logs.
   You should see something like the following:
   ```
   routes-service_1              | 2019-03-12 00:28:59.472  INFO f9c0e174c8d9 --- [           main] c.a.c.r.RoutesServiceApplication         : Starting RoutesServiceApplication v1.0.0-SNAPSHOT on f9c0e174c8d9 with PID 1 (/app/app.jar started by root in /app)
   routes-service_1              | 2019-03-12 00:28:59.485 DEBUG f9c0e174c8d9 --- [           main] c.a.c.r.RoutesServiceApplication         : Running with Spring Boot v2.1.3.RELEASE, Spring v5.1.5.RELEASE
   routes-service_1              | 2019-03-12 00:28:59.486  INFO f9c0e174c8d9 --- [           main] c.a.c.r.RoutesServiceApplication         : The following profiles are active: container
   routes-service_1              | 2019-03-12 00:29:01.512  INFO f9c0e174c8d9 --- [           main] .s.d.r.c.RepositoryConfigurationDelegate : Multiple Spring Data modules found, entering strict repository configuration mode!
   routes-service_1              | 2019-03-12 00:29:01.518  INFO f9c0e174c8d9 --- [           main] .s.d.r.c.RepositoryConfigurationDelegate : Bootstrapping Spring Data repositories in DEFAULT mode.
   routes-service_1              | 2019-03-12 00:29:01.570  INFO f9c0e174c8d9 --- [           main] .s.d.r.c.RepositoryConfigurationDelegate : Finished Spring Data repository scanning in 37ms. Found 0 repository interfaces.
   routes-service_1              | 2019-03-12 00:29:01.586  INFO f9c0e174c8d9 --- [           main] .s.d.r.c.RepositoryConfigurationDelegate : Multiple Spring Data modules found, entering strict repository configuration mode!
   routes-service_1              | 2019-03-12 00:29:01.608  INFO f9c0e174c8d9 --- [           main] .s.d.r.c.RepositoryConfigurationDelegate : Bootstrapping Spring Data repositories in DEFAULT mode.
   routes-service_1              | 2019-03-12 00:29:01.637  INFO f9c0e174c8d9 --- [           main] .s.d.r.c.RepositoryConfigurationDelegate : Finished Spring Data repository scanning in 18ms. Found 0 repository interfaces.
   routes-service_1              | 2019-03-12 00:29:03.783  INFO f9c0e174c8d9 --- [           main] c.z.h.HikariDataSource                   : routes-hikari-pool - Starting...
   routes-service_1              | 2019-03-12 00:29:04.962  INFO f9c0e174c8d9 --- [           main] c.z.h.HikariDataSource                   : routes-hikari-pool - Start completed.
   routes-service_1              | 2019-03-12 00:29:05.148  INFO f9c0e174c8d9 --- [           main] o.h.j.i.u.LogHelper                      : HHH000204: Processing PersistenceUnitInfo [
   routes-service_1              |         name: default
   routes-service_1              |         ...]
   routes-service_1              | 2019-03-12 00:29:05.275  INFO f9c0e174c8d9 --- [           main] o.h.Version                              : HHH000412: Hibernate Core {5.3.7.Final}
   routes-service_1              | 2019-03-12 00:29:05.277  INFO f9c0e174c8d9 --- [           main] o.h.c.Environment                        : HHH000206: hibernate.properties not found
   routes-service_1              | 2019-03-12 00:29:05.582  INFO f9c0e174c8d9 --- [           main] o.h.a.c.Version                          : HCANN000001: Hibernate Commons Annotations {5.0.4.Final}
   routes-service_1              | 2019-03-12 00:29:06.005  INFO f9c0e174c8d9 --- [           main] o.h.d.Dialect                            : HHH000400: Using dialect: org.hibernate.dialect.MySQL5InnoDBDialect
   routes-service_1              | 2019-03-12 00:29:07.235  INFO f9c0e174c8d9 --- [           main] o.h.h.i.QueryTranslatorFactoryInitiator  : HHH000397: Using ASTQueryTranslatorFactory
   routes-service_1              | 2019-03-12 00:29:07.369  INFO f9c0e174c8d9 --- [           main] j.LocalContainerEntityManagerFactoryBean : Initialized JPA EntityManagerFactory for persistence unit 'default'
   routes-service_1              | 2019-03-12 00:29:08.545 DEBUG f9c0e174c8d9 --- [           main] c.a.c.r.i.DbInit                         : will create schema now...
   routes-service_1              | 2019-03-12 00:29:08.929 DEBUG f9c0e174c8d9 --- [           main] c.a.c.r.i.CitiesCsvProcessor             : total csv records: 12893
   routes-service_1              | 2019-03-12 00:29:08.932 DEBUG f9c0e174c8d9 --- [           main] c.a.c.r.i.RouteGenerator                 : totalCountries: 234, averageCitiesPerCountry: 56, maxCitiesPerCountry: 4848, minCitiesPerCountry: 1, sumOfCities: 12893
   routes-service_1              | 2019-03-12 00:29:09.143 DEBUG f9c0e174c8d9 --- [           main] c.a.c.r.i.RouteGenerator                 : countries which not satisfy noOfItinerariesForSelectedRootCity: 73
   routes-service_1              | 2019-03-12 00:29:09.145 DEBUG f9c0e174c8d9 --- [           main] c.a.c.r.i.RouteGenerator                 : accurateNumberOfRecordsInDbAfterExecution: 5133
   routes-service_1              | 2019-03-12 00:29:09.145 DEBUG f9c0e174c8d9 --- [           main] c.a.c.r.i.RouteGenerator                 : total db workers: 161
   routes-service_1              | 2019-03-12 00:29:12.348 DEBUG f9c0e174c8d9 --- [           main] c.a.c.r.s.CacheService                   : will clear redis [cache(CityInfo) ---> RouteInfo], keys: []
   routes-service_1              | 2019-03-12 00:29:12.350 DEBUG f9c0e174c8d9 --- [           main] c.a.c.r.s.CacheService                   : will clear redis [cache(routeId:String) ---> RouteInfo], keys: []
   routes-service_1              | 2019-03-12 00:29:12.668  INFO f9c0e174c8d9 --- [           main] o.s.b.w.e.n.NettyWebServer               : Netty started on port(s): 8080
   routes-service_1              | 2019-03-12 00:29:12.693  INFO f9c0e174c8d9 --- [           main] c.a.c.r.RoutesServiceApplication         : Started RoutesServiceApplication in 14.313 seconds (JVM running for 17.476)

   ```

7) Execute: `docker-compose logs itineraries-lookup-service` to see that we do not have any error logs.
   You should see something like the following:
   ```
   itineraries-lookup-service_1  | 2019-03-12 00:29:00.095  INFO 0e534ddbad08 --- [           main] .c.i.ItinerariesLookupServiceApplication : Starting ItinerariesLookupServiceApplication v1.0.0-SNAPSHOT on 0e534ddbad08 with PID 1 (/app/app.jar started by root in /app)
   itineraries-lookup-service_1  | 2019-03-12 00:29:00.132 DEBUG 0e534ddbad08 --- [           main] .c.i.ItinerariesLookupServiceApplication : Running with Spring Boot v2.1.3.RELEASE, Spring v5.1.5.RELEASE
   itineraries-lookup-service_1  | 2019-03-12 00:29:00.133  INFO 0e534ddbad08 --- [           main] .c.i.ItinerariesLookupServiceApplication : The following profiles are active: container
   itineraries-lookup-service_1  | 2019-03-12 00:29:03.916  INFO 0e534ddbad08 --- [           main] trationDelegate$BeanPostProcessorChecker : Bean 'org.springframework.retry.annotation.RetryConfiguration' of type [org.springframework.retry.annotation.RetryConfiguration$$EnhancerBySpringCGLIB$$98bebf4e] is not eligible for getting processed by all BeanPostProcessors (for example: not eligible for auto-proxying)
   itineraries-lookup-service_1  | 2019-03-12 00:29:05.132  WARN 0e534ddbad08 --- [           main] i.u.w.jsr                                : UT026010: Buffer pool was not set on WebSocketDeploymentInfo, the default pool will be used
   itineraries-lookup-service_1  | 2019-03-12 00:29:05.168  INFO 0e534ddbad08 --- [           main] i.u.servlet                              : Initializing Spring embedded WebApplicationContext
   itineraries-lookup-service_1  | 2019-03-12 00:29:05.169  INFO 0e534ddbad08 --- [           main] o.s.w.c.ContextLoader                    : Root WebApplicationContext: initialization completed in 4820 ms
   itineraries-lookup-service_1  | 2019-03-12 00:29:05.723  INFO 0e534ddbad08 --- [           main] c.h.i.AddressPicker                      : [LOCAL] [dev] [3.11.1] Prefer IPv4 stack is true, prefer IPv6 addresses is false
   itineraries-lookup-service_1  | 2019-03-12 00:29:05.751  INFO 0e534ddbad08 --- [           main] c.h.i.AddressPicker                      : [LOCAL] [dev] [3.11.1] Picked [172.25.0.8]:5701, using socket ServerSocket[addr=/0.0.0.0,localport=5701], bind any local is true
   itineraries-lookup-service_1  | 2019-03-12 00:29:05.805  INFO 0e534ddbad08 --- [           main] c.h.system                               : [172.25.0.8]:5701 [dev] [3.11.1] Hazelcast 3.11.1 (20181218 - d294f31) starting at [172.25.0.8]:5701
   itineraries-lookup-service_1  | 2019-03-12 00:29:05.806  INFO 0e534ddbad08 --- [           main] c.h.system                               : [172.25.0.8]:5701 [dev] [3.11.1] Copyright (c) 2008-2018, Hazelcast, Inc. All Rights Reserved.
   itineraries-lookup-service_1  | 2019-03-12 00:29:05.807  INFO 0e534ddbad08 --- [           main] c.h.i.Node                               : [172.25.0.8]:5701 [dev] [3.11.1] A non-empty group password is configured for the Hazelcast member. Starting with Hazelcast version 3.8.2, members with the same group name, but with different group passwords (that do not use authentication) form a cluster. The group password configuration will be removed completely in a future release.
   itineraries-lookup-service_1  | 2019-03-12 00:29:06.292  INFO 0e534ddbad08 --- [           main] c.h.s.i.o.i.BackpressureRegulator        : [172.25.0.8]:5701 [dev] [3.11.1] Backpressure is disabled
   itineraries-lookup-service_1  | 2019-03-12 00:29:07.077  INFO 0e534ddbad08 --- [           main] c.h.i.Node                               : [172.25.0.8]:5701 [dev] [3.11.1] Creating MulticastJoiner
   itineraries-lookup-service_1  | 2019-03-12 00:29:07.310  INFO 0e534ddbad08 --- [           main] c.h.s.i.o.i.OperationExecutorImpl        : [172.25.0.8]:5701 [dev] [3.11.1] Starting 4 partition threads and 3 generic threads (1 dedicated for priority tasks)
   itineraries-lookup-service_1  | 2019-03-12 00:29:07.327  INFO 0e534ddbad08 --- [           main] c.h.i.d.Diagnostics                      : [172.25.0.8]:5701 [dev] [3.11.1] Diagnostics disabled. To enable add -Dhazelcast.diagnostics.enabled=true to the JVM arguments.
   itineraries-lookup-service_1  | 2019-03-12 00:29:07.337  INFO 0e534ddbad08 --- [           main] c.h.c.LifecycleService                   : [172.25.0.8]:5701 [dev] [3.11.1] [172.25.0.8]:5701 is STARTING
   itineraries-lookup-service_1  | 2019-03-12 00:29:10.648  INFO 0e534ddbad08 --- [           main] c.h.i.c.ClusterService                   : [172.25.0.8]:5701 [dev] [3.11.1] 
   itineraries-lookup-service_1  | 
   itineraries-lookup-service_1  | Members {size:1, ver:1} [
   itineraries-lookup-service_1  |         Member [172.25.0.8]:5701 - 1acce855-c4d1-4978-b99a-f0f390a5ee09 this
   itineraries-lookup-service_1  | ]
   itineraries-lookup-service_1  | 
   itineraries-lookup-service_1  | 2019-03-12 00:29:10.689  INFO 0e534ddbad08 --- [           main] c.h.c.LifecycleService                   : [172.25.0.8]:5701 [dev] [3.11.1] [172.25.0.8]:5701 is STARTED
   itineraries-lookup-service_1  | 2019-03-12 00:29:10.765  INFO 0e534ddbad08 --- [           main] c.h.i.p.i.PartitionStateManager          : [172.25.0.8]:5701 [dev] [3.11.1] Initializing cluster partition table arrangement...
   itineraries-lookup-service_1  | 2019-03-12 00:29:10.897 DEBUG 0e534ddbad08 --- [           main] c.a.c.i.s.CacheService                   : total entries in itineraries-lookups map: 0
   itineraries-lookup-service_1  | 2019-03-12 00:29:10.989  INFO 0e534ddbad08 --- [           main] o.a.k.c.p.ProducerConfig                 : ProducerConfig values: 
   itineraries-lookup-service_1  |         acks = 1
   itineraries-lookup-service_1  |         batch.size = 16384
   itineraries-lookup-service_1  |         bootstrap.servers = [kafka:29092]
   itineraries-lookup-service_1  |         buffer.memory = 33554432
   itineraries-lookup-service_1  |         client.dns.lookup = default
   itineraries-lookup-service_1  |         client.id = KafkaExampleProducer
   itineraries-lookup-service_1  |         compression.type = none
   itineraries-lookup-service_1  |         connections.max.idle.ms = 540000
   itineraries-lookup-service_1  |         delivery.timeout.ms = 120000
   itineraries-lookup-service_1  |         enable.idempotence = false
   itineraries-lookup-service_1  |         interceptor.classes = []
   itineraries-lookup-service_1  |         key.serializer = class com.adidas.chriniko.itinerarieslookupservice.service.kafka.ItinerarySearchInfoSerializer
   itineraries-lookup-service_1  |         linger.ms = 0
   itineraries-lookup-service_1  |         max.block.ms = 60000
   itineraries-lookup-service_1  |         max.in.flight.requests.per.connection = 5
   itineraries-lookup-service_1  |         max.request.size = 1048576
   itineraries-lookup-service_1  |         metadata.max.age.ms = 300000
   itineraries-lookup-service_1  |         metric.reporters = []
   itineraries-lookup-service_1  |         metrics.num.samples = 2
   itineraries-lookup-service_1  |         metrics.recording.level = INFO
   itineraries-lookup-service_1  |         metrics.sample.window.ms = 30000
   itineraries-lookup-service_1  |         partitioner.class = class org.apache.kafka.clients.producer.internals.DefaultPartitioner
   itineraries-lookup-service_1  |         receive.buffer.bytes = 32768
   itineraries-lookup-service_1  |         reconnect.backoff.max.ms = 1000
   itineraries-lookup-service_1  |         reconnect.backoff.ms = 50
   itineraries-lookup-service_1  |         request.timeout.ms = 30000
   itineraries-lookup-service_1  |         retries = 2147483647
   itineraries-lookup-service_1  |         retry.backoff.ms = 100
   itineraries-lookup-service_1  |         sasl.client.callback.handler.class = null
   itineraries-lookup-service_1  |         sasl.jaas.config = null
   itineraries-lookup-service_1  |         sasl.kerberos.kinit.cmd = /usr/bin/kinit
   itineraries-lookup-service_1  |         sasl.kerberos.min.time.before.relogin = 60000
   itineraries-lookup-service_1  |         sasl.kerberos.service.name = null
   itineraries-lookup-service_1  |         sasl.kerberos.ticket.renew.jitter = 0.05
   itineraries-lookup-service_1  |         sasl.kerberos.ticket.renew.window.factor = 0.8
   itineraries-lookup-service_1  |         sasl.login.callback.handler.class = null
   itineraries-lookup-service_1  |         sasl.login.class = null
   itineraries-lookup-service_1  |         sasl.login.refresh.buffer.seconds = 300
   itineraries-lookup-service_1  |         sasl.login.refresh.min.period.seconds = 60
   itineraries-lookup-service_1  |         sasl.login.refresh.window.factor = 0.8
   itineraries-lookup-service_1  |         sasl.login.refresh.window.jitter = 0.05
   itineraries-lookup-service_1  |         sasl.mechanism = GSSAPI
   itineraries-lookup-service_1  |         security.protocol = PLAINTEXT
   itineraries-lookup-service_1  |         send.buffer.bytes = 131072
   itineraries-lookup-service_1  |         ssl.cipher.suites = null
   itineraries-lookup-service_1  |         ssl.enabled.protocols = [TLSv1.2, TLSv1.1, TLSv1]
   itineraries-lookup-service_1  |         ssl.endpoint.identification.algorithm = https
   itineraries-lookup-service_1  |         ssl.key.password = null
   itineraries-lookup-service_1  |         ssl.keymanager.algorithm = SunX509
   itineraries-lookup-service_1  |         ssl.keystore.location = null
   itineraries-lookup-service_1  |         ssl.keystore.password = null
   itineraries-lookup-service_1  |         ssl.keystore.type = JKS
   itineraries-lookup-service_1  |         ssl.protocol = TLS
   itineraries-lookup-service_1  |         ssl.provider = null
   itineraries-lookup-service_1  |         ssl.secure.random.implementation = null
   itineraries-lookup-service_1  |         ssl.trustmanager.algorithm = PKIX
   itineraries-lookup-service_1  |         ssl.truststore.location = null
   itineraries-lookup-service_1  |         ssl.truststore.password = null
   itineraries-lookup-service_1  |         ssl.truststore.type = JKS
   itineraries-lookup-service_1  |         transaction.timeout.ms = 60000
   itineraries-lookup-service_1  |         transactional.id = null
   itineraries-lookup-service_1  |         value.serializer = class com.adidas.chriniko.itinerarieslookupservice.service.kafka.ItineraryInfoResultSerializer
   itineraries-lookup-service_1  | 
   itineraries-lookup-service_1  | 2019-03-12 00:29:11.130  INFO 0e534ddbad08 --- [           main] o.a.k.c.u.AppInfoParser                  : Kafka version : 2.1.1
   itineraries-lookup-service_1  | 2019-03-12 00:29:11.131  INFO 0e534ddbad08 --- [           main] o.a.k.c.u.AppInfoParser                  : Kafka commitId : 21234bee31165527
   itineraries-lookup-service_1  | 2019-03-12 00:29:11.968  INFO 0e534ddbad08 --- [           main] pertySourcedRequestMappingHandlerMapping : Mapped URL path [/v2/api-docs] onto method [public org.springframework.http.ResponseEntity<springfox.documentation.spring.web.json.Json> springfox.documentation.swagger2.web.Swagger2Controller.getDocumentation(java.lang.String,javax.servlet.http.HttpServletRequest)]
   itineraries-lookup-service_1  | 2019-03-12 00:29:12.115  INFO 0e534ddbad08 --- [           main] o.s.s.c.ThreadPoolTaskExecutor           : Initializing ExecutorService 'applicationTaskExecutor'
   itineraries-lookup-service_1  | 2019-03-12 00:29:12.447  INFO 0e534ddbad08 --- [           main] d.s.w.p.DocumentationPluginsBootstrapper : Context refreshed
   itineraries-lookup-service_1  | 2019-03-12 00:29:12.506  INFO 0e534ddbad08 --- [           main] d.s.w.p.DocumentationPluginsBootstrapper : Found 1 custom documentation plugin(s)
   itineraries-lookup-service_1  | 2019-03-12 00:29:12.577  INFO 0e534ddbad08 --- [           main] s.d.s.w.s.ApiListingReferenceScanner     : Scanning for api listing references
   itineraries-lookup-service_1  | 2019-03-12 00:29:12.896  INFO 0e534ddbad08 --- [           main] o.xnio                                   : XNIO version 3.3.8.Final
   itineraries-lookup-service_1  | 2019-03-12 00:29:12.908  INFO 0e534ddbad08 --- [           main] o.x.nio                                  : XNIO NIO Implementation Version 3.3.8.Final
   itineraries-lookup-service_1  | 2019-03-12 00:29:13.000  INFO 0e534ddbad08 --- [           main] o.s.b.w.e.u.UndertowServletWebServer     : Undertow started on port(s) 8181 (http) with context path ''
   itineraries-lookup-service_1  | 2019-03-12 00:29:13.004  INFO 0e534ddbad08 --- [           main] .c.i.ItinerariesLookupServiceApplication : Started ItinerariesLookupServiceApplication in 14.063 seconds (JVM running for 16.839)

   ```

8) Now it is time to find a root city(appear only as origin city and not as destiny) from [Routes Service](https://github.com/chriniko13/routes-service)
   Connect to mysql of [Routes Service](https://github.com/chriniko13/routes-service) 
   Connection Info: (jdbc:mysql://localhost:3306/db, username: user, password: user, you can see that from `docker-compose.yml`)
   And execute the following sql:
   
   ```sql
       select origin_city_name, origin_country, destiny_city_name, destiny_country, departure_time, arrival_time
       from routes
       where origin_city_name NOT IN (
         select destiny_city_name
         from routes
         where destiny_country = 'Spain'
       )
       and origin_country = 'Spain';
    ```
   

9) Perform Http Request with POST method on url: `http://localhost:8181/api/itinerary-info?allItinerariesInfo=false&allItinerariesInfoDetailed=false`
   
   Example Payload:
   ```json
       {
        "name":"Tarragona",
        "country":"Spain"
       }

    ```
    
    Example Response:
    ```json
        {
            "itinerariesInfoByProcessingCriteria": {
                "less-connections-and-less-time": [
                    {
                        "fastDisplay": "[Tarragona ---> Salamanca]",
                        "noOfConnections": 1,
                        "noOfVisitedCities": 2,
                        "departureTimeOfItinerary": "2019-03-12T00:29:09Z",
                        "arrivalTimeOfItinerary": "2019-03-12T03:29:09Z",
                        "timeDurationOfItinerary": "PT3H",
                        "detailedRouteInfo": [
                            {
                                "id": "6a29b25e-2f75-46c4-b72b-a96ac7f33205",
                                "city": {
                                    "name": "Tarragona",
                                    "country": "Spain"
                                },
                                "destinyCity": {
                                    "name": "Salamanca",
                                    "country": "Spain"
                                },
                                "departureTime": "2019-03-12T00:29:09Z",
                                "arrivalTime": "2019-03-12T03:29:09Z"
                            }
                        ]
                    },
                    {
                        "fastDisplay": "[Tarragona ---> Gijon]",
                        "noOfConnections": 1,
                        "noOfVisitedCities": 2,
                        "departureTimeOfItinerary": "2019-03-12T00:29:09Z",
                        "arrivalTimeOfItinerary": "2019-03-12T04:29:09Z",
                        "timeDurationOfItinerary": "PT4H",
                        "detailedRouteInfo": [
                            {
                                "id": "72dbd810-ae2c-4ddb-a198-998d80f0808a",
                                "city": {
                                    "name": "Tarragona",
                                    "country": "Spain"
                                },
                                "destinyCity": {
                                    "name": "Gijon",
                                    "country": "Spain"
                                },
                                "departureTime": "2019-03-12T00:29:09Z",
                                "arrivalTime": "2019-03-12T04:29:09Z"
                            }
                        ]
                    },
                    {
                        "fastDisplay": "[Tarragona ---> Vitoria ---> Santander ---> Logrono]",
                        "noOfConnections": 3,
                        "noOfVisitedCities": 4,
                        "departureTimeOfItinerary": "2019-03-12T00:29:09Z",
                        "arrivalTimeOfItinerary": "2019-03-12T05:29:09Z",
                        "timeDurationOfItinerary": "PT5H",
                        "detailedRouteInfo": [
                            {
                                "id": "fe82a3c4-908c-48c3-b569-ea030c8b4a90",
                                "city": {
                                    "name": "Tarragona",
                                    "country": "Spain"
                                },
                                "destinyCity": {
                                    "name": "Vitoria",
                                    "country": "Spain"
                                },
                                "departureTime": "2019-03-12T00:29:09Z",
                                "arrivalTime": "2019-03-12T01:29:09Z"
                            },
                            {
                                "id": "10d05df9-5542-4a1d-97fb-6f100f52bd01",
                                "city": {
                                    "name": "Vitoria",
                                    "country": "Spain"
                                },
                                "destinyCity": {
                                    "name": "Santander",
                                    "country": "Spain"
                                },
                                "departureTime": "2019-03-12T01:29:09Z",
                                "arrivalTime": "2019-03-12T04:29:09Z"
                            },
                            {
                                "id": "7a6ba369-6a6e-4ea8-80cb-8320e32055e4",
                                "city": {
                                    "name": "Santander",
                                    "country": "Spain"
                                },
                                "destinyCity": {
                                    "name": "Logrono",
                                    "country": "Spain"
                                },
                                "departureTime": "2019-03-12T04:29:09Z",
                                "arrivalTime": "2019-03-12T05:29:09Z"
                            }
                        ]
                    }
                ],
                "less-connections": [
                    {
                        "fastDisplay": "[Tarragona ---> Salamanca]",
                        "noOfConnections": 1,
                        "noOfVisitedCities": 2,
                        "departureTimeOfItinerary": "2019-03-12T00:29:09Z",
                        "arrivalTimeOfItinerary": "2019-03-12T03:29:09Z",
                        "timeDurationOfItinerary": "PT3H",
                        "detailedRouteInfo": [
                            {
                                "id": "6a29b25e-2f75-46c4-b72b-a96ac7f33205",
                                "city": {
                                    "name": "Tarragona",
                                    "country": "Spain"
                                },
                                "destinyCity": {
                                    "name": "Salamanca",
                                    "country": "Spain"
                                },
                                "departureTime": "2019-03-12T00:29:09Z",
                                "arrivalTime": "2019-03-12T03:29:09Z"
                            }
                        ]
                    },
                    {
                        "fastDisplay": "[Tarragona ---> Gijon]",
                        "noOfConnections": 1,
                        "noOfVisitedCities": 2,
                        "departureTimeOfItinerary": "2019-03-12T00:29:09Z",
                        "arrivalTimeOfItinerary": "2019-03-12T04:29:09Z",
                        "timeDurationOfItinerary": "PT4H",
                        "detailedRouteInfo": [
                            {
                                "id": "72dbd810-ae2c-4ddb-a198-998d80f0808a",
                                "city": {
                                    "name": "Tarragona",
                                    "country": "Spain"
                                },
                                "destinyCity": {
                                    "name": "Gijon",
                                    "country": "Spain"
                                },
                                "departureTime": "2019-03-12T00:29:09Z",
                                "arrivalTime": "2019-03-12T04:29:09Z"
                            }
                        ]
                    },
                    {
                        "fastDisplay": "[Tarragona ---> Vitoria ---> Santander ---> Logrono]",
                        "noOfConnections": 3,
                        "noOfVisitedCities": 4,
                        "departureTimeOfItinerary": "2019-03-12T00:29:09Z",
                        "arrivalTimeOfItinerary": "2019-03-12T05:29:09Z",
                        "timeDurationOfItinerary": "PT5H",
                        "detailedRouteInfo": [
                            {
                                "id": "fe82a3c4-908c-48c3-b569-ea030c8b4a90",
                                "city": {
                                    "name": "Tarragona",
                                    "country": "Spain"
                                },
                                "destinyCity": {
                                    "name": "Vitoria",
                                    "country": "Spain"
                                },
                                "departureTime": "2019-03-12T00:29:09Z",
                                "arrivalTime": "2019-03-12T01:29:09Z"
                            },
                            {
                                "id": "10d05df9-5542-4a1d-97fb-6f100f52bd01",
                                "city": {
                                    "name": "Vitoria",
                                    "country": "Spain"
                                },
                                "destinyCity": {
                                    "name": "Santander",
                                    "country": "Spain"
                                },
                                "departureTime": "2019-03-12T01:29:09Z",
                                "arrivalTime": "2019-03-12T04:29:09Z"
                            },
                            {
                                "id": "7a6ba369-6a6e-4ea8-80cb-8320e32055e4",
                                "city": {
                                    "name": "Santander",
                                    "country": "Spain"
                                },
                                "destinyCity": {
                                    "name": "Logrono",
                                    "country": "Spain"
                                },
                                "departureTime": "2019-03-12T04:29:09Z",
                                "arrivalTime": "2019-03-12T05:29:09Z"
                            }
                        ]
                    }
                ],
                "less-time": [
                    {
                        "fastDisplay": "[Tarragona ---> Salamanca]",
                        "noOfConnections": 1,
                        "noOfVisitedCities": 2,
                        "departureTimeOfItinerary": "2019-03-12T00:29:09Z",
                        "arrivalTimeOfItinerary": "2019-03-12T03:29:09Z",
                        "timeDurationOfItinerary": "PT3H",
                        "detailedRouteInfo": [
                            {
                                "id": "6a29b25e-2f75-46c4-b72b-a96ac7f33205",
                                "city": {
                                    "name": "Tarragona",
                                    "country": "Spain"
                                },
                                "destinyCity": {
                                    "name": "Salamanca",
                                    "country": "Spain"
                                },
                                "departureTime": "2019-03-12T00:29:09Z",
                                "arrivalTime": "2019-03-12T03:29:09Z"
                            }
                        ]
                    },
                    {
                        "fastDisplay": "[Tarragona ---> Gijon]",
                        "noOfConnections": 1,
                        "noOfVisitedCities": 2,
                        "departureTimeOfItinerary": "2019-03-12T00:29:09Z",
                        "arrivalTimeOfItinerary": "2019-03-12T04:29:09Z",
                        "timeDurationOfItinerary": "PT4H",
                        "detailedRouteInfo": [
                            {
                                "id": "72dbd810-ae2c-4ddb-a198-998d80f0808a",
                                "city": {
                                    "name": "Tarragona",
                                    "country": "Spain"
                                },
                                "destinyCity": {
                                    "name": "Gijon",
                                    "country": "Spain"
                                },
                                "departureTime": "2019-03-12T00:29:09Z",
                                "arrivalTime": "2019-03-12T04:29:09Z"
                            }
                        ]
                    },
                    {
                        "fastDisplay": "[Tarragona ---> Vitoria ---> Santander ---> Logrono]",
                        "noOfConnections": 3,
                        "noOfVisitedCities": 4,
                        "departureTimeOfItinerary": "2019-03-12T00:29:09Z",
                        "arrivalTimeOfItinerary": "2019-03-12T05:29:09Z",
                        "timeDurationOfItinerary": "PT5H",
                        "detailedRouteInfo": [
                            {
                                "id": "fe82a3c4-908c-48c3-b569-ea030c8b4a90",
                                "city": {
                                    "name": "Tarragona",
                                    "country": "Spain"
                                },
                                "destinyCity": {
                                    "name": "Vitoria",
                                    "country": "Spain"
                                },
                                "departureTime": "2019-03-12T00:29:09Z",
                                "arrivalTime": "2019-03-12T01:29:09Z"
                            },
                            {
                                "id": "10d05df9-5542-4a1d-97fb-6f100f52bd01",
                                "city": {
                                    "name": "Vitoria",
                                    "country": "Spain"
                                },
                                "destinyCity": {
                                    "name": "Santander",
                                    "country": "Spain"
                                },
                                "departureTime": "2019-03-12T01:29:09Z",
                                "arrivalTime": "2019-03-12T04:29:09Z"
                            },
                            {
                                "id": "7a6ba369-6a6e-4ea8-80cb-8320e32055e4",
                                "city": {
                                    "name": "Santander",
                                    "country": "Spain"
                                },
                                "destinyCity": {
                                    "name": "Logrono",
                                    "country": "Spain"
                                },
                                "departureTime": "2019-03-12T04:29:09Z",
                                "arrivalTime": "2019-03-12T05:29:09Z"
                            }
                        ]
                    }
                ]
            }
        }
    ```
       

10) If you request again the same itinerary response time is a lot faster due to the fact that
    [Itineraries Lookup Service](https://github.com/chriniko13/itineraries-lookup-service) uses Hazelcast for caching results
    and [Routes Service](https://github.com/chriniko13/routes-service) uses Redis for caching results.
    
11) Screenshots:
    


#### Useful Docker Commands

* `docker ps`

* `docker-compose logs <container_name>`, eg: `docker-compose logs routes-service`

* `docker container ls`

* `docker image ls`

* `docker volume ls`

* `docker network ls`

* `docker info`

* `docker-compose ps`

* `docker-compose images`

#### Useful Docker Commands - Use with caution

* `docker system prune`

* `docker volume prune`

* `docker container prune`

* `docker image prune`
