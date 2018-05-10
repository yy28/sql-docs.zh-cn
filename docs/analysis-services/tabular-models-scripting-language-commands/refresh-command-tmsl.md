---
title: 刷新命令 (TMSL) |Microsoft 文档
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1cb0af1e4d5f3a89e981dc8ec12df68ed5f93110
ms.sourcegitcommit: 1aedef909f91dc88dc741748f36eabce3a04b2b1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2018
---
# <a name="refresh-command-tmsl"></a>刷新命令 (TMSL)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  处理当前数据库中的对象。   
**刷新**始终运行并行，除非限制其与[序列命令&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/sequence-command-tmsl.md)。  
  
 您可以在数据刷新操作期间覆盖某些对象的某些属性：  
  
-   更改**QueryDefinition**属性**分区**要导入使用即时上筛选器表达式的数据对象。  
  
-   提供作为的一部分的数据源凭据**刷新**命令，在**ConnectionString**属性**数据源**对象。 而非存储，无法提供和持续时间内执行操作时，暂时使用凭据时视为更加安全，这种方法。  
  
 请参阅本主题举例说明了这些属性重写中的示例。  
  
> [!NOTE]  
>  与不同的是多维的处理，没有任何特殊的处理的处理进行表格处理的错误。  

  
## <a name="request"></a>请求  
 **刷新**将使用类型参数和对象定义。  
  
```  
    {  
        "refresh": {  
            "description": "Parameters of Refresh command of Analysis Services JSON API",  
            "properties": {  
            "type": {  
                "enum": [  
                "full",  
                "clearValues",  
                "calculate",  
                "dataOnly",  
                "automatic",  
                "add",  
                "defragment"  
                ]  
            },  
            "objects": {  
. . .   
```  
  
 **类型**参数设置作用域上处理操作。  
  
