### Adidas Backend Assignment


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



#### How to run it?
TODO