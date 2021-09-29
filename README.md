# FLiP-Jetson

## Build

```

docker exec 03ecc2709715 solr delete -c jetson

docker exec 03ecc2709715 solr create -c jetson

java -jar target/IoTProducer-1.0-jar-with-dependencies.jar --serviceUrl pulsar://localhost:6650 --topic 'iotjetsonjson' --message

bin/pulsar-admin sink stop --name solr-sink-jetson --namespace default --tenant public
bin/pulsar-admin sinks delete --tenant public --namespace default --name solr-sink-jetson
bin/pulsar-admin sinks create --archive ./connectors/pulsar-io-solr-2.8.0.nar --tenant public --namespace default --name solr-sink-jetson --sink-config-file conf/solr-sink-jetson.yml --inputs iotjetsonjson --parallelism 1


bin/pulsar-admin sinks get --tenant public --namespace default --name solr-sink-jetson
bin/pulsar-admin sinks status --tenant public --namespace default --name solr-sink-jetson


go get -u "github.com/apache/pulsar-client-go/pulsar"
go mod tidy

```

## Reference

* https://github.com/tspannhw/FLiP-Energy/blob/main/README.md
* https://github.com/tspannhw/minifi-xaviernx/blob/master/demo.py
* https://github.com/tspannhw/FLiP-SQL
* https://github.com/tspannhw/FLiP-IoT
* https://pulsar.apache.org/docs/en/client-libraries-go/
