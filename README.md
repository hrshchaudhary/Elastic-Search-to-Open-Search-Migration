# Elastic-Search-to-Open-Search-Migration
If you are thinking of migrating Elastic Search to Open Search this repo is for you. This repo provides rest high level client.
Basically there are three steps which are to be used:

1. Provisiong an Open Search Cluster
2. Setup Authentication mechanism of OS cluster (IAM role (recommended way), master username and password, etc)
3. Dump data from Elastic Search to Open Search.

## Details
This repo assumes that step 1 and step 2 are already done.
Talking about dumping data. <br />
There is [elasticdump](https://github.com/elasticsearch-dump/elasticsearch-dump) tool which is used to dump data from one elastic search cluster to another. You just need to make compatible the open search cluster with the elastic search version used, for which nice details are provided as [upgrade paths](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/version-migration.html) by aws. <br />
To dump indexes you need to follow a path:

1. Dump Settings <br />
   ```shell
   elasticdump --input=<es-host>:9200/<index> --output=https://<username>:<percentage-encoded-password>@<opensearch-domain-endpoint>/<index> --type=settings
   ```
2. Dump Alias (If any) <br />
   ```shell
   elasticdump --input=<es-host>:9200/<index> --output=https://<username>:<percentage-encoded-password>@<opensearch-domain-endpoint>/<index> --type=alias
   ```
3. Dump Mapping <br />
   ```shell
   elasticdump --input=<es-host>:9200/<index> --output=https://<username>:<percentage-encoded-password>@<opensearch-domain-endpoint>/<index> --type=mapping
   ```
4. Dump Data
   ```shell
   elasticdump --input=<es-host>:9200/<index> --output=https://<username>:<percentage-encoded-password>@<opensearch-domain-endpoint>/<index> --type=data
   ```
