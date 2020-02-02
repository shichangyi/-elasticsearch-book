> 短语匹配

```markdown
# match_phrase

GET /my_index/my_type/_search
{
    "query": {
        "match_phrase": {
            "title": "quick brown fox"
        }
    } 
}

#什么情况下会被命中
```

> 混合起来

```markdown
# slop 参数的意义
GET /my_index/my_type/_search
{
    "query": {
        "match_phrase": {
            "title": "quick brown fox",
            "slop" : 10
        }
    } 
}
```

> 多值字段

```markdown
# 下面的情况， 在 es2.x 是一样的， match_phrase 搜索 Abraham Lincoln 都可以查询出数据
# 在es7.4 不存在这样的情况
# 理论上， 多词字段的情况是有问题的，
PUT /my_index/groups/1
{
    "names": [ "John Abraham", "Lincoln Smith"]
}

PUT /my_index/groups/1
{
    "names": [ "John Abraham Lincoln Smith"]
}

# 为了解决这个问题， 引入了参数: "position_increment_gap": 100
# 表示在多词字段中， 相邻的词间隔100
PUT /my_index/_mapping/groups 
{
    "properties": {
        "names": {
            "type":                "string",
            "position_increment_gap": 100
        }
    }
}
```

> 越近越好

```markdown
#邻近查询 — 一个 slop 大于 0，
#越近， 查询相关度越大
```

> 使用邻近度提高相关度

```markdown
# 场景 查询 "quick brown fox", 期望 查询相关度 按如下优先级返回
# 1. 精确包含 quick brown fox 查询出来
# 2，如果 quick this brown fox 也能查询出来
# 3. quick fox , fox 也能搜索出来

#解决办法， 
# 1.使用 match 对 quick brown fox 查询， 将返回大量的文档， 在 match 里面
# 2. 使用近视查询 来增强 分数， 调整相关性， 越相关，越靠前

## 代码如下

GET /my_index/my_type/_search
{
  "query": {
    "bool": {
      "must": {
        "match": { # 匹配大多数文档
          "title": {
            "query":  "quick brown fox",
            "minimum_should_match": "30%" # 减尾减支，消除太多不相干的文档
          }
        }
      },
      "should": {  # should 被用来增强分数， 调整相关性
        "match_phrase": { # 近视匹配
          "title": {
            "query": "quick brown fox",
            "slop":  50
          }
        }
      }
    }
  }
}
```

> 性能优化

```markdown
# match_phrase 比 term 查询慢10倍
# 临近查询 比 term 慢 20 倍
# 提升临近查询性能的思路， 就是减少临近查询 匹配的文档
# rescore 是一个好的思路， 只是使用 临近查询来修正 match 每个分片前 50 的文档的分数
POST bigcrmindex/_search?routing=21299
{
  "query": {
    "match": {
      "f_name": "六度人和"
    }
  },
  "rescore": { # 重排分数
    "query": {
      "rescore_query":{
        "match_phrase": {
          "f_name": "六度人和"
        }
      }
    },
    "window_size": 50  # 重排每个分片的前50
  },

  "_source": ["f_name","f_company"]
}
```

> 找相关词

```

```



