# 《 实验三: 聚合练习操作》

> **学院：省级示范性软件学院**
>
> **课程：高级数据库技术与应用**
>
> **题目：**《 实验三: 聚合练习操作》
>
> **姓名：** 刘双硕
>
> **学号：** 2100150421
>
> **班级：** 软工2201
>
> **日期：** 2024-10-31
>
> **实验环境：** elasticsearch-8.12.2 kibana-8.12.2

## 一、实验目的

通过本次实验，让我深入理解Elasticsearch中的聚合（Aggregations）概念，包括它的作用和在数据处理中的重要性。通过编写和执行聚合查询，我将增强自己的对es语法的了解。



## 二、实验内容

1. 统计每个产品类别的总销售额。

   - 代码段

     ```elasticsearch
     POST /ecommerce/_search?
     {
       "size": 0,
       "aggs": {
         "total_sales_per_category": {
           "terms": {
             "field": "product_category"
           },
           "aggs": {
             "total_sales": {
               "sum": {
                 "field": "total_amount"
               }
             }
           }
         }
       }
     }
     ```

   - 文字解释:

     先通过product_category聚合创建产品类别的桶,然后使用sum进行对销售额的聚合求得总销售额.

   - 操作成功的代码段

     ```elasticsearch
     {
       "took": 13,
       "timed_out": false,
       "_shards": {
         "total": 1,
         "successful": 1,
         "skipped": 0,
         "failed": 0
       },
       "hits": {
         "total": {
           "value": 100,
           "relation": "eq"
         },
         "max_score": null,
         "hits": []
       },
       "aggregations": {
         "total_sales_per_category": {
           "doc_count_error_upper_bound": 0,
           "sum_other_doc_count": 0,
           "buckets": [
             {
               "key": "Jewelry",
               "doc_count": 14,
               "total_sales": {
                 "value": 17477.37028503418
               }
             },
             {
               "key": "Electronics",
               "doc_count": 13,
               "total_sales": {
                 "value": 18941.559997558594
               }
             },
             {
               "key": "Home Appliances",
               "doc_count": 13,
               "total_sales": {
                 "value": 25865.190231323242
               }
             },
             {
               "key": "Beauty",
               "doc_count": 11,
               "total_sales": {
                 "value": 22708.94012451172
               }
             },
             {
               "key": "Furniture",
               "doc_count": 10,
               "total_sales": {
                 "value": 17228.31996154785
               }
             },
             {
               "key": "Books",
               "doc_count": 9,
               "total_sales": {
                 "value": 11878.820098876953
               }
             },
             {
               "key": "Groceries",
               "doc_count": 9,
               "total_sales": {
                 "value": 16172.980072021484
               }
             },
             {
               "key": "Fashion",
               "doc_count": 8,
               "total_sales": {
                 "value": 7073.110048294067
               }
             },
             {
               "key": "Toys",
               "doc_count": 7,
               "total_sales": {
                 "value": 10528.830047607422
               }
             },
             {
               "key": "Sports",
               "doc_count": 6,
               "total_sales": {
                 "value": 13250.500122070312
               }
             }
           ]
         }
       }
     }
     ```

     

2. 计算每个城市的平均订单金额。

   - 代码段

     ```elasticsearch
     POST /ecommerce/_search?
     {
       "size": 0,
       "aggs": {
         "avg_order_sales_per_city": {
           "terms": {
             "field": "customer_city"
           },
           "aggs": {
             "avg_order_sales": {
               "avg": {
                 "field": "total_amount"
               }
             }
           }
         }
       }
     }
     ```

     

   - 文字解释:

     先按照cunstomer_city进行聚合得到每个城市的桶,然后使用avg聚合total_amount得到平均订单的金额.

   - 操作成功的代码段

     ```elasticsearch
     {
       "took": 2,
       "timed_out": false,
       "_shards": {
         "total": 1,
         "successful": 1,
         "skipped": 0,
         "failed": 0
       },
       "hits": {
         "total": {
           "value": 100,
           "relation": "eq"
         },
         "max_score": null,
         "hits": []
       },
       "aggregations": {
         "avg_order_sales_per_city": {
           "doc_count_error_upper_bound": 0,
           "sum_other_doc_count": 0,
           "buckets": [
             {
               "key": "Los Angeles",
               "doc_count": 13,
               "avg_order_sales": {
                 "value": 1482.7977142333984
               }
             },
             {
               "key": "San Diego",
               "doc_count": 13,
               "avg_order_sales": {
                 "value": 1878.4761915940505
               }
             },
             {
               "key": "San Jose",
               "doc_count": 12,
               "avg_order_sales": {
                 "value": 1587.2216771443684
               }
             },
             {
               "key": "Philadelphia",
               "doc_count": 11,
               "avg_order_sales": {
                 "value": 1370.19365345348
               }
             },
             {
               "key": "New York",
               "doc_count": 10,
               "avg_order_sales": {
                 "value": 1801.9510040283203
               }
             },
             {
               "key": "Chicago",
               "doc_count": 9,
               "avg_order_sales": {
                 "value": 1062.1610989040798
               }
             },
             {
               "key": "Houston",
               "doc_count": 9,
               "avg_order_sales": {
                 "value": 1735.199978298611
               }
             },
             {
               "key": "Dallas",
               "doc_count": 8,
               "avg_order_sales": {
                 "value": 1291.8024978637695
               }
             },
             {
               "key": "Phoenix",
               "doc_count": 8,
               "avg_order_sales": {
                 "value": 2315.7625274658203
               }
             },
             {
               "key": "San Antonio",
               "doc_count": 7,
               "avg_order_sales": {
                 "value": 1607.7128516605922
               }
             }
           ]
         }
       }
     }
     ```

     

3. 找出销量最高的前5个产品。

   - 代码段

     ```elasticsearch
     POST /ecommerce/_search?
     {
       "size": 0,
       "aggs": {
         "top_5_products": {
           "terms": {
             "field": "product_id",
             "size": 5,
             "order": {
               "total_quantity": "desc"
             }
           },
           "aggs": {
             "total_quantity": {
               "sum": {
                 "field": "quantity"
               }
             }
           }
         }
       }
     }
     ```

     

   - 文字解释:

     先按照product_id进行聚合得到产品的桶,然后使用sum聚合quantity得到每个产品的销售量,然后使用销售量进行降序排序,然后设置size=5取得前五个,得到销量最高的前5个产品.

   - 操作成功的代码段

     ```elasticsearch
     {
       "took": 8,
       "timed_out": false,
       "_shards": {
         "total": 1,
         "successful": 1,
         "skipped": 0,
         "failed": 0
       },
       "hits": {
         "total": {
           "value": 100,
           "relation": "eq"
         },
         "max_score": null,
         "hits": []
       },
       "aggregations": {
         "top_5_products": {
           "doc_count_error_upper_bound": -1,
           "sum_other_doc_count": 84,
           "buckets": [
             {
               "key": "P031",
               "doc_count": 4,
               "total_quantity": {
                 "value": 13
               }
             },
             {
               "key": "P005",
               "doc_count": 3,
               "total_quantity": {
                 "value": 11
               }
             },
             {
               "key": "P021",
               "doc_count": 3,
               "total_quantity": {
                 "value": 11
               }
             },
             {
               "key": "P076",
               "doc_count": 3,
               "total_quantity": {
                 "value": 11
               }
             },
             {
               "key": "P099",
               "doc_count": 3,
               "total_quantity": {
                 "value": 11
               }
             }
           ]
         }
       }
     }
     ```

     

4. 计算男性和女性客户的平均年龄。

   - 代码段

     ```elasticsearch
     POST /ecommerce/_search?
     {
       "size": 0,
       "aggs": {
         "average_age_by_gender": {
           "terms": {
             "field": "customer_gender"
           },
           "aggs": {
             "average_age": {
               "avg": {
                 "field": "customer_age"
               }
             }
           }
         }
       }
     }
     ```

     

   - 文字解释:

     先按customer_gender进行聚合得到性别的桶,然后avg聚合customer_age,得到平均年龄.

   - 操作成功的代码段

     ```elasticsearch
     {
       "took": 2,
       "timed_out": false,
       "_shards": {
         "total": 1,
         "successful": 1,
         "skipped": 0,
         "failed": 0
       },
       "hits": {
         "total": {
           "value": 100,
           "relation": "eq"
         },
         "max_score": null,
         "hits": []
       },
       "aggregations": {
         "average_age_by_gender": {
           "doc_count_error_upper_bound": 0,
           "sum_other_doc_count": 0,
           "buckets": [
             {
               "key": "male",
               "doc_count": 55,
               "average_age": {
                 "value": 45.61818181818182
               }
             },
             {
               "key": "female",
               "doc_count": 45,
               "average_age": {
                 "value": 43.888888888888886
               }
             }
           ]
         }
       }
     }
     ```

     

5. 统计每种支付方式的使用次数和总金额。

   - 代码段

     ```elasticsearch
     POST /ecommerce/_search?
     {
       "size": 0,
       "aggs": {
         "payment_methods": {
           "terms": {
             "field": "payment_method"
           },
           "aggs": {
             "count": {
               "value_count": {
                 "field": "order_id"
               }
             },
             "total_amount": {
               "sum": {
                 "field": "total_amount"
               }
             }
           }
         }
       }
     }
     ```

     

   - 文字解释:

     先按支付方式创建桶,然后使用count,sum分别聚合order_id,total_amount,得到使用次数和总金额.

   - 操作成功的代码段

     ```elasticsearch
     {
       "took": 2,
       "timed_out": false,
       "_shards": {
         "total": 1,
         "successful": 1,
         "skipped": 0,
         "failed": 0
       },
       "hits": {
         "total": {
           "value": 100,
           "relation": "eq"
         },
         "max_score": null,
         "hits": []
       },
       "aggregations": {
         "payment_methods": {
           "doc_count_error_upper_bound": 0,
           "sum_other_doc_count": 0,
           "buckets": [
             {
               "key": "Cash on Delivery",
               "doc_count": 29,
               "total_amount": {
                 "value": 38746.55044555664
               },
               "count": {
                 "value": 29
               }
             },
             {
               "key": "Debit Card",
               "doc_count": 29,
               "total_amount": {
                 "value": 48975.19040107727
               },
               "count": {
                 "value": 29
               }
             },
             {
               "key": "Credit Card",
               "doc_count": 22,
               "total_amount": {
                 "value": 36358.470153808594
               },
               "count": {
                 "value": 22
               }
             },
             {
               "key": "PayPal",
               "doc_count": 20,
               "total_amount": {
                 "value": 37045.40998840332
               },
               "count": {
                 "value": 20
               }
             }
           ]
         }
       }
     }
     ```

     

6. 计算每月的总销售额。

   - 代码段

     ```elasticsearch
     POST /ecommerce/_search?
     {
       "size": 0,
       "aggs": {
         "total_sales_per_month": {
           "date_histogram": {
             "field": "order_date",
             "calendar_interval": "month"
           },
           "aggs": {
             "total_sales": {
               "sum": {
                 "field": "total_amount"
               }
             }
           }
         }
       }
     }
     ```

     

   - 文字解释:

     先对order_date按月为间隔创建桶,然后使用sum聚合total_amount得到每个月的总销售额.

   - 操作成功的代码段

     ```elasticsearch
     {
       "took": 14,
       "timed_out": false,
       "_shards": {
         "total": 1,
         "successful": 1,
         "skipped": 0,
         "failed": 0
       },
       "hits": {
         "total": {
           "value": 100,
           "relation": "eq"
         },
         "max_score": null,
         "hits": []
       },
       "aggregations": {
         "total_sales_per_month": {
           "buckets": [
             {
               "key_as_string": "2023-01-01T00:00:00.000Z",
               "key": 1672531200000,
               "doc_count": 12,
               "total_sales": {
                 "value": 24381.61993408203
               }
             },
             {
               "key_as_string": "2023-02-01T00:00:00.000Z",
               "key": 1675209600000,
               "doc_count": 11,
               "total_sales": {
                 "value": 18870.850006103516
               }
             },
             {
               "key_as_string": "2023-03-01T00:00:00.000Z",
               "key": 1677628800000,
               "doc_count": 10,
               "total_sales": {
                 "value": 17959.33026123047
               }
             },
             {
               "key_as_string": "2023-04-01T00:00:00.000Z",
               "key": 1680307200000,
               "doc_count": 9,
               "total_sales": {
                 "value": 18775.959869384766
               }
             },
             {
               "key_as_string": "2023-05-01T00:00:00.000Z",
               "key": 1682899200000,
               "doc_count": 10,
               "total_sales": {
                 "value": 11713.169967651367
               }
             },
             {
               "key_as_string": "2023-06-01T00:00:00.000Z",
               "key": 1685577600000,
               "doc_count": 9,
               "total_sales": {
                 "value": 6771.1600341796875
               }
             },
             {
               "key_as_string": "2023-07-01T00:00:00.000Z",
               "key": 1688169600000,
               "doc_count": 7,
               "total_sales": {
                 "value": 9110.010131835938
               }
             },
             {
               "key_as_string": "2023-08-01T00:00:00.000Z",
               "key": 1690848000000,
               "doc_count": 8,
               "total_sales": {
                 "value": 12135.870210647583
               }
             },
             {
               "key_as_string": "2023-09-01T00:00:00.000Z",
               "key": 1693526400000,
               "doc_count": 3,
               "total_sales": {
                 "value": 8615.500122070312
               }
             },
             {
               "key_as_string": "2023-10-01T00:00:00.000Z",
               "key": 1696118400000,
               "doc_count": 6,
               "total_sales": {
                 "value": 12106.000183105469
               }
             },
             {
               "key_as_string": "2023-11-01T00:00:00.000Z",
               "key": 1698796800000,
               "doc_count": 6,
               "total_sales": {
                 "value": 8176.529968261719
               }
             },
             {
               "key_as_string": "2023-12-01T00:00:00.000Z",
               "key": 1701388800000,
               "doc_count": 9,
               "total_sales": {
                 "value": 12509.620300292969
               }
             }
           ]
         }
       }
     }
     ```

     

7. 找出平均订单金额最高的前3个客户。

   - 代码段

     ```elasticsearch
     POST /ecommerce/_search?
     {
       "size": 0,
       "aggs": {
         "top_3_avg_order_customer": {
           "terms": {
             "field": "customer_id",
             "size": 3,
             "order": {
               "avg_order_sales": "desc"
             }
           },
           "aggs": {
             "avg_order_sales": {
               "avg": {
                 "field": "total_amount"
               }
             }
           }
         }
       }
     }
     ```

     

   - 文字解释:

     先按customer_id进行聚合得到客户的桶,然后avg聚合total_amount得到平均订单金额,然后使用order对平均订单金额进行降序排序,然后设置size=3,得到前三位客户.

   - 操作成功的代码段

     ```elasticsearch
     {
       "took": 5,
       "timed_out": false,
       "_shards": {
         "total": 1,
         "successful": 1,
         "skipped": 0,
         "failed": 0
       },
       "hits": {
         "total": {
           "value": 100,
           "relation": "eq"
         },
         "max_score": null,
         "hits": []
       },
       "aggregations": {
         "top_3_avg_order_customer": {
           "doc_count_error_upper_bound": -1,
           "sum_other_doc_count": 97,
           "buckets": [
             {
               "key": "C977",
               "doc_count": 1,
               "avg_order_sales": {
                 "value": 4886.10009765625
               }
             },
             {
               "key": "C543",
               "doc_count": 1,
               "avg_order_sales": {
                 "value": 4858.9501953125
               }
             },
             {
               "key": "C165",
               "doc_count": 1,
               "avg_order_sales": {
                 "value": 4816.60009765625
               }
             }
           ]
         }
       }
     }
     ```

     

