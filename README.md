## Bank App using Akka Cassandra

### Architecture

_"Bank"_ application
- each bank account is a persistent actor
- all events are recorded (created, update etc)
- all events are replayed in cased of failure/restart
- one big bank (persistent) actor manages all actors
- a HTTP server with a REST API handles requests
- all events are stored in Cassandra

### Routes

#### POST: Add new bank account
```shell
curl -v http://localhost:8080/bank -H 'Content-Type: application/json' -d '{"user":"atzz", "currency":"USD", "balance": 1000.0}'
```

#### GET: Retrieve details of a bank account
```shell
curl -v http://localhost:8080/bank/6b5c59fa-fea1-4f7d-ae47-baacf2647eef
```

#### PUT: Update existing bank account
```shell
curl -v -X PUT http://localhost:8080/bank/f08d03ea-6740-4c6e-91c8-3216b144629a -H 'Content-Type: application/json' -d '{"currency":"USD", "amount": 112098.0}'
```