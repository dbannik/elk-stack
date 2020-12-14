# elk-stack

## Initialize
```shell script
cp -n .env.dist .env
```

## Run Elasticsearch and Kibana
```shell script
docker-compose -f docker-compose.yml -f docker-compose.kibana.yml up -d
```

## Create alias docker compose
```shell script
echo "docker-compose -f docker-compose.yml -f docker-compose.kibana.yml \$@" > ./docker-compose
chmod +x ./docker-compose
```
