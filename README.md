# elk-stack

Init
```shell script
cp -n .env.dist .env
```

Run Elasticsearch and Kibana
```shell script
docker-compose -f docker-compose.yml -f docker-compose.kibana.yml up -d
```
