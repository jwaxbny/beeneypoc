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

#### SAMPLE: news-crawl

[https://github.com/commoncrawl/news-crawl](https://github.com/commoncrawl/news-crawl)

BUILD
```
> docker build -t newscrawler:1.16 .
```

RUN
```
> docker run --net=host -p 9200:9200 -p 5601:5601 -p 8080:8080 -v /data/elasticsearch -v /data/warc --rm -i -t newscrawler:1.16 /bin/bash
```

#### Urls to Storm, Kibana ElasticSearch

1. Get docker ip
```
> docker inspect <containerid>
```

2. Make sure your firewall is not in the way.

for linux:
```
> ufw allow out on docker0 from 172.17.0.0/16
```

3. After 2-3 minute try to open:

STORM
(http://localhost:8080)[http://localhost:8080]

ELASTICSEARCH
(http://localhost:9200)[http://localhost:9200]

KIBANA
(http://localhost:5601){http://localhost:5601}


