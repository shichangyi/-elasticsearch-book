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
>
> 使用邻近度提高相关度
>
> 性能优化
>
> 寻找相关词