||||  
|-|-|-|  
|**刷新类型**|**适用于**|**Description**|  
|完整|数据库，<br />表，<br />分区|对于指定分区、表或数据库中的所有分区，刷新数据并重新计算所有依赖项。 对于计算分区，重新计算此分区及其所有依赖项。|  
|clearValues|数据库，<br />表，<br />分区|清除此对象及其所有依赖项内的值。|  
|计算|数据库，<br />表，<br />分区|仅当需要时，重新计算此对象及其所有依赖项。 此值不会强制重新计算，可变公式除外。|  
|dataOnly|数据库，<br />表，<br />分区|刷新此对象内的数据并清除所有依赖项。|  
|automatic|数据库，<br />表，<br />分区|如果对象需要刷新并重新计算，则刷新并重新计算对象及其所有依赖项。 如果分区处于“就绪”以外的状态，则应用。|  
|add|分区|将数据追加到此分区并重新计算所有依赖项。 此命令仅对常规分区有效，不用于计算分区。|  
|碎片整理|数据库，<br />表|在指定的表中对数据进行碎片整理。 在表中添加或删除数据时，每一列的字典都会受到污染，会出现实际列值中不再存在的值。 碎片整理选项将清除不再使用的字典中的值。|  
  
 你可以刷新下列对象：  
  
 [数据库对象&#40;TMSL&#41; ](../../analysis-services/tabular-models-scripting-language-objects/database-object-tmsl.md)处理数据库。  
  
```  
{  
  "refresh": {  
    "type": "automatic",  
    "objects": [  
      {  
        "database": "AdventureWorksTabular1200"  
      }  
    ]  
  }  
}  
```  
  
 [Tables 对象&#40;TMSL&#41; ](../../analysis-services/tabular-models-scripting-language-objects/tables-object-tmsl.md)处理单个表。  
  
```  
{  
  "refresh": {  
    "type": "automatic",  
    "objects": [  
      {  
        "database": "AdventureWorksTabular1200",  
        "table": "Date"  
      }  
    ]  
  }  
}  
```  
  
 [分区对象&#40;TMSL&#41; ](../../analysis-services/tabular-models-scripting-language-objects/partitions-object-tmsl.md)处理表中的单个分区。  
  
```  
{  
  "refresh": {  
    "type": "automatic",  
    "objects": [  
      {  
        "database": "AdventureWorksTabular1200",  
        "table": "FactSalesQuota",  
        "partition": "FactSalesQuota"  
      },  
      {  
        "database": "AdventureWorksTabular1200",  
        "table": "FactSalesQuota",  
        "partition": "FactSalesQuota - 2011"  
      }  
    ]  
  }  
}  
```  
  
## <a name="response"></a>响应  
 如果该命令成功，则，返回空结果。 否则，返回 XMLA 异常。  
  
## <a name="examples"></a>示例  
 重写二者， **ConnectionString**和查询的分区的定义。  
  
```  
{   
    "refresh": {   
        "type": "data",   
        "objects": [   
            {   
                "database": "tmtestdb",   
                "table": "sales"   
            },   
            {   
                "database": "tmtestdb",   
                "table": "customer"   
            }   
        ],   
        "overrides": [   
            {   
                "dataSources": [ // Bindings for Data Sources   
                    {   
                        "object": {   
                            "database": "tmtestdb",   
                            "dataSource": "contoso"   
                        },   
                        "dataSource": {   
                        "connectionString": "Provider=SQLNCLI11;Data Source=localhost;Initial Catalog=contoso;Integrated Security=SSPI;Persist Security Info=false"   
"   
                        }   
                    }   
                ],   
                "partitions": [ // Bindings for Partitions   
                    {   
                        "object": {   
                            "database": "tmtestdb",   
                            "table": "sales",   
                            "partition": "2015"   
                        },   
                        "partition": {   
                            "source": {   
                                "query": [  
                                     "SELECT sales.salesamount, customer.customername FROM sales",  
                                     "JOIN customer on custKey = sales.custkey",  
                                     "JOIN date on date.DateKey = customer.OrderDate",  
                                     "WHERE date.CalendarYear='2015'"  
                                  ],  
                            }   
                        }   
                    }   
                ]   
            }   
        ]   
    }   
}   
```  
  
 特定范围的重写通过类型参数设置为**dataOnly**刷新，元数据保持不变。  
  
```  
{   
        "refresh" : {   
            "type" : "dataOnly",   
            "objects" : [   
                {   
                    "database" : "TMTestDB",   
                    "table" : "Customer"   
                },   
                {   
                    "database" : "TMTestDB",   
                    "table" : "Sales"   
                }   
            ],   
            "overrides" : [{   
                "scope" : {   
                    "database" : "TMTestDB",   
                    "table" : "Sales"   
                },   
                "dataSources" : [{   
                    "originalObject" : {   
                        "dataSource" : "SqlServer sqlcldb2 AS_foodmart_2000"   
                    },   
                    "connectionString" : "Provider=SQLNCLI11;Data Source=sqlcldb2;Initial Catalog=AS_foodmart_2000;Integrated Security=SSPI;Persist Security Info=false"   
                }]   
            }]   
        }   
    }   
```  
  
## <a name="usage-endpoints"></a>使用情况 （终结点）  
 语句中使用此命令元素[执行方法&#40;XMLA&#41; ](../../analysis-services/xmla/xml-elements-methods-execute.md)通过以下方式公开的 XMLA 终结点调用：  
  
-   作为 XMLA 窗口中 SQL Server Management Studio (SSMS)  
  
-   为输入文件到**调用 ascmd** PowerShell cmdlet  
  
-   输入到的 SSIS 任务或 SQL Server 代理作业  
  
 你可以从 SSMS 生成用于此命令的现成脚本。  例如，你可以单击**脚本**处理对话框中。  
  
 [ \[MS SSAS T\]: QL Server Analysis Services 表格 （SQL Server 技术协议）](http://go.microsoft.com/fwlink/p/?LinkId=784855)文档包括部分 3.1.5.2.2，用于描述 JSON 表格元数据命令和对象的结构。 目前，该文档介绍命令和在 TMSL 脚本中尚未实现的功能。 请参阅主题 ([表格模型脚本语言&#40;TMSL&#41;引用](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)) 阐述上支持的功能。  
  
## <a name="see-also"></a>另请参阅  
 [表格模型脚本语言 (TMSL) 参考](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [处理选项和设置&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md)  
  
  