8. 计算每个年龄段（18-30，31-50，51+）的客户数量。

   - 代码段

     ```elasticsearch
     POST /ecommerce/_search?
     {
       "size": 0,
       "aggs": {
         "age_groups": {
           "range": {
             "field": "customer_age",
             "ranges": [
               { "from": 18, "to": 30 },
               { "from": 31, "to": 50 },
               { "from": 51 }
             ]
           }
         }
       }
     ```

     

   - 文字解释:

     按客户年龄为18-30,31-50,51- ... 聚合为三个桶,得到其用户数量.

   - 操作成功的代码段

     ```elasticsearch
     {
       "took": 2,
       "timed_out": false,
       "_shards": {
         "total": 1,
         "successful": 1,
         "skipped": 0,
         "failed": 0
       },
       "hits": {
         "total": {
           "value": 100,
           "relation": "eq"
         },
         "max_score": null,
         "hits": []
       },
       "aggregations": {
         "age_groups": {
           "buckets": [
             {
               "key": "18.0-30.0",
               "from": 18,
               "to": 30,
               "doc_count": 24
             },
             {
               "key": "31.0-50.0",
               "from": 31,
               "to": 50,
               "doc_count": 31
             },
             {
               "key": "51.0-*",
               "from": 51,
               "doc_count": 42
             }
           ]
         }
       }
     }
     ```

     

9. 计算每个产品类别的平均单价。

   - 代码段

     ```elasticsearch
     POST /ecommerce/_search?
     {
       "size": 0,
       "aggs": {
         "average_price_per_category": {
           "terms": {
             "field": "product_category"
           },
           "aggs": {
             "average_price": {
               "avg": {
                 "field": "price"
               }
             }
           }
         }
       }
     }
     ```

     

   - 文字解释:

     按prodect_category进行聚合,得到产品类别的桶,然后avg聚合price得到平均单价

   - 操作成功的代码段

     ```elasticsearch
     {
       "took": 2,
       "timed_out": false,
       "_shards": {
         "total": 1,
         "successful": 1,
         "skipped": 0,
         "failed": 0
       },
       "hits": {
         "total": {
           "value": 100,
           "relation": "eq"
         },
         "max_score": null,
         "hits": []
       },
       "aggregations": {
         "average_price_per_category": {
           "doc_count_error_upper_bound": 0,
           "sum_other_doc_count": 0,
           "buckets": [
             {
               "key": "Jewelry",
               "doc_count": 14,
               "average_price": {
                 "value": 537.6807218279157
               }
             },
             {
               "key": "Electronics",
               "doc_count": 13,
               "average_price": {
                 "value": 484.44461763822113
               }
             },
             {
               "key": "Home Appliances",
               "doc_count": 13,
               "average_price": {
                 "value": 645.6961549612192
               }
             },
             {
               "key": "Beauty",
               "doc_count": 11,
               "average_price": {
                 "value": 701.0781749378551
               }
             },
             {
               "key": "Furniture",
               "doc_count": 10,
               "average_price": {
                 "value": 518.5519981384277
               }
             },
             {
               "key": "Books",
               "doc_count": 9,
               "average_price": {
                 "value": 524.0977762010363
               }
             },
             {
               "key": "Groceries",
               "doc_count": 9,
               "average_price": {
                 "value": 566.4644444783529
               }
             },
             {
               "key": "Fashion",
               "doc_count": 8,
               "average_price": {
                 "value": 369.4774992465973
               }
             },
             {
               "key": "Toys",
               "doc_count": 7,
               "average_price": {
                 "value": 485.97999899727955
               }
             },
             {
               "key": "Sports",
               "doc_count": 6,
               "average_price": {
                 "value": 483.9566599527995
               }
             }
           ]
         }
       }
     }
     ```

     

10. 找出订单数量最多的前5个城市。

    - 代码段

      ```elasticsearch
      POST /ecommerce/_search?
      {
        "size": 0,
        "aggs": {
          "top_5_cities": {
            "terms": {
              "field": "customer_city",
              "size": 5
            }
          }
        }
      }
      ```

      

    - 文字解释:

      按customer_city聚合得到每个城市的桶,因为Terms默认按文档数量降序排列,size=5可以得到订单数量最多的前5个城市.

    - 操作成功的代码段

      ```elasticsearch
      {
        "took": 3,
        "timed_out": false,
        "_shards": {
          "total": 1,
          "successful": 1,
          "skipped": 0,
          "failed": 0
        },
        "hits": {
          "total": {
            "value": 100,
            "relation": "eq"
          },
          "max_score": null,
          "hits": []
        },
        "aggregations": {
          "top_5_cities": {
            "doc_count_error_upper_bound": 0,
            "sum_other_doc_count": 41,
            "buckets": [
              {
                "key": "Los Angeles",
                "doc_count": 13
              },
              {
                "key": "San Diego",
                "doc_count": 13
              },
              {
                "key": "San Jose",
                "doc_count": 12
              },
              {
                "key": "Philadelphia",
                "doc_count": 11
              },
              {
                "key": "New York",
                "doc_count": 10
              }
            ]
          }
        }
      }
      ```

      

