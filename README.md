# elk_mysql_docker

this is a example to use elk with mysql data in docker-compose

after git clone

use command docker-compose up to build & run image of elk & mysql 

* in /mysql/db/init.sql this will auto generate sample when docker-compose up

* need to change password in elk config and docker-compose restart


you can test elastic api in kibana dev tool

elastic api
  * list all indexes     
    * GET /_cat/indices
  * query all data in index
    * POST /_index/_search
        {
          "query":{
            "match_all": {}
          }
        }
  * fuzzy query
    * POST /_index/_search
        {
          "sort":[{"id":"desc"}],
          "size": 100, 
          "query":{
            "match_phrase": {
              "field": "value"
              }
            }
          }
        }
     * POST /member/_search
        {
          "sort":[{"id":"desc"}],
          "size": 100, 
          "query": {
            "bool": {
              "must": [
                {
                  "wildcard": {
                    "field": {
                      "property": "*text*"
                    }
                  }
                }
              ]
            }
          }
        }
   
 * insert document into index
   * POST _index/_doc/_id
        {
          "field1" : "value1",
          "field2" : "value2"
        }     
* delete index
  * DELETE /member

* delete data in index
  * POST /member/_delete_by_query
        {
          "query" : { 
                "match_all" : {}
            }
        }







Reference 
* https://github.com/deviantony/docker-elk
* https://godleon.github.io/blog/Elasticsearch/Elasticsearch-getting-started/
* https://www.tutorialspoint.com/elasticsearch/index.htm




