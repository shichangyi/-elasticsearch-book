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

```

```



> 越近越好
>
> 使用邻近度提高相关度
>
> 性能优化
>
> 寻找相关词



