# Ambiente Kong API Gateway

Ambiente de execucao do Kong API Gateway usando ferramenta docker-compose

## Ferramentas necessarias
* docker
* docker-compose
* editor *.yaml


## Ferramentas que serao provisionadas usando o docker-compose
* Fluent-Bit
* Kibana
* ElasticSearch
* Jaeger
* Grafana
* Prometheus
* Prometheus Node Exporter

### Arquivos de configuracao fluent-bit

Na pasta [fluent-bit](compose/fluent-bit) contem os arquivos necessarios para configuracao da ferramenta, o docker-compose utilizara esta pasta para montar as configuracoes


### Arquivos de configuracao prometheus

Na pasta [prom-conf](compose/prom-conf) contem os arquivos necessarios para configuracao do prometheus, inclusive a configuracao de _scraping_ das metricas do Kong API Gateway


## Rodando

Na pasta raiz do projeto voce pode executar

```shell
docker-compose -f compose/kong_compose.yml up -d
```

Documentação dos plugins: 
https://docs.konghq.com/hub/

Gerando nossa imagem do Kong: 
docker build -t rodrigordavila/kong-fc docke/.

Derrubando os containers: 
docker-compose -f compose/kong_compose.yml down

URL de configuração do Konga: 
http://localhost:1337/

Api administrativa do Kong:
local - http://kong:8001

```shell
curl --location 'http://localhost:80/api/bets' \
--header 'Content-Type: application/json' \
--data-raw '{
    "match": "1X-DC",
    "email": "joe@doe.com",
    "championship": "Uefa Champions League",
    "awayTeamScore": "2",
    "homeTeamScore": "3"
}'
```


Plugins:
Correlation-id
Rate limit
Response Transformer

Consumers: 
Plugin de segurança de que irá consumir a API
Basic Auth
Api Keys


Monitoramento:
http://localhost:3000/ Grafana
Add plugin Prometheus nos plugins globais
Add no grafana Data sources Protmetheus (http://prometheus:9090)
Importe dashboard Grafana .json
https://grafana.com/grafana/dashboards/7424-kong-official/