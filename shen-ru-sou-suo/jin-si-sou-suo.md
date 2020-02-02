> 短语匹配

```
什么是短语
一个被认定为和短语 quick brown fox 匹配的文档，必须满足以下这些要求：

quick 、 brown 和 fox 需要全部出现在域中。
brown 的位置应该比 quick 的位置大 1 。
fox 的位置应该比 quick 的位置大 2 。


查询 
GET /my_index/my_type/_search
{
    "query": {
        "match_phrase": {
            "title": "quick brown fox"
        }
    }
}
```

> 混合起来

```

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



