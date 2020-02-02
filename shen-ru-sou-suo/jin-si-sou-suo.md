> 短语匹配

```
基本格式
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

```
slop 参数的意义
```

xxx  this is

```
GET /my_index/my_type/_search
{
    "query": {
        "match_phrase": {
            "title": {
                "query": "quick fox",
                "slop":  1
            }
        }
    }
}
```

> 多值字段
>
> 越近越好
>
> 使用邻近度提高相关度
>
> 性能优化
>
> 寻找相关词