11. 计算每个季度的平均订单金额。

    - 代码段

      ```elasticsearch
      POST /ecommerce/_search?
      {
        "size": 0,
        "aggs": {
          "average_order_amount_per_quarter": {
            "date_histogram": {
              "field": "order_date",
              "calendar_interval": "quarter"
            },
            "aggs": {
              "average_amount": {
                "avg": {
                  "field": "total_amount"
                }
              }
            }
          }
        }
      }
      ```

      

    - 文字解释:

      按季度对订单时间进行分桶,然后avg聚合得到total_amount

    - 操作成功的代码段

      ```elasticsearch
      {
        "took": 2,
        "timed_out": false,
        "_shards": {
          "total": 1,
          "successful": 1,
          "skipped": 0,
          "failed": 0
        },
        "hits": {
          "total": {
            "value": 100,
            "relation": "eq"
          },
          "max_score": null,
          "hits": []
        },
        "aggregations": {
          "average_order_amount_per_quarter": {
            "buckets": [
              {
                "key_as_string": "2023-01-01T00:00:00.000Z",
                "key": 1672531200000,
                "doc_count": 33,
                "average_amount": {
                  "value": 1854.9030364065459
                }
              },
              {
                "key_as_string": "2023-04-01T00:00:00.000Z",
                "key": 1680307200000,
                "doc_count": 28,
                "average_amount": {
                  "value": 1330.724638257708
                }
              },
              {
                "key_as_string": "2023-07-01T00:00:00.000Z",
                "key": 1688169600000,
                "doc_count": 18,
                "average_amount": {
                  "value": 1658.9655813641018
                }
              },
              {
                "key_as_string": "2023-10-01T00:00:00.000Z",
                "key": 1696118400000,
                "doc_count": 21,
                "average_amount": {
                  "value": 1561.530973888579
                }
              }
            ]
          }
        }
      }
      ```

      

12. 统计每个产品类别中的商品数量。

    - 代码段

      ```elasticsearch
      POST /ecommerce/_search?
      {
        "size": 0,
        "aggs": {
          "product_count_per_category": {
            "terms": {
              "field": "product_category"
            },
            "aggs": {
              "product_count": {
                "value_count": {
                  "field": "product_id"
                }
              }
            }
          }
        }
      }
      ```

      

    - 文字解释:

      按商品种类进行分桶,然后value_count进行聚合,得到商品数量.

    - 操作成功的代码段

      ```elasticsearch
      {
        "took": 2,
        "timed_out": false,
        "_shards": {
          "total": 1,
          "successful": 1,
          "skipped": 0,
          "failed": 0
        },
        "hits": {
          "total": {
            "value": 100,
            "relation": "eq"
          },
          "max_score": null,
          "hits": []
        },
        "aggregations": {
          "product_count_per_category": {
            "doc_count_error_upper_bound": 0,
            "sum_other_doc_count": 0,
            "buckets": [
              {
                "key": "Jewelry",
                "doc_count": 14,
                "product_count": {
                  "value": 14
                }
              },
              {
                "key": "Electronics",
                "doc_count": 13,
                "product_count": {
                  "value": 13
                }
              },
              {
                "key": "Home Appliances",
                "doc_count": 13,
                "product_count": {
                  "value": 13
                }
              },
              {
                "key": "Beauty",
                "doc_count": 11,
                "product_count": {
                  "value": 11
                }
              },
              {
                "key": "Furniture",
                "doc_count": 10,
                "product_count": {
                  "value": 10
                }
              },
              {
                "key": "Books",
                "doc_count": 9,
                "product_count": {
                  "value": 9
                }
              },
              {
                "key": "Groceries",
                "doc_count": 9,
                "product_count": {
                  "value": 9
                }
              },
              {
                "key": "Fashion",
                "doc_count": 8,
                "product_count": {
                  "value": 8
                }
              },
              {
                "key": "Toys",
                "doc_count": 7,
                "product_count": {
                  "value": 7
                }
              },
              {
                "key": "Sports",
                "doc_count": 6,
                "product_count": {
                  "value": 6
                }
              }
            ]
          }
        }
      }
      ```

      

