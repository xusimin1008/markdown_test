```
商品评论查询：
{
  "query": {
    "filtered": {
      "query": {
        "bool": {
          "should": [
            {
              "multi_match": {
                "query": "service",
                "fields": [
                  "summary",
                  "content"
                ]
              }
            }
          ]
        }
      },
      "filter": {
        "and": [
          {
            "match": {
              "product_id": "B00AWKJPOA"
            }
          },
          {
            "term": {
              "rating": "1.0"
            }
          }
        ]
      }
    }
  }
}
```
