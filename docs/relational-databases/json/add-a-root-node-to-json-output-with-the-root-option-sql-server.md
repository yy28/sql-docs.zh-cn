---
title: "使用 ROOT 选项将根节点添加到 JSON 输出中 (SQL Server) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 06/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ROOT (FOR JSON)
ms.assetid: b9afa74a-f59f-483e-a178-42be2e9882c9
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: Human Translation
ms.sourcegitcommit: 439b568fb268cdc6e6a817f36ce38aeaeac11fab
ms.openlocfilehash: e7b316ab5b6f809b348fa882a42a89431590c40b
ms.contentlocale: zh-cn
ms.lasthandoff: 06/23/2017

---
# <a name="add-a-root-node-to-json-output-with-the-root-option-sql-server"></a>使用 ROOT 选项将根节点添加到 JSON 输出中 (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  若要将一个顶层元素添加到 **FOR JSON** 子句的 JSON 输出中，请指定 **ROOT** 选项。  
  
 如果你没有指定 **ROOT** 选项，则 JSON 输出不会包括根元素。  
  
## <a name="examples"></a>示例  
 下表展示了在指定和未指定 **ROOT** 选项的情况下 **FOR JSON** 子句的输出。  
  
 下表中的示例假定可选自变量 *RootName* 为空。 如果你提供了根元素的名称，则此值会替换示例中的值 **root** 。  
  
 未指定 **ROOT** 选项  
  
```json  
{  
   <<json properties>>  
}  
```  
  
```json  
[  
   <<json array elements>>  
]  
```  
  
 指定 **ROOT** 选项  
  
```json  
{   
  "root": {  
   <<json properties>>  
 }  
}  
```  
  
```json  
{   
  "root": [  
   << json array elements >>  
  ]  
}  
```  
  
 下面又通过一个示例展示了在指定 **ROOT** 选项的情况下 **FOR JSON** 子句的输出。 此示例指定了可选自变量 *RootName* 的值。  
  
 **Query**  
  
```sql  
SELECT TOP 5   
       BusinessEntityID As Id,  
       FirstName, LastName,  
       Title As 'Info.Title',  
       MiddleName As 'Info.MiddleName'  
   FROM Person.Person  
   FOR JSON PATH, ROOT('info')
```  
  
 **结果**  
  
```json  
{
    "info": [{
        "Id": 1,
        "FirstName": "Ken",
        "LastName": "Sánchez",
        "Info": {
            "MiddleName": "J"
        }
    }, {
        "Id": 2,
        "FirstName": "Terri",
        "LastName": "Duffy",
        "Info": {
            "MiddleName": "Lee"
        }
    }, {
        "Id": 3,
        "FirstName": "Roberto",
        "LastName": "Tamburello"
    }, {
        "Id": 4,
        "FirstName": "Rob",
        "LastName": "Walters"
    }, {
        "Id": 5,
        "FirstName": "Gail",
        "LastName": "Erickson",
        "Info": {
            "Title": "Ms.",
            "MiddleName": "A"
        }
    }]
}
```  
  
 **结果（未指定根）**  
  
```json  
[{
    "Id": 1,
    "FirstName": "Ken",
    "LastName": "Sánchez",
    "Info": {
        "MiddleName": "J"
    }
}, {
    "Id": 2,
    "FirstName": "Terri",
    "LastName": "Duffy",
    "Info": {
        "MiddleName": "Lee"
    }
}, {
    "Id": 3,
    "FirstName": "Roberto",
    "LastName": "Tamburello"
}, {
    "Id": 4,
    "FirstName": "Rob",
    "LastName": "Walters"
}, {
    "Id": 5,
    "FirstName": "Gail",
    "LastName": "Erickson",
    "Info": {
        "Title": "Ms.",
        "MiddleName": "A"
    }
}]
```  

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>了解有关内置 JSON 支持在 SQL Server 中的详细信息  
对于大量的特定解决方案，使用情况和建议，请参阅[博客文章有关内置 JSON 支持](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)在 SQL Server 和 Azure SQL Database: Microsoft 项目经理 Jovan Popovic 中。
 
## <a name="see-also"></a>另请参阅  
 [FOR 子句 (Transact-SQL)](../../t-sql/queries/select-for-clause-transact-sql.md)  
  
  