13. 计算男性和女性客户的平均订单金额。

    - 代码段

      ```elasticsearch
      POST /ecommerce/_search?
      {
        "size": 0,
        "aggs": {
          "average_order_amount_by_gender": {
            "terms": {
              "field": "customer_gender"
            },
            "aggs": {
              "average_amount": {
                "avg": {
                  "field": "total_amount"
                }
              }
            }
          }
        }
      }
      ```

      

    - 文字解释:

      按性别进行分桶,然后avg聚合total_amount得到平均订单金额

    - 操作成功的代码段

      ```elasticsearch
      {
        "took": 2,
        "timed_out": false,
        "_shards": {
          "total": 1,
          "successful": 1,
          "skipped": 0,
          "failed": 0
        },
        "hits": {
          "total": {
            "value": 100,
            "relation": "eq"
          },
          "max_score": null,
          "hits": []
        },
        "aggregations": {
          "average_order_amount_by_gender": {
            "doc_count_error_upper_bound": 0,
            "sum_other_doc_count": 0,
            "buckets": [
              {
                "key": "male",
                "doc_count": 55,
                "average_amount": {
                  "value": 1798.5043728915127
                }
              },
              {
                "key": "female",
                "doc_count": 45,
                "average_amount": {
                  "value": 1382.397343995836
                }
              }
            ]
          }
        }
      }
      ```

      

14. 找出总销售额最高的前10个日期。

    - 代码段

      ```elasticsearch
      POST /ecommerce/_search?
      {
        "size": 0,
        "aggs": {
          "top_10_dates_by_sales": {
            "terms": {
              "field": "order_date",
              "size": 10, 
              "order": {
                "total_sales": "desc"
              }
            },
            "aggs": {
              "total_sales": {
                "sum": {
                  "field": "total_amount"
                }
              }
            }
          }
        }
      }
      ```

      

    - 文字解释:

      按订单日期进行分桶,然后sum聚合得到总销售额,然后对总销售额进行排序,设置size=10得到总销售额最高的前10个日期。

    - 操作成功的代码段

      ```elasticsearch
      {
        "took": 18,
        "timed_out": false,
        "_shards": {
          "total": 1,
          "successful": 1,
          "skipped": 0,
          "failed": 0
        },
        "hits": {
          "total": {
            "value": 100,
            "relation": "eq"
          },
          "max_score": null,
          "hits": []
        },
        "aggregations": {
          "top_10_dates_by_sales": {
            "doc_count_error_upper_bound": -1,
            "sum_other_doc_count": 86,
            "buckets": [
              {
                "key": 1682726400000,
                "key_as_string": "2023-04-29T00:00:00.000Z",
                "doc_count": 2,
                "total_sales": {
                  "value": 5951.77001953125
                }
              },
              {
                "key": 1677628800000,
                "key_as_string": "2023-03-01T00:00:00.000Z",
                "doc_count": 2,
                "total_sales": {
                  "value": 5457.640075683594
                }
              },
              {
                "key": 1703980800000,
                "key_as_string": "2023-12-31T00:00:00.000Z",
                "doc_count": 2,
                "total_sales": {
                  "value": 5177.3402099609375
                }
              },
              {
                "key": 1694736000000,
                "key_as_string": "2023-09-15T00:00:00.000Z",
                "doc_count": 1,
                "total_sales": {
                  "value": 4886.10009765625
                }
              },
              {
                "key": 1696291200000,
                "key_as_string": "2023-10-03T00:00:00.000Z",
                "doc_count": 1,
                "total_sales": {
                  "value": 4858.9501953125
                }
              },
              {
                "key": 1678665600000,
                "key_as_string": "2023-03-13T00:00:00.000Z",
                "doc_count": 1,
                "total_sales": {
                  "value": 4592.9501953125
                }
              },
              {
                "key": 1691107200000,
                "key_as_string": "2023-08-04T00:00:00.000Z",
                "doc_count": 1,
                "total_sales": {
                  "value": 4131.9501953125
                }
              },
              {
                "key": 1677283200000,
                "key_as_string": "2023-02-25T00:00:00.000Z",
                "doc_count": 2,
                "total_sales": {
                  "value": 3872.6699829101562
                }
              },
              {
                "key": 1681171200000,
                "key_as_string": "2023-04-11T00:00:00.000Z",
                "doc_count": 1,
                "total_sales": {
                  "value": 3790.89990234375
                }
              },
              {
                "key": 1674777600000,
                "key_as_string": "2023-01-27T00:00:00.000Z",
                "doc_count": 1,
                "total_sales": {
                  "value": 3714.25
                }
              }
            ]
          }
        }
      }
      ```

      

