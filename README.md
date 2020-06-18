# beeneypoc
Learn StormCrawler ElasticSearch

## Local Setup (OSX)

### ElasticSearch

[running-open-distro-for-elasticsearch](https://aws.amazon.com/blogs/opensource/running-open-distro-for-elasticsearch/)

1. Install Docker Desktop

2. To Build
```
> docker-compose up
```

3. Confirm Elastic is running
```
> curl -XGET https://localhost:9200 -u admin:admin --insecure
```

3. Kibana
[http://localhost:5601](http://localhost:5601)

```
SAMPLE QUERY (on Demo Website Log data)
Run using Kibana DEV TOOLS panel

GET kibana_sample_data_logs/_search
{
  "query": {
    "bool": {
      "must": [
        {
          "term": {
            "machine.os.keyword": {
              "value": "ios"
            }
          }
        },
        {
          "range": {
            "bytes": {
              "gte": 5000
            }
          }
        },
        {
          "term": {
            "clientip": {
              "value": "68.0.0.0/8"
            }
          }
        }
      ]
    }
  }
}

```

### StormCrawler

[stormcrawler-elasticsearch](https://www.elastic.co/blog/stormcrawler-open-source-web-crawler-strengthened-by-elasticsearch-kibana)


