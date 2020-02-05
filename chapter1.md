[高阶概念](https://www.elastic.co/guide/cn/elasticsearch/guide/current/aggs-high-level.html)

* [尝试聚合](https://www.elastic.co/guide/cn/elasticsearch/guide/current/_aggregation_test_drive.html)
* [条形图](https://www.elastic.co/guide/cn/elasticsearch/guide/current/_building_bar_charts.html)

```
POST /bigcrmindex,index_*/_search
{
  "size": 0, 
  "query": {
    "range": {
      "f_create_time": {
        "gte": 1546272000000,
        "lte": 1577808000000
      }
    }
  }, 
  "aggs": {
    "create": {
      "terms": {
        "script": "(doc['f_create_time'][0] - 1546272000000L) / (86400000L * 30)",
        "size": 100
      }
    }
  }
}
```

* [按时间统计](https://www.elastic.co/guide/cn/elasticsearch/guide/current/_looking_at_time.html)

```
POST /bigcrmindex,index_*/_search
{
  "size": 0, 
  "query": {
    "range": {
      "f_create_time": {
        "gte": 1546272000000,
        "lte": 1677808000000
      }
    }
  }, 
  "aggs": {
    "create": {
      "date_histogram": {
        "script": "doc['f_create_time'][0]",
        "calendar_interval": "1M",
        "format": "yyyy-MM-dd" 
      }
    }
  }
}


 "aggs": {
    "create": {
      "date_histogram": {
        "script": "doc['f_create_time'][0]",
        "calendar_interval": "1y",
        "format": "yyyy" ,
        "extended_bounds": { # 数据不冲。数据集合 包括 2019 到 2020， 但是可能还有其他
          "min": "2019",
          "max": "2020"
        }
      }
    }
  }
  
  
```

* [范围限定的聚合](https://www.elastic.co/guide/cn/elasticsearch/guide/current/_scoping_aggregations.html)

```

```

* [过滤和聚合](https://www.elastic.co/guide/cn/elasticsearch/guide/current/_filtering_queries_and_aggregations.html)
* [多桶排序](https://www.elastic.co/guide/cn/elasticsearch/guide/current/_sorting_multivalue_buckets.html)
* [近似聚合](https://www.elastic.co/guide/cn/elasticsearch/guide/current/_approximate_aggregations.html)
* [通过聚合发现异常指标](https://www.elastic.co/guide/cn/elasticsearch/guide/current/significant-terms.html)
* [Doc Values and Fielddata](https://www.elastic.co/guide/cn/elasticsearch/guide/current/docvalues-and-fielddata.html)
* [总结](https://www.elastic.co/guide/cn/elasticsearch/guide/current/_closing_thoughts.html)



