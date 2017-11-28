---
title: "分区对象 (TMSL) |Microsoft 文档"
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: df1da0d2-d824-42ba-b9dc-47fbd8edc10f
caps.latest.revision: "10"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6ea3c1f7486caa923bcf5cfc07d83a65e76578e5
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="partitions-object-tmsl"></a>分区对象 (TMSL)

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

  定义了分区或逻辑分段，表行集。 分区包含，用于导入数据，在建模环境中，或作为传递通过 DirectQuery 的查询执行的完整数据查询的示例数据的 SQL 查询。  
  
 在分区上的属性确定如何将数据源的表。  在对象层次结构，一个分区的父对象是一个表对象。  
  
## <a name="object-definition"></a>对象定义  
 所有对象都有一组通用的属性，包括名称、 类型、 说明、 一个属性集合和批注。 **分区**对象还具有以下属性。  
  
 类型  
 分区的类型。 有效的值是数值，并包括以下各项：  
  
-   查询 (1) – 此分区中的数据通过对执行查询**数据源**。 **数据源**必须 model.bim 文件中定义的数据源。  
  
-   计算 (2)-通过执行计算的表达式填充此分区中的数据。  
  
-   无 (3) – 此分区中的数据是通过将数据行集推送到服务器，作为刷新操作的一部分进行填充。  
  
 mode  
 定义的分区的查询模式。 有效值为**导入**， **DirectQuery**，或**默认**（继承）。 此值是必需的。  
  
|||  
|-|-|  
|**导入**|指示请求针对存储导入的数据的内存中分析引擎发出的查询。|  
|**DirectQuery**|传递给外部关系数据库的查询执行。 DirectQuery 模式下使用分区提供模型设计过程中使用的示例数据。 部署在生产服务器上，你应切换回完整数据视图。 回想一下 DirectQuery 模式要求每个表，一个分区，且每个模型的一个数据源。|  
|**默认值**|如果你想要切换较高对象树中，在模型或数据库级别的模式，则将此设置。 当你选择默认值时，查询模式下将导入或 DirectQuery。|  
  
 源 (source)  
 标识要查询的数据的位置。 有效值为**查询，计算**，或**无**。 此值是必需的。  
  
