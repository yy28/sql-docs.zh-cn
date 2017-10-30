---
title: "创建命令 (TMSL) |Microsoft 文档"
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
ms.assetid: e3024f89-ebfa-47e4-9893-708f379fd9b8
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9ab10d4af0caa658bff323c2bcd484d37ee354f3
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="create-command-tmsl"></a>创建命令 (TMSL)

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

  创建指定的对象和的所有子代指定的对象。 如果该对象已存在，该命令将引发错误。  
  
## <a name="request"></a>请求  
 根据对象的请求的结构而有所不同。 一个对象，它父级必须包括的所有子级，尽管同级及其父对象的完整对象定义不是必需的。  
  
 [数据库对象 &#40;TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/database-object-tmsl.md)将数据库添加到服务器。  
  
```  
{   
  "create": {   
    "database": {   
      "name": "AdventureworksDW2016",   
      "description": "<description>",   
      "tables": [   
        { },   
        { },   
        { }   
      ],   
      "relationships": [   
        { },   
        { }   
      ]   
    }   
  }   
}  
```  
  
 [数据源对象 &#40;TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/datasources-object-tmsl.md)  
  
```  
{  
  "create": {  
    "parentObject": {  
      "database": "AdventureworksDW2016"  
    },  
    "dataSource": {  
      "name": "SqlServer localhost AdventureworksDW2016",  
      "connectionString": "Provider=SQLNCLI11;Data Source=localhost;Initial Catalog=AdventureworksDW2016;Integrated Security=SSPI;Persist Security Info=false",  
      "impersonationMode": "impersonateAccount",  
      "account": "<account name>",  
      "annotations": [  
        {  
          "name": "ConnectionEditUISource",  
          "value": "SqlServer"  
        }  
      ]  
    }  
  }  
}  
```  
  
 [Tables 对象 &#40;TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/tables-object-tmsl.md)向表中添加列。  
  
```  
{   
  "create": {   
    "parentObject": {   
      "database": "AdventureworksDW2016",   
      "table": "DimSales"  
    },   
    "columns": {   
      "type": ["calculated"  | "data" ]  
      "name": "\<column-name>",   
       "expression":  "<DAX expression>"  
    }   
  }   
}   
```  
  
 [分区对象 &#40;TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/partitions-object-tmsl.md)分区添加到父表对象。  
  
```  
{  
  "create": {  
    "parentObject": {  
      "database": "AdventureWorksTabular1200",  
      "table": "Date"  
    },  
    "partition": {  
      "name": "Date 2",  
      "source": {  
        "query": "SELECT [dbo].[DimDate].* FROM [dbo].[DimDate]",  
        "dataSource": "SqlServer localhost AdventureworksDW2016"  
      }  
    }  
  }  
}  
```  
  
 [角色对象 &#40;TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl.md)按最小方式将角色添加到数据库，但没有成员身份或筛选器。  
  
```  
{  
  "create": {  
    "parentObject": {  
      "database": "AdventureWorksDW2016"  
    },  
    "role": {  
      "name": "DataReader",  
      "modelPermission": "read"  
    }  
  }  
}  
```  
  
 除**数据库**对象，正在创建的对象为指定的子**parentObject**。 父级**数据库**对象始终是**服务器**对象。  
  
 从上下文，则假定服务器。 例如，如果从 Management Studio 或 AMO PowerShell 运行脚本，服务器将指定连接在会话或作为参数。  
  
## <a name="response"></a>响应  
 如果该命令成功，则，返回空结果。 否则，返回 XMLA 异常。  
  
## <a name="examples"></a>示例  
 **示例 1** -添加角色指定成员资格和筛选器。  
  
```  
{   
   "create":{   
      "parentObject":{   
         "database":"AdventureWorksTabular1200"  
      },  
      "role":{  
         "name":"DataReader",  
         "modelPermission":"read",  
         "members":[   
            {  
               "memberName": "account-01",  
               "memberId":"S-1-5-21-1111111111-2222222222-33333333-444444"  
            },  
            {   
               "memberName": "account-02",  
               "memberId":"S-2-5-21-1111111111-2222222222-33333333-444444"  
            }  
         ],  
         "tablePermissions":[   
            {   
               "name":"Date",  
               "filterExpression":"CalendarYear('2011')"  
            }  
         ]  
      }  
   }  
}  
```  
  
## <a name="usage-endpoints"></a>使用情况 （终结点）  
 语句中使用此命令元素[执行方法 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-methods-execute.md)通过以下方式公开的 XMLA 终结点调用：  
  
-   作为 XMLA 窗口中 SQL Server Management Studio (SSMS)  
  
-   为输入文件到**调用 ascmd** PowerShell cmdlet  
  
-   输入到的 SSIS 任务或 SQL Server 代理作业  
  
 你可以从 SSMS 生成用于此命令的现成脚本。  例如，你可以右键单击现有数据库 >**脚本** > **编写数据库脚本为** > **创建到**。  
  
 [ \[MS SSAS T\]: QL Server Analysis Services 表格 （SQL Server 技术协议）](http://go.microsoft.com/fwlink/p/?LinkId=784855)文档包括部分 3.1.5.2.2，用于描述 JSON 表格元数据命令和对象的结构。 目前，该文档介绍命令和在 TMSL 脚本中尚未实现的功能。 请参阅主题 ([表格模型脚本语言 &#40;TMSL &#41;引用](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)) 阐述上支持的功能。  

## <a name="see-also"></a>另请参阅  
 [表格模型脚本语言 (TMSL) 参考](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)  
  
  