15. 计算每个季度销售额最高的产品类别。

    - 代码段

      ```elasticsearch
      POST /ecommerce/_search?
      {
        "size": 0,
        "aggs": {
          "top_category_per_quarter": {
            "date_histogram": {
              "field": "order_date",
              "calendar_interval": "quarter"
            },
            "aggs": {
              "top_category": {
                "terms": {
                  "field": "product_category",
                  "size": 1,
                  "order": {
                    "total_sales": "desc"
                  }
                },
                "aggs": {
                  "total_sales": {
                    "sum": {
                      "field": "total_amount"
                    }
                  }
                }
              }
            }
          }
        }
      }
      ```

      

    - 文字解释:

      先按季度对订单时间进行分桶,然后按商品种类进行分桶,然后sum聚合total_amount得到总销售额,然后在商品种类的桶中设置总销售额降序排序和size=1,得到每个季度销售额最高的产品类别.

    - 操作成功的代码段

      ```elasticsearch
      {
        "took": 3,
        "timed_out": false,
        "_shards": {
          "total": 1,
          "successful": 1,
          "skipped": 0,
          "failed": 0
        },
        "hits": {
          "total": {
            "value": 100,
            "relation": "eq"
          },
          "max_score": null,
          "hits": []
        },
        "aggregations": {
          "top_category_per_quarter": {
            "buckets": [
              {
                "key_as_string": "2023-01-01T00:00:00.000Z",
                "key": 1672531200000,
                "doc_count": 33,
                "top_category": {
                  "doc_count_error_upper_bound": 0,
                  "sum_other_doc_count": 25,
                  "buckets": [
                    {
                      "key": "Jewelry",
                      "doc_count": 8,
                      "total_sales": {
                        "value": 11757.280212402344
                      }
                    }
                  ]
                }
              },
              {
                "key_as_string": "2023-04-01T00:00:00.000Z",
                "key": 1680307200000,
                "doc_count": 28,
                "top_category": {
                  "doc_count_error_upper_bound": 0,
                  "sum_other_doc_count": 24,
                  "buckets": [
                    {
                      "key": "Home Appliances",
                      "doc_count": 4,
                      "total_sales": {
                        "value": 6474.219955444336
                      }
                    }
                  ]
                }
              },
              {
                "key_as_string": "2023-07-01T00:00:00.000Z",
                "key": 1688169600000,
                "doc_count": 18,
                "top_category": {
                  "doc_count_error_upper_bound": 0,
                  "sum_other_doc_count": 15,
                  "buckets": [
                    {
                      "key": "Home Appliances",
                      "doc_count": 3,
                      "total_sales": {
                        "value": 6066.1199951171875
                      }
                    }
                  ]
                }
              },
              {
                "key_as_string": "2023-10-01T00:00:00.000Z",
                "key": 1696118400000,
                "doc_count": 21,
                "top_category": {
                  "doc_count_error_upper_bound": 0,
                  "sum_other_doc_count": 17,
                  "buckets": [
                    {
                      "key": "Beauty",
                      "doc_count": 4,
                      "total_sales": {
                        "value": 9416.89013671875
                      }
                    }
                  ]
                }
              }
            ]
          }
        }
      }
      ```

      

## 三、问题及解决办法

- 无法在只对时间分桶的情况下求得计算每个季度销售额最高的产品类别.
  - 先对时间进行分桶,然后再对产品类别进行分桶,在产品类别的桶中获取销售额最高的产品类别.
