# tempo-elastic-example

This demo repo is a simple example of using Elasticsearch, Grafana and Tempo together to log and discover traces.

1. Run `docker-compose up` in the root of the repo to start all applications.
    
   Note that filebeat has a 30s delay before starting.  This is b/c it will fail to start if Elastic/Kibana have not already started

1. Once Elasticsearh has started use the following command to create a `logfmt` pipeline that will be used by filebeat:
   ```
   curl --user elastic:changeme -X PUT -H 'Content-Type: application/json'  --data @./pipeline.json http://localhost:9200/_ingest/pipeline/logfmt
   ```

   This pipeline processor is used to parse logfmt.  Unfortunately, filebeat does not seem capable of this on its own and so we rely on these fantastic and almost certainly wrong regexes to parse them for us.

   If you are interested in using logfmt with Elastic then logstash with [this plugin](https://github.com/wheely/logstash-filter-logfmt) may be a better route.

   Regexes are slightly modified versions of the ones found in [this issue](https://github.com/elastic/elasticsearch/issues/31786).
  
1. Navigate to Grafana at http://localhost:3000 

1. Go to Explore and choose Elasticsearch as your datasource.  Make sure that for "Metric" you have chosen "Logs"

1. Execute the following query to find log lines with traceIDs

   `container.image.name:"grafana/tns-app:latest" and _exists_:traceID`

1. Expand the log line and click the Tempo link to go to Tempo.