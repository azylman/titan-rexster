# Docker image for Titan graph database with DynamoDB backend

Titan is a free, open source database that is capable of processing
extremely large graphs and it supports a variety of indexing and storage backends,
which makes it easier to extend than some popular NoSQL Graph databases.

This docker image instantiaties a Titan graph database that integrates with DynamoDB as a storage
backend.

## Titan

This container is using Titan 0.5.4. Please refer to
its [page](https://github.com/thinkaurelius/titan/wiki/Downloads) for more information.

## Tinkerpop and Rexster

[Tinkerpop](http://www.tinkerpop.com/) is a vendor-independent API specification for
manipulating and access Graph databases.

[Rexster](https://github.com/tinkerpop/rexster/wiki) is a service that provides protocols
for accessing a graph database. Currently it supports two protocols:
	- REST over HTTP: Human-readable and good for testing
	- RexPro: Binary Protocol for performence

If you'd like to avoid vendor lock-in, then I'd recommend using Rexster as the API
for accessing your Graph database. It has support for popular graph databases,
so you can avoid refactoring your code. Take a look at Tinkerpop Gremlin for a
Groovy-DSL for querying graphs to see how RexPro and Gremlin provide syntactical
elegance to query graphs.

## Running

The minimum system requirements for this stack is 1 GB with 2 cores.

```
docker run image_name
```

It requires four environment variables:
  * **DYNAMODB_HOSTPORT** - where to access dynamo, e.g. https://dynamodb.us-west-1.amazonaws.com
  * **AWS_ACCESS_KEY_ID**
  * **AWS_SECRET_ACCESS_KEY**
  * **GRAPH_NAME** - name of the graph

### Ports

8182: HTTP port for REST API

8183: RexPro for native access (Binary protocol)

8184: JMX Port (You won't need to use this, probably)

You can read more about it in the Rexster documentation.

To test out the REST API (over Boot2docker):

```
curl http://localhost:<port-mapped-to-8182>/graphs/graph/vertices
```
