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

# `prefix`

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



