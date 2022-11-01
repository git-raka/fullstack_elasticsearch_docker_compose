# fullstack elasticsearch

### Create directory 
```
mkdir ~/elastic && cd ~/elastic
```

### Create instances.yml
```
vi instances.yml
``` 
https://github.com/git-raka/fullstack_elasticsearch_docker_compose/blob/73a0445f5da0b97a45421395dc29d96cf6d56956/instances.yml#L1-L26

### Create environtment file
```
vi .env
```
https://github.com/git-raka/fullstack_elasticsearch_docker_compose/blob/752729ab0553606c4017d3aca4013ae300c4d21e/.env#L1-L3

### Create Kibana config
```
vi kibana.yml
```
https://github.com/git-raka/fullstack_elasticsearch_docker_compose/blob/752729ab0553606c4017d3aca4013ae300c4d21e/kibana.yml#L1-L15

### Create the certfile
```
vim create-certs.yml
```
https://github.com/git-raka/fullstack_elasticsearch_docker_compose/blob/752729ab0553606c4017d3aca4013ae300c4d21e/create-certs.yml#L1-L29

### Create Docker Compose File
```
vim docker-compose.yml
```
https://github.com/git-raka/fullstack_elasticsearch_docker_compose/blob/0c6a432c192ebad76c95bc6ede9b59653af23228/docker-compose.yml#L1-L127

### Generate Certificates
```
docker-compose -f create-certs.yml run --rm create_certs
```
<img width="769" alt="image" src="https://user-images.githubusercontent.com/77326619/199182914-bdd7bc58-d137-449f-bb78-522cd5aa0a7f.png">


### Bring up the dev cluster
```
docker-compose up -d
```
<img width="777" alt="image" src="https://user-images.githubusercontent.com/77326619/199183046-d8f0e7c3-5471-4768-aab6-46914fd516f5.png">

### Generate password for the instance
```
docker exec es01 /bin/bash -c "bin/elasticsearch-setup-passwords \
auto --batch --url https://es01:9200"
```
<img width="778" alt="image" src="https://user-images.githubusercontent.com/77326619/199183184-e0350c80-2508-4d6b-ad47-5dee6f52d9eb.png">

write down the output

```
Changed password for user apm_system
PASSWORD apm_system = QQLaZMXVPIweAF95pAFN

Changed password for user kibana_system
PASSWORD kibana_system = OP5J01VeD10mdkK9FDst

Changed password for user kibana
PASSWORD kibana = OP5J01VeD10mdkK9FDst

Changed password for user logstash_system
PASSWORD logstash_system = rNOYXcWfVx7zW3ksvggB

Changed password for user beats_system
PASSWORD beats_system = 1FCpGAUPPNZqBqKlChbt

Changed password for user remote_monitoring_user
PASSWORD remote_monitoring_user = 07s30JzSXqcJkXHpsCTh

Changed password for user elastic
PASSWORD elastic = AMGKZ7xDWcpaQtXWGzff
```
### Replace the “CHANGEME” with previous password to kibana_system in docker-compose.yml and kibana.yml
```
sed -i 's|CHANGEME|\"OP5J01VeD10mdkK9FDst\"|g' docker-compose.yml
sed -i 's|CHANGEME|OP5J01VeD10mdkK9FDst|g' kibana.yml
```
<img width="767" alt="image" src="https://user-images.githubusercontent.com/77326619/199183565-7a262646-c6ba-4443-b426-a2ceef2adedd.png">

### restart docker-compose
```
docker-compose down
```
<img width="776" alt="image" src="https://user-images.githubusercontent.com/77326619/199183700-5c2210e3-827c-4c31-a614-95b6b9a87340.png">
```
docker-compose up -d
```
<img width="777" alt="image" src="https://user-images.githubusercontent.com/77326619/199183812-0bf5d04c-147a-46e9-a325-4f7ec00a4160.png">

## Open lab in browser
Login to you lab kibana instance with the ip of the host.
*https://host.ip:5601*

use elastic / AMGKZ7xDWcpaQtXWGzff from the output above to login.
# And of course.. Get some coffee and go outside and get some fresh air when the installation is running.
