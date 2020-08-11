
Telemetry data : like for ex time taken to connect to data base. can be visualise using grafana.

# installation 
```bash
docker run -d -p 3000:3000 --name grafana grafana/grafana:6.5.0
```

Grafana is just a tool to visualise , it does not staore data , it pull data from different data source like mysql, graphite, etc.

# Graphite
  1.  A bucket is a collection of telemetry data
  2.  Bucket tree identified by . like aditya.execution.count
  3. value of counter is increased by the value it receives
  4. types : counter , timer , gauge
 ## Statsd  is used for collecting data and passing it to graphite.
  1.  data is sent in the form of plain text
  2.  Use UDP for that(default)
  3.  data format =  <bucker>:<value>|type := example aditya.execuion.count:1|C  # counter will be increased by 1
  
  
  
