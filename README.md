[![Build Status](http://drone.eu-west-1.prod.aws.skyscanner.local/api/badges/logging-services/grappler-proto-deserializer/status.svg)](http://drone.eu-west-1.prod.aws.skyscanner.local/logging-services/grappler-proto-deserializer)
# Grappler Proto Deserializer
 
Deserializes configured Protobuf streams from `task.inputs` and serializes them 
as JSON to a topic name in the format `<input_topic>_json`.

This project is the successor to [grappler-proto-consumer](http://git.prod.skyscanner.local/logging-services/grappler-proto-consumer).
Be aware: `grappler-proto-consumer` generates JSON with `snake_case` keys, but
this project generates JSON with `camelCase` keys.

## Running locally

With a [grappler-local](http://git.prod.skyscanner.local/logging-services/grappler-local)
stack running, mirror one or more of the configured input streams and then run:

```
mvn package && grp deploy protodeser_dev
```

(see [.jobs.yml](.jobs.yml)). Check that your local job is running in
[YARN](http://yarnnm:8088/cluster).

## Metrics

In addition to the regular Samza metrics, this job will emit the following 
metrics under `net.skyscanner.loggingservices.protodeser.LSProtoDeserializer`:

* `deserialize-from-proto-ms`: time taken to parse Protobuf messages
* `serialize-to-json-ms`: time taken to convert to JSON 
* `failed-parses`: counter (since job started) of how many messages failed to parse.

## Further reading

* [Grappler Protobuf Deserialization](http://git.prod.skyscanner.local/logging-services/getting-started/blob/master/proto_deser.md).
* [Grappler Samza Jobs](http://git.prod.skyscanner.local/logging-services/getting-started/blob/master/samza_jobs.md)

# workplacements_git
