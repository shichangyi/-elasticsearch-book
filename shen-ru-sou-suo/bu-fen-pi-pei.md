# [**prefix 前缀查询**](https://www.elastic.co/guide/cn/elasticsearch/guide/current/prefix-query.html)

```markdown
# prefix 查询是低级查询， 查询方式是去扫描 倒排索引的 terms, 然后获取id
# prefix 性能比较慢，而且只能是前缀匹配， 实现 mysql 的 like 11111115*
POST /bigcrmindex/_search?routing=21299
{
  "query": {
    "bool": {
      "must": [
        {
          "prefix": {
            "f_email": {
              "value": "11111115"
            }
          }
        },
        {
          "term": {
            "f_corp_id": {
              "value": 21299
            }
          }
        }
      ]
    }
  },
  "_source": ["f_email"]
}
```

# [通配符与正则表达式查询](https://www.elastic.co/guide/cn/elasticsearch/guide/current/_wildcard_and_regexp_queries.html)

```markdown
# wildcard  查询原理 跟 prefix 一样， 只是支持通配符，都是扫描 terms
# regexp    查询原理 跟 prefix 一样， 只是支持通配符，都是扫描 terms
# wildcard   & regexp & prefix 不会对查询词做人和分析的， 不区分大小写，原样查询

GET /my_index/address/_search
{
    "query": {
        "wildcard": {
            "postcode": "W?F*HW" 
        }
    }
}

GET /my_index/address/_search
{
    "query": {
        "regexp": {
            "postcode": "W[0-9].+" 
        }
    }
}
```

# [查询时输入即搜索](https://www.elastic.co/guide/cn/elasticsearch/guide/current/_query_time_search_as_you_type.html)

```markdown
# 如何实现用户一边输入， 一边查询呢
# 可以使用 match_phrase_prefix, 跟 match_phrase原理类似， 不同的是。它的原理如下
# johnnie 开始
# 跟着 walker
# 跟着以 bl 开始的词 ， 其中 bl 是部分查询， 相当于 bl*, 这个查询， 使用的是 prefix
{
    "match_phrase_prefix" : {
        "brand" : {
            "query": "walker johnnie bl", 
            "slop":  10
        }
    }
}
```

# [索引时优化](https://www.elastic.co/guide/cn/elasticsearch/guide/current/_index_time_optimizations.html)

# 

# [Ngrams 在部分匹配的应用](https://www.elastic.co/guide/cn/elasticsearch/guide/current/_ngrams_for_partial_matching.html)

# 

# [索引时输入即搜索](https://www.elastic.co/guide/cn/elasticsearch/guide/current/_index_time_search_as_you_type.html)

# 

# [Ngrams 在复合词的应用](https://www.elastic.co/guide/cn/elasticsearch/guide/current/ngrams-compound-words.html)



