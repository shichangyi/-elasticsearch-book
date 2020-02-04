`prefix`

```markdown
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





