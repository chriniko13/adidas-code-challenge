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



#### How to run it?
TODO
