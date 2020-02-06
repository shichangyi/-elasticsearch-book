[高阶概念](https://www.elastic.co/guide/cn/elasticsearch/guide/current/aggs-high-level.html)

* [尝试聚合](https://www.elastic.co/guide/cn/elasticsearch/guide/current/_aggregation_test_drive.html)
* [条形图](https://www.elastic.co/guide/cn/elasticsearch/guide/current/_building_bar_charts.html)
* [按时间统计](https://www.elastic.co/guide/cn/elasticsearch/guide/current/_looking_at_time.html)
* [范围限定的聚合](https://www.elastic.co/guide/cn/elasticsearch/guide/current/_scoping_aggregations.html)

```
#多指标桶
POST /index_*,bigcrmindex/_search
{
  "size": 0, 
  "query": {
    "term": {
      "f_corp_id": {
        "value": "21299"
      }
    }
  }, 
  "aggs": {
    "nums21299": {
      "terms": {
        "field": "f_step",
        "size": 10
      }
    },
    "all":{
       "sum": {
        "field": "f_step"
      }
    }
  }
}

#局部-all 对比桶
POST /index_*,bigcrmindex/_search
{
  "size": 0, 
  "query": {
    "term": {
      "f_corp_id": {
        "value": "21299"
      }
    }
  }, 
  "aggs": {
    "nums21299": {
      "terms": {
        "field": "f_step",
        "size": 10
      }
    },
    "all":{
      "global": {}, # 全局桶
      "aggs": {
        "allNUms": {
           "terms": {
              "field": "f_step",
              "size": 10
            }
          }
        }
    }
  }
}



```

* [过滤和聚合](https://www.elastic.co/guide/cn/elasticsearch/guide/current/_filtering_queries_and_aggregations.html)

* [多桶排序](https://www.elastic.co/guide/cn/elasticsearch/guide/current/_sorting_multivalue_buckets.html)

* [近似聚合](https://www.elastic.co/guide/cn/elasticsearch/guide/current/_approximate_aggregations.html)

* [通过聚合发现异常指标](https://www.elastic.co/guide/cn/elasticsearch/guide/current/significant-terms.html)

* [Doc Values and Fielddata](https://www.elastic.co/guide/cn/elasticsearch/guide/current/docvalues-and-fielddata.html)

* [总结](https://www.elastic.co/guide/cn/elasticsearch/guide/current/_closing_thoughts.html)



