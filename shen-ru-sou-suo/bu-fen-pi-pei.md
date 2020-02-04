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


```



