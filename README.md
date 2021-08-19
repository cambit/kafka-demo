
docker exec -it connect mkdir -p /tmp/kafka-connect/examples
docker cp ./connectors/source-csv-filepulse-00/example.csv connect://tmp/kafka-connect/examples/example.csv


File progress
docker exec -it -e KAFKA_OPTS="" connect kafka-console-consumer  --topic filepulse-xml-01 --from-beginning --bootstrap-server broker:29092



===========================
If you think you’ve got string/JSON data…

You can use console tools including kafkacat and kafka-console-consumer. My personal preference is kafkacat:

$ kafkacat -b localhost:9092 -t users-json-noschema -C -c1
{
  "registertime":1493356576434,"userid":"User_8","regionid":"Region_2","gender":"MALE"}

Using the excellent jq, you can also validate and format the JSON:

$ kafkacat -b localhost:9092 -t users-json-noschema -C -c1|jq '.'
{
  "registertime": 1493356576434,
  "userid": "User_8",
  "regionid": "Region_2",
  "gender": "MALE"
}