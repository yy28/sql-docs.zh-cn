---
title: Alter 命令 (TMSL) |Microsoft 文档
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tmsl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6dc7ba58ce3e5db228046324c17c91719db35d0b
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="alter-command-tmsl"></a>Alter 命令 (TMSL)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  更改现有对象，但不是其子项，在表格模式下的 Analysis Services 实例上。  如果不存在该对象，该命令将引发错误。  
  
 使用**Alter**命令目标的更新，如同在表上设置一个属性，而无需指定的所有列以及。 此命令是类似于**CreateOrReplace**，但没有无需再次提供完整的对象定义的要求。  
  
 为具有读写属性，如果指定一个读 / 写属性的对象，你将需要指定所有这些，使用新报表或现有的值。 可以使用 AMO PowerShell 若要获取属性列表。 
  
## <a name="request"></a>请求  
 **Alter**不具有任何特性。 输入包括要将更改后, 跟已修改的对象定义的对象。  
  
 下面的示例演示用于更改分区对象的属性的语法。 对象路径建立的分区对象是要更改通过的父对象的名称-值对。 第二个输入是一个指定新的属性值的分区对象。  
  
```  
{   
  "alter": {   
    "object": {   
      "database": "\<database-name>",   
      "table": "\<table-name>",   
      "partition": "\<partition-name>"   
    },   
    "partition": {   
      "name": "\<new-partition-name>",   
       . . .  << other properties   
    }   
  }   
}   
```  
  
 根据对象的请求的结构而有所不同。 **Alter**可与任何以下对象：  
  
 [数据库对象&#40;TMSL&#41; ](../../analysis-services/tabular-models-scripting-language-objects/database-object-tmsl.md)重命名数据库。  
  
```  
"alter": {   
    "object": {   
      "database": "\<database-name>"  
    },   
    "database": {   
      "name": "\<new-database-name>",   
    }   
  }   
```  
  
 [数据源对象&#40;TMSL&#41; ](../../analysis-services/tabular-models-scripting-language-objects/datasources-object-tmsl.md)重命名的连接，这是数据库的子对象。  
  
```  
{   
   "alter":{   
      "object":{   
         "database":"AdventureWorksTabular1200",  
         "dataSource":"SqlServer localhost AdventureworksDW2016"  
      },  
      "dataSource":{   
         "name":"A new connection name"  
      }  
   }  
}  
```  
  
 [Tables 对象&#40;TMSL&#41; ](../../analysis-services/tabular-models-scripting-language-objects/tables-object-tmsl.md)请参阅**示例 1**下面。  
  
 [分区对象&#40;TMSL&#41; ](../../analysis-services/tabular-models-scripting-language-objects/partitions-object-tmsl.md)请参阅**示例 2**下面。  
  
 [角色对象&#40;TMSL&#41; ](../../analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl.md)更改角色对象的属性。  
  
```  
{   
   "alter":{   
      "object":{   
         "database":"AdventureWorksTabular1200",  
         "role":"DataReader"  
      },  
      "role":{   
         "name":"New Name"  
      }  
   }  
}  
```  
  
## <a name="response"></a>响应  
 如果该命令成功，则，返回空结果。 否则，返回 XMLA 异常。  
  
## <a name="examples"></a>示例  
 下面的示例演示可以在 Management Studio 中的 XMLA 窗口中运行，也可以使用作为输入中的脚本[Invoke ASCmd cmdlet](../../analysis-services/powershell/invoke-ascmd-cmdlet.md) AMO PowerShell 中。  
  
 **示例 1** -此脚本更改表的名称属性。  
  
```  
{   
  "alter": {   
    "object": {   
      "database": "AdventureWorksDW2016",   
      "table": "DimDate"  
    },   
    "table": {   
      "name": "DimDate2"  
    }   
  }   
}  
```  
  
 假定本地命名实例 （实例名为"表格"） 和具有 alter 脚本，此命令的 JSON 文件的表名称从变为 DimDate DimDate2:  
  
 `invoke-ascmd -inputfile '\\my-computer\my-shared-folder\altertablename.json' -server 'localhost\Tabular'`  
  
 **示例 2** -此脚本将重命名一个分区，例如在当前年份时前一年的年份结束。 请确保指定的所有属性。 如果你离开**源**未指定，它可能会中断所有现有的分区定义。  
  
 除非您要创建的更换，或更改数据的源对象本身，任何在脚本 （如下面的分区脚本） 中引用的数据源必须是现有**数据源**模型中的对象。 如果你需要更改数据源，应将其作为一个单独的步骤。  
  
```  
{   
  "alter": {   
    "object": {   
      "database": "InternetSales",   
      "table": "DimDate",  
      "partition": "CurrentYear"  
    },   
    "partition": {   
      "name": "Year2009",  
       "source": {  
             "query":  "SELECT [dbo].[DimDate].* FROM [dbo].[DimDate] WHERE [dbo].[DimDate].CalendarYear = 2009",  
              "dataSource": "SqlServer localhost AdventureworksDW2016"  
        }  
    }   
  }   
}  
```  
  
## <a name="usage-endpoints"></a>使用情况 （终结点）  
 语句中使用此命令元素[执行方法&#40;XMLA&#41; ](../../analysis-services/xmla/xml-elements-methods-execute.md)通过以下方式公开的 XMLA 终结点调用：  
  
-   作为 XMLA 窗口中 SQL Server Management Studio (SSMS)  
  
-   为输入文件到**调用 ascmd** PowerShell cmdlet  
  
-   输入到的 SSIS 任务或 SQL Server 代理作业  
  
 无法从 SSMS 生成用于此命令的现成脚本。 相反，你可以从一个示例开始或编写自己。  
  
 [ \[MS SSAS T\]: QL Server Analysis Services 表格 （SQL Server 技术协议）](http://go.microsoft.com/fwlink/p/?LinkId=784855)文档包括部分 3.1.5.2.2，用于描述 JSON 表格元数据命令和对象的结构。 目前，该文档介绍命令和在 TMSL 脚本中尚未实现的功能。 请参阅主题 ([表格模型脚本语言&#40;TMSL&#41;引用](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)) 阐述上支持的功能。  

## <a name="see-also"></a>另请参阅  
 [表格模型脚本语言 (TMSL) 参考](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)  
  
  
