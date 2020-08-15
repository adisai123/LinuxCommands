
Telemetry data : like for ex time taken to connect to data base. can be visualise using grafana.

# installation 
```bash
docker run -d -p 3000:3000 --name grafana grafana/grafana:6.5.0
```

db configuration file : grafana.ini  (remove ; in that file . After modification restart grafana) 

Grafana is just a tool to visualise , it does not staore data , it pull data from different data source like mysql, graphite, etc.

# Graphite
  1.  A bucket is a collection of telemetry data
  2.  Bucket tree identified by . like aditya.execution.count
  3. value of counter is increased by the value it receives
  4. types : counter , timer , gauge
  5. Graphite made up of front end (graphite web ) and backend (carbon)
  6. front end has a database to store graphs you created.(default sqlite)(also external database is also possible) (you can alos enable cacheing using memcache)
  7. carbon has carbon cache , also whisper database is also there to store data.
  8. installation : sudo apt-get install graphite-web graphite-carbon
  9.  sudo vim /etc/default/graphite-carbon 
  10. storage policy  cat /etc/carbon/storage-schemas.conf (how log bucket will be set has this setting)
  11.  Docker grafana , graphite , stastd : https://hub.docker.com/r/hopsoft/graphite-statsd/   
        docker pull hopsoft/graphite-statsd
        
        ```
        docker run -d\
 --name graphite\
 --restart=always\
 -p 80:80\
 -p 81:81\
 -p 2003-2004:2003-2004\
 -p 2023-2024:2023-2024\
 -p 8125:8125/udp\
 -p 8126:8126\
 hopsoft/graphite-statsd
 ```
 
 statsd :sending data
 echo "$2:1|c"  | nc -w 1 -u $1 8125
 ## Statsd  is used for collecting data and passing it to graphite.
  1.  data is sent in the form of plain text
  2.  Use UDP for that(default)
  3.  data format =  <bucker>:<value>|type := example aditya.execuion.count:1|C  # counter will be increased by 1
  
  dynaamic variale
  
  you can add annotation on graph (kind of tool tips)
  
  alerts , email(notification) (if range cross , add rules)
  
  counter , gauge , heatmap 
  
  
  influxdb : - its timeseries databases
  Telegraf is a metrics collection series
  
