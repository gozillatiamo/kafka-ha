# Kafka high availability

```bash
docker network create monitoring
```

## Start Kafka Cluster

## KRaft

```bash
cd kafka && docker compose --profile all up -d
```

OR to specific datacenter

```bash
cd kafka && docker compose --profile dc1 up -d
```

to scale down

```bash
cd kafka && docker compose --profile all up -d --scale {service_name}=0
```

## ZooKeeper

Lagacy way

```bash
cd kafka/zookeeper && docker compose up -d
```

## Create topic

```bash
kafka-topics.sh --bootstrap-server localhost:19092 --topic user --create --partitions 3 --replication-factor 3
```

## Producer connectivity

```bash
kafka-console-producer.sh \
--broker-list localhost:19092,localhost:29092,localhost:39092 \
--topic user \
--request-required-acks all \
--property "parse.key=true" \
--property "key.separator=:"
```

## Consumer connectivity

```bash
kafka-console-consumer.sh \
--bootstrap-server {broker_host:port} \
--topic user \
--group brokers \
--property "print.key=true"
```

## Management & Monitoring

### Start all

```bash
cd monitors & docker compose --profile all up -d
```

### Start Confluent only (do not run this for now.)

```bash
cd monitors & docker compose --profile confluent up -d
```

### Start garfana only

```bash
cd monitors & docker compose --profile grafana up -d
```

### Start kafka-ui only

```bash
cd monitors & docker compose --profile kafka-ui up -d
```

### JMX Metric

- broker: <http://localhost:9999/metrics>
- controller: <http://localhost:9998/metrics>

### Prometheus

- targets: <http://localhost:9090/targets?search=>

### Grafana

- dashboard: <http://localhost:3000/dashboards>
- alerting: <http://localhost:3000/alerting/list>

### kafka-ui

- dashboard: <http://localhost:8080>

### confluent-control-center

- dashboard: <http://localhost:9021>
