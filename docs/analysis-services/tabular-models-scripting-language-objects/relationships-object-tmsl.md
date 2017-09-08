---
title: "关系对象 (TMSL) |Microsoft 文档"
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 7588565f-ea34-4402-8be9-331188bdb8c2
caps.latest.revision: 7
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 260788cabb01d26215a51f0853b1b8dffc8163d5
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="relationships-object-tmsl"></a>关系对象 (TMSL)

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

  定义源和目标表，可以指定基数和的查询和安全筛选器方向之间的关系。  
  
## <a name="object-definition"></a>对象定义  
 所有对象都有一组通用的属性，包括名称、 类型、 说明、 一个属性集合和批注。 **关系**对象还具有以下属性。  
  
 isActive  
 一个布尔值，该值指示是否将关系标记为活动或非活动。 一个活动关系自动用于跨表筛选。 可以通过使用 USERELATIONSHIP 函数的 DAX 计算显式使用的非活动关系。  
  
 crossFilteringBehavior  
 指示关系如何影响数据的筛选。 请参阅[双向交叉筛选器的 SQL Server 2016 Analysis Services 中的表格模型](../../analysis-services/tabular-models/bi-directional-cross-filters-tabular-models-analysis-services.md)有关详细信息。 以下是有效值：  
  
-   一个 (1)-在关系的"To"端中选择的行将自动筛选关系的"From"端中的表的扫描。  
  
-   BothDirections (2)-关系任意一端的筛选器将自动筛选另一个表。  
  
-   自动 (3)-则引擎将分析关系，并使用启发来选择一个行为。  
  
 joinOnDateBehavior  
 在联接两个日期时间列时，指示是联接日期和时间部分还是仅联接日期部分。  
  
-   DateAndTime (1)-当联接两个日期时间列，联接日期和时间部分。  
  
-   DatePartOnly (2)-当联接两个日期时间列，联接仅日期部分。  
  
 relyOnReferentialIntegrity  
 未使用;留待将来使用。  
  
 securityFilteringBehavior  
 枚举值，该值指示关系如何影响计算行级别安全性表达式时，筛选的数据。 以下是有效值：  
  
-   一个 (1)-在关系的"To"端中选择的行将自动筛选关系的"From"端中的表的扫描。  
  
-   BothDirections (2)-关系任意一端的筛选器将自动筛选另一个表。  
  
## <a name="usage"></a>用法  
 关系对象中使用[Alter 命令 &#40;TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/alter-command-tmsl.md)，[创建命令 &#40;TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/create-command-tmsl.md)， [CreateOrReplace 命令 &#40;TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl.md)，和[删除命令 &#40;TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/delete-command-tmsl.md).  
  
 在创建时，替换或更改关系的对象，将指定对象定义的所有读写的属性。 省略一个读 / 写属性被视为删除操作。  
  
## <a name="full-syntax"></a>完整的语法  
 下面是关系对象的架构表示。  
  
```  
"relationships": {  
          "type": "array",  
          "items": {  
            "anyOf": [  
              {  
                "description": "SingleColumnRelationship object of Tabular Object Model (TOM)",  
                "type": "object",  
                "properties": {  
                  "name": {  
                    "type": "string"  
                  },  
                  "isActive": {  
                    "type": "boolean"  
                  },  
                  "type": {  
                    "enum": [  
                      "singleColumn"  
                    ]  
                  },  
                  "crossFilteringBehavior": {  
                    "enum": [  
                      "oneDirection",  
                      "bothDirections",  
                      "automatic"  
                    ]  
                  },  
                  "joinOnDateBehavior": {  
                    "enum": [  
                      "dateAndTime",  
                      "datePartOnly"  
                    ]  
                  },  
                  "relyOnReferentialIntegrity": {  
                    "type": "boolean"  
                  },  
                  "securityFilteringBehavior": {  
                    "enum": [  
                      "oneDirection",  
                      "bothDirections"  
                    ]  
                  },  
                  "fromCardinality": {  
                    "enum": [  
                      "none",  
                      "one",  
                      "many"  
                    ]  
                  },  
                  "toCardinality": {  
                    "enum": [  
                      "none",  
                      "one",  
                      "many"  
                    ]  
                  },  
                  "fromColumn": {  
                    "type": "string"  
                  },  
                  "fromTable": {  
                    "type": "string"  
                  },  
                  "toColumn": {  
                    "type": "string"  
                  },  
                  "toTable": {  
                    "type": "string"  
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
            ]  
          }  
        }  
```  
  
## <a name="see-also"></a>另请参阅  
 [表格模型脚本语言 (TMSL) 参考](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [创建关系](../../integration-services/data-flow/transformations/create-relationships.md)  
  
  