|||  
|-|-|  
|**无**|用于导入模式，其中加载数据，并存储在内存中。|  
|**查询**|对于 DirectQuery 模式下，这是执行针对模型的中指定的关系数据库的 SQL 查询**数据源**。 请参阅[数据源对象 &#40;TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/datasources-object-tmsl.md).|  
|**计算**|计算的表源自创建表时指定的表达式。 该表达式被视为创建计算表的分区的源。|  
  
 dataview  
 对于 DirectQuery 分区，其他 dataView 属性进一步指定查询以检索数据是示例数据还是完整数据集。 有效值为**完整**，**示例**，或**默认**（继承）。 如上所述，仅在数据建模和测试中使用示例。 请参阅[将示例数据添加到设计模式中的 DirectQuery 模型](../../analysis-services/tabular-models/add-sample-data-to-a-directquery-model-in-design-mode.md)有关详细信息。  
  
## <a name="usage"></a>用法  
 在使用分区对象[Alter 命令 &#40;TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/alter-command-tmsl.md)，[创建命令 &#40;TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/create-command-tmsl.md)， [CreateOrReplace 命令 &#40;TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl.md)，[删除命令 &#40;TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/delete-command-tmsl.md)，[刷新命令 &#40;TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/refresh-command-tmsl.md)，和[撰写 MergePartitions 命令 &#40;TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/mergepartitions-command-tmsl.md).  
  
 在创建时，替换或更改分区的对象，将指定对象定义的所有读写的属性。 省略一个读 / 写属性被视为删除操作。 读写属性包括名称、 说明、 模式和源。  
  
## <a name="examples"></a>示例  
 **示例 1** -表 （不事实数据表） 的简单的分区结构。  
  
```  
"partitions": [  
          {  
            "name": "Customer",  
            "source": {  
              "query": "SELECT [dbo].[Customer].* FROM [dbo].[Customer]",  
              "dataSource": "SqlServer localhost FoodmartDB"  
            }  
]  
```  
  
 **示例 2** -已分区的事实数据通常基于从同一个表中创建数据的不重叠分区的 WHERE 子句。  
  
```  
"partitions": [  
          {  
            "name": "sales_fact_2015",  
            "source": {  
              "query": "SELECT [dbo].[sales_fact_2015].* FROM [dbo].[sales_fact_2015] WHERE [dbo].[sales_fact_2015].[Quarter]=4",                                                                                          
              "dataSource": "SqlServer localhost FoodmartDB"  
            },  
          }  
        ]  
```  
  
 **示例 3** -基于 DAX 表达式的计算的表。  
  
```  
"partitions": [  
          {  
            "name": "CalcTable1",  
            "source": {  
              "type": "calculated",  
              "expression": "'Product Class'"  
            },  
            }  
]  
```  
  
## <a name="full-syntax"></a>完整的语法  
 下面是将 partition 对象的架构表示。  
  
```  
"partitions": {  
                "type": "array",  
                "items": {  
                  "description": "Partition object of Tabular Object Model (TOM)",  
                  "type": "object",  
                  "properties": {  
                    "name": {  
                      "type": "string"  
                    },  
                    "description": {  
                      "anyOf": [  
                        {  
                          "type": "string"  
                        },  
                        {  
                          "type": "array",  
                          "items": {  
                            "type": "string"  
                          }  
                        }  
                      ]  
                    },  
                    "mode": {  
                      "enum": [  
                        "import",  
                        "directQuery",  
                        "default"  
                      ]  
                    },  
                    "dataView": {  
                      "enum": [  
                        "full",  
                        "sample",  
                        "default"  
                      ]  
                    },  
                    "source": {  
                      "anyOf": [  
                        {  
                          "description": "QueryPartitionSource object of Tabular Object Model (TOM)",  
                          "type": "object",  
                          "properties": {  
                            "type": {  
                              "enum": [  
                                "query",  
                                "calculated",  
                                "none"  
                              ]  
                            },  
                            "query": {  
                              "anyOf": [  
                                {  
                                  "type": "string"  
                                },  
                                {  
                                  "type": "array",  
                                  "items": {  
                                    "type": "string"  
                                  }  
                                }  
                              ]  
                            },  
                            "dataSource": {  
                              "type": "string"  
                            }  
                          },  
                          "additionalProperties": false  
                        },  
                        {  
                          "description": "CalculatedPartitionSource object of Tabular Object Model (TOM)",  
                          "type": "object",  
                          "properties": {  
                            "type": {  
                              "enum": [  
                                "query",  
                                "calculated",  
                                "none"  
                              ]  
                            },  
                            "expression": {  
                              "anyOf": [  
                                {  
                                  "type": "string"  
                                },  
                                {  
                                  "type": "array",  
                                  "items": {  
                                    "type": "string"  
                                  }  
                                }  
                              ]  
                            }  
                          },  
                          "additionalProperties": false  
                        }  
                      ]  
                    },  
                    "annotations": {  
                      "type": "array",  
                      "items": {  
                        "description": "Annotation object of Tabular Object Model (TOM)",  
                        "type": "object",  
                        "properties": {  
                          "name": {  
                            "type": "string"  
                          },  
                          "value": {  
                            "anyOf": [  
                              {  
                                "type": "string"  
                              },  
                              {  
                                "type": "array",  
                                "items": {  
                                  "type": "string"  
                                }  
                              }  
                            ]  
                          }  
                        },  
                        "additionalProperties": false  
                      }  
                    }  
                  },  
                  "additionalProperties": false  
                }  
              },  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [表格模型脚本语言 (TMSL) 参考](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)  
  
  
