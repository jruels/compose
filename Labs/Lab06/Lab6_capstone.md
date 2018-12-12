# Docker-Compose Capstone Project
You will have the chance to create your own docker-compose application project and shared with the class. 

You can use your favorite open source docker-compose applications repos, create your own docker-compose repos, or using the existing Labs here.

### Networks
* front-tier
* back-tier 

Review the example compose file 
`compose-network/docker-compose.yml`
```
version: "3"

services:
  vote:
    build: ./vote
    command: python app.py
    volumes:
     - ./vote:/app
    ports:
      - "5000:80"
    networks:
      - front-tier
      - back-tier

  result:
    build: ./result
    command: nodemon server.js
    volumes:
      - ./result:/app
    ports:
      - "5001:80"
      - "5858:5858"
    networks:
      - front-tier
      - back-tier

  worker:
    build:
      context: ./worker
    depends_on:
      - "redis"
    networks:
      - back-tier

  redis:
    image: redis:alpine
    container_name: redis
    ports: ["6379"]
    networks:
      - back-tier

  db:
    image: postgres:9.4
    container_name: db
    volumes:
      - "db-data:/var/lib/postgresql/data"
    networks:
      - back-tier

volumes:
  db-data:

networks:
  front-tier:
  back-tier:
```

The architecture of the application is: 
![](Lab5_networks/F3421A7B-ABC6-4253-99D0-7AF7B8C84B30.png)

Now let’s launch the application 
```
docker-compose -f compose-network/docker-compose.yml up -d 
```

Confirm the application started successfully 
```
docker-compose ps 
```

Now if things look good load up the voting app and the results app in a browser. 

#### Voting Application 
http://localhost:5000/

![](Lab5_networks/E077D77F-D369-4291-AB6F-CC1DF3AF49C1.png)


#### Results Application 
http://localhost:5001/


![](Lab5_networks/9C2EF934-073B-4A6D-93FA-6B57DA660F48.png)

## Lab Complete