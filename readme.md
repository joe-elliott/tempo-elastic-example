- docker-compose up
  - wait :(
- curl --user elastic:changeme -X PUT -H 'Content-Type: application/json' --data @./pipeline.json http://localhost:9200/_ingest/pipeline/logfmt
  -  curl --user elastic:changeme http://localhost:9200/_ingest/pipeline/logfmt
  - mostly works
- localhost:3000
- Explore -> Elasticsearch -> Metrics -> Logs
- `container.image.name:"grafana/tns-app:latest" and _exists_:traceID`
