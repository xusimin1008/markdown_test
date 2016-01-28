1. 不能删除某个type的mapping， 只能重建索引，
2. 设置action.destructive_requires_name=true，使其只能通过index名称来删除索引，不能使用_all或通配符
3. 不能删除mapping中的某个字段，只能重建索引
4. 可以直接往index中添加新的type，或往type中添加新的filed [Put Mapping](https://www.elastic.co/guide/en/elasticsearch/reference/current/indices-put-mapping.html)
