# Index and Shards

> Let's learn about Elasticsearch's Index and Shard
>
> Reference: [Elastic Guide Book - Index and Shards](https://esbook.kimjmin.net/03-cluster/3.2-index-and-shards)

<br>
<br>

- In Elasticsearch, a single data unit is called a `document`, and a collection of documents is called an `index`
- An index is split into units called `shards`, which are distributed and stored across nodes
  - A shard is a Lucene search instance

<br>
<br>

## Primary Shard & Replica

- When creating an index without separate configuration,
  - From version 7.0 onwards, an index consists of 1 shard by default,
  - In versions 6.x and below, it consists of 5
- When nodes are added to the cluster, shards are distributed across each node, and 1 replica is created by default
  - The initially created shard is called `Primary Shard`, and the copy is called `Replica`
  - When there is only 1 node, only the primary shard exists and no replica is created
  - Elasticsearch recommends configuring a minimum of 3 nodes even for the smallest cluster for data availability and integrity!

<br>

![primary_shard_and_replica](../../kor/images/primary_shard_and_replica.png)

- The same `shard` and `replica` contain identical data, and are always **stored on different nodes**
  - In the diagram above, if Node-3 disappears due to system down or network disconnection, the cluster will lose shards 0 and 4 that were on Node-3
  - However, since shards 0 and 4 still remain on other nodes (Node-1, Node-2), the entire data can be used without loss

<br>

 ![node_went_down](../../kor/images/node_went_down.png)

- Initially, the cluster waits for the lost node to recover.
  - However, if it times out and determines the lost node will not return, Elasticsearch begins **replicating** shards 0 and 4 that now only have a single `primary shard` remaining since the replica was lost
  - Even when nodes decrease from 4 to 3, once replication is complete, shards 0-4 maintain 10 total data copies with 5 `primary shards` and 5 `replicas` each
      ![replicated_shard](../../kor/images/replicated_shard.png)
    - This way, through primary shards and replicas, Elasticsearch guarantees data availability and integrity without losing data even when nodes are lost during operation!!

<br>
<br>

## Tips

When a primary shard is lost, a new primary shard is not created; instead, the remaining replica is first promoted to primary shard, and then a new replica is created on another node!
