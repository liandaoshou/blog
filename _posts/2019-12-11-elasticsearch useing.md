---
layout: post
title:  "docker安装elasticsearch及常用操作"
date:   2019-12-11 08:20:00 +0800
categories: docker 
tag: docker
---

# 安装elasticsearch
```
docker pull elasticsearch:7.2.0
```
下载完毕后启动es

```
docker run --name elasticsearch -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" -d elasticsearch:7.2.0
```
浏览器中打开http://localhost:9200 看到以下表示安装成功

```
{
  "name" : "530dd7820315",
  "cluster_name" : "docker-cluster",
  "cluster_uuid" : "7O0fjpBJTkmn_axwmZX0RQ",
  "version" : {
    "number" : "7.2.0",
    "build_flavor" : "default",
    "build_type" : "docker",
    "build_hash" : "508c38a",
    "build_date" : "2019-06-20T15:54:18.811730Z",
    "build_snapshot" : false,
    "lucene_version" : "8.0.0",
    "minimum_wire_compatibility_version" : "6.8.0",
    "minimum_index_compatibility_version" : "6.0.0-beta1"
  },
  "tagline" : "You Know, for Search"
}
```

修改配置，解决跨域

```
docker exec -it elasticsearch /bin/bash
cd /usr/share/elasticsearch/config/
vi elasticsearch.yml
```

在elasticsearch.yml的文件末尾加上:
```
http.cors.enabled: true
http.cors.allow-origin: "*"
```

修改配置后重启容器
```
docker restart elasticsearch
```

概念介绍

索引: 含有相同属性的文档集合

类型：索引可以定义一个或多个类型，文档必须属于一个类型

文档：文档是可以被索引的基础数据单位

api的基本格式

API基本格式 http://ip:port/索引/类型/文档

分片： 每个索引都有多个分片，每个分片是一个lucene索引  分片shard是es分布式系统的高可用方案
es会将一份数据分解在不同的机器上，默认是5份，备份shard默认为1，每个分片都有一个备份，
如果其中一个分片宕机，将由备份进行其他请求操作实现高可用，相同分片不能和相对于的备份存储同一机器。

备份： 拷贝一份分片就完成分片的备份

# 安装kibana
```
docker pull kibana:7.2.0
```
等待下载完毕

```
docker run --name kibana --link=elasticsearch:test  -p 5601:5601 -d kibana:7.2.0
 
docker start kibana
```

稍等一会
浏览器打开 http://localhost:5601/即可正常访问


#kibana dev_tools 常见使用
##新增
```$xslt
PUT /people 创建索引

POST /people/man/ 为索引添加数据类型自动创建

{
"name":"123"
}
```

##更新
```$xslt
POST /people/man/X5619G4BJkJic-QduVA-/_update

{
    "doc":{
    "name":"222"
    }
}
```
##删除
```$xslt
DELETE /people/man/X5619G4BJkJic-QduVA-

DELETE /people
```
##查询
```$xslt
GET _search
{
"query": {
"match_all": {}
}
}      
查询所有


GET _search
{
    "query":{
        "match_all":{

        }
    },
    "from":0,
    "size":3
}   
添加分页 from从第几个开始size几个


GET _search
{
    "query":{
        "match_all":{

        }
    },
    "sort":[
        {
            "age":{
                "order":"desc"
            }
        }
    ],
    "_source":[
        "age"
    ]
}      
根据年龄排序 _source显示相关的字段即可 查看更方便


GET _search
{
    "query":{
        "match":{
            "name":"elasticSearch入门 "
        }
    }
} 

es会将elasticSearch入门  进行拆分为elasticSearch和入门  进行匹配只要匹配其中一个都会进行返回


GET _search
{
    "query":{
        "match_phrase":{
            "name":"rabbitmq"
        }
    }
}  

这个是完整匹配必须一模一样的才进行返回如 rabbitmq    rabbitmq  A 但是rabbitAmq不行

GET _search
{
    "query":{
        "terms":{
            "name":[
                "php",
                "ajax"
            ]
        }
    }
} 

查询名字是php 和ajax的doc 完全匹配

GET _search
{
    "query":{
        "term":{
            "score":"479"
        }
    }
}

一个terms和term term会将作为一个完整的查询匹配不会进行分词匹配


GET _search
{

    "query":{
        "range":{
            "score":{
                "gte":400,
                "lte":500
            }
        }
    }
}
 
范围查询400-500分数的doc   可以比较时间now表示当前时间

GET _search
{
    "size":0,
    "aggs":{
        "group_haha":{
            "terms":{
                "field":"age"
            }
        }
    }
} 

聚合查询查询相同年级的人数有多少个 group_haha随便定义都可以


GET _search
{
    "size":0,
    "aggs":{
        "group_haha":{
            "terms":{
                "field":"age"
            }
        },
        "group_hehe":{
            "terms":{
                "field":"score"
            }
        }
    }
}

可以进行多个聚合同时返回

GET _search
{
    "size":0,
    "aggs":{
        "group_stats":{
            "stats":{
                "field":"score"
            }
        }
    }
} 

可以进行计算返回最大最小平均总和也可以直接查询最小 将关键字stats、改为min或max


GET /tvs/sales/_search
{
    "size":0,
    "query":{
        "term":{
            "brand":{
                "value":"小米"    先进行筛选
            }
        }
    },
    "aggs":{
        "group_by_color":{
            "terms":{
                "field":"color"  对筛选的数据进行聚合
            }
        }
    }
}

按每种颜色的平均销售额降序排序


GET /tvs/sales/_search
{
    "size":0,
    "aggs":{
        "group_by_color":{
            "terms":{
                "field":"color",
                "order":{
                    "avg_price":"asc"
                }
            },
            "aggs":{
                "avg_price":{
                    "avg":{
                        "field":"price"  //计算出每种颜色的平均价然后进行排序
                    }
                }
            }
        }
    }
}

GET _search
{
    "query":{
        "query_string":{
            "query":"(java and jianqiao) OR scala"
        }
    }
}
```


批量操作
```
GET /_mget
{
    "docs":[
        {
            "_index":"people",
            "_type":"man",
            "_id":"AWs_K3KEYHh6lG16ttAX"
        },
        {
            "_index":"people",
            "_type":"man",
            "_id":"AWs_LJiZYHh6lG16ttAZ"
        }
    ]
} 
 一次查询多条doc

GET /people/_mget
{
    "docs":[
        {
            "_type":"man",
            "_id":"AWs_K3KEYHh6lG16ttAX"
        },
        {
            "_type":"wuman",
            "_id":"AWs_LJiZYHh6lG16ttAZ"
        }
    ]
} 
一次查询多条doc 可以指定不同的type

GET /people/man/_mget
{
"ids":["AWs_LJiZYHh6lG16ttAZ"]
}

如果都在同一个index和type中指定ids查询

在查询多条记录的时候使用mget可以提升es的销量
```