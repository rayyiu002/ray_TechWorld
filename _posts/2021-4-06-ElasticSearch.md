---
category: Notes
url_path: '/notes'
title: 'ElasticSearch'

layout: null
---

## Description
+ Open source, Java-based, RESTful search engine
+ Built on top of Apache Lucene
+ Search and index document files in diverse formats
+ The response of queries are in JSON format 


### 1. Indices and Types

+ 1.1 API　Example

```localhost:9200/test/users/1```

```{
       "city": "cityID123"
   }
```


### 2. Mapping, Indexing 

+ 2.1 Mapping - Create index by specifying the types

```PUT localhost:9200/test/
   {
       "mappings": {
           "users": {
               "properties": {
                   "age": {
                       "type": "long"
                   },
                   "first_name": {
                       "type": "string"
                   },
                   "gender": {
                       "type": "string"
                   },
                   "level": {
                       "type": "string"
                   },
                   "last_name": {
                       "type": "string"
                   }
               }
           }
       }
   }
```

+ 2.2 Indexing - Make data being searchable by the index API/
E.g. Mark following user with index "test"
```POST localhost:9200/test/users/
   {
       "first_name": "Johnny",
       "last_name": "Knoxville",
       "gender": "male",
       "level": "awesome",
       "age": 45
   }
```

+ 2.3 Searching

Search API
```POST localhost:9200/test/users/_search```

Response
```{
  "took": 4,
  "timed_out": false,
  "_shards": {
    "total": 5,
    "successful": 5,
    "failed": 0
  },
  "hits": {
    "total": 3,
    "max_score": 1,
    "hits": [
      {
        "_index": "test",
        "_type": "users",
        "_id": "AVRQQlCE0YBBUjDwpzQZ",
        "_score": 1,
        "_source": {
          "first_name": "Bam",
          "last_name": "Margera",
          "gender": "male",
          "level": "super awesome",
          "age": 36
        }
      },
      ...
    ]
  }
}
```

+2.4 Boost
Matches on the title field will have twice the weight as those on the content field, which has the default boost of 1.0.

```
 GET /_search
 {
   "query": {
     "bool": {
       "should": [
         {
           "match": {
             "title": {
               "query": "quick brown fox",
               "boost": 2 
             }
           }
         },
         {
           "match": { 
             "content": "quick brown fox"
           }
         }
       ]
     }
   }
 }
```

### 3. Advanced Searching

+ 3.1 Search by keyword in specific field

'Match' Query API to get the record with field contains "keyword" (full-text searching)
```
POST localhost:9200/test/users/_search

{
    "query": {
        "match": {
            "field": "keyword"
        }
    }
}
```

Response
```
{
  "took": 19,
  "timed_out": false,
  "_shards": {
    "total": 5,
    "successful": 5,
    "failed": 0
  },
  "hits": {
    "total": 3,
    "max_score": 0.2712221,
    "hits": [
      {
        "_index": "test",
        "_type": "users",
        "_id": "AVRQQlCE0YBBUjDwpzQZ",
        "_score": 0.2712221,
        "_source": {
          "field": "keyword 1",
          ...
        }
      },
      {
        "_index": "test",
        "_type": "users",
        "_id": "AVRQRtYW0YBBUjDwpzQa",
        "_score": 0.09848769,
        "_source": {
          "field": "keyword 2",
          ...
        }
      },
      {
        "_index": "test",
        "_type": "users",
        "_id": "AVRQRx-E0YBBUjDwpzQf",
        "_score": 0.09848769,
        "_source": {
          "field": "keyword 3",
          ...
        }
      }
    ]
  }
}
```
+ 3.2 Search by keyword in specific field with exact match

'Term' Query API to get the record with field equal to "keyword" (exact value) 
```
POST localhost:9200/test/users/_search

{
     "query": {
        "term": {
            "field": "keyword"
        }
    }
}

```

+ 3.3 Search by filtering

'Term' Query API to get the record with field equal to "keyword" (exact value) 
```
POST localhost:9200/test/users/_search

{
    "query": {
        "bool": {
            "must": [
                {
                    "match": {
                        "level": "super awesome"
                    }
                },
                {
                    "range": {
                        "age": {
                            "lt": 40
                        }
                    }
                }
            ],
            "filter": {
                "match": {
                    "gender": "male"
                }
            }
        }    
    }
}
```
+ 3.4 More API Examples

+ Basic Match Query for searching keyword in all fields
```GET /bookdb_index/book/_search?q=keyword```

+ Basic Match Query for searching keyword in particular field
```GET /bookdb_index/book/_search?q=field:keyword```

+ Bool Query
 + Must (equivalent to AND), Must_not (equivalent to NOT), Should (equivalent to OR)
```
POST /bookdb_index/book/_search
{
  "query": {
    "bool": {
      "must": {
        "bool" : { 
          "should": [
            { "match": { "title": "Elasticsearch" }},
            { "match": { "title": "Solr" }} 
          ],
          "must": { "match": { "authors": "clinton gormely" }} 
        }
      },
      "must_not": { "match": {"authors": "radu gheorge" }}
    }
  }
}
```

+ Fuzzy  Query
```
POST /bookdb_index/book/_search
{
    "query": {
        "multi_match" : {
            "query" : "comprihensiv guide",
            "fields": ["title", "summary"],
            "fuzziness": "AUTO"
        }
    },
    "_source": ["xxx", "yyy"],
    "size": 1
}
```

+ Wildcard Query for searching a specified pattern to match
```
POST /bookdb_index/book/_search
{
    "query": {
        "wildcard" : {
            "authors" : "t*"
        }
    },
    "_source": ["xxx", "yyy"],
    "highlight": {
        "fields" : {
            "field1" : "Test"
        }
    }
}
```

+ Regexp Query (Similar to Wildcard query but supports more complex patterns)
```
POST /bookdb_index/book/_search
{
    "query": {
        "regexp" : {
            "authors" : "t[a-z]*y"
        }
    },
    "_source": ["xxx", "yyy"],
    "highlight": {
        "fields" : {
            "field1" : "Test"
        }
    }
}
```

+ Query String (Similar to Multi_match query but concise shorthand syntax)
```
POST /bookdb_index/book/_search
{
    "query": {
        "simple_query_string" : {
            "query": "(saerch~1 algorithm~1) + (grant ingersoll)  | (tom morton)",
            "fields": ["title", "authors" , "summary^2"]
        }
    },
    "_source": [ "title", "summary", "authors" ],
    "highlight": {
        "fields" : {
            "summary" : {}
        }
    }
} 
```

+ Term Query with sorting
```
POST /bookdb_index/book/_search
{
    "query": {
        "term" : {
            "publisher": "manning"
        }
    },
    "_source" : ["title","publish_date","publisher"],
    "sort": [
        { "publish_date": {"order":"desc"}}
    ]
}
```

+ Range Query
```
POST /bookdb_index/book/_search
{
    "query": {
        "range" : {
            "publish_date": {
                "gte": "2015-01-01",
                "lte": "2015-12-31"
            }
        }
    },
    "_source" : ["title","publish_date","publisher"]
}
```

### Reference
+ [https://dzone.com/articles/an-introduction-to-elasticsearch](https://dzone.com/articles/an-introduction-to-elasticsearch)
+ [23-useful-elasticsearch-example-queries](https://dzone.com/articles/23-useful-elasticsearch-example-queries)
