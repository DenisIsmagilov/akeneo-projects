# Proof of concept to improve category research

## Generate documents tokenized by category path

A product belonging to "node_1/node_2/node_3" will be tokenized.
So, it will belong, for ES, to: "node_1", "node_1/node_2", "node_1/node_2/node_3".

```
$ export NUMBER_TREE=4
$ export TREE_DEPTH=4
$ export NUMBER_CHILDREN_PER_CATEGORY=12
$ export NUMBER_PRODUCTS=10000
$ export NUMBER_CATEGORY_PER_PRODUCT=5
$ export ES_REQUEST_DIRECTORY=/var/tmp/poc
$ chmod +x ./generate_and_load.sh
$ ./generate_and_load.sh
```

```
curl -X POST \
  http://localhost:9200/poc_categories/_msearch \
  -H 'content-type: application/x-ndjson' \
  -d '{ "index" : "poc_categories"}
{"size":0, "query" : {"constant_score": {"filter": {"term": { "categories" : "node_2/node_10/node_1"}}}}}
{ "index" : "poc_categories"}
{"size":0, "query" : {"constant_score": {"filter": {"term": { "categories" : "node_2/node_9/node_4"}}}}}
'
```
