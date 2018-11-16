---
title: 处理关系数据的 XQueries |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- relational data [XQuery]
- XQuery, relational data
ms.assetid: 9812b71a-52ec-48a0-92f3-016a93660229
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 9aa8b150a26e64d4a61efe80ab635110e540af33
ms.sourcegitcommit: 0f7cf9b7ab23df15624d27c129ab3a539e8b6457
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2018
ms.locfileid: "51291014"
---
# <a name="xqueries-handling-relational-data"></a>处理关系数据的 XQuery
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  指定 XQuery **xml**类型列或变量使用之一[XML 数据类型方法](../t-sql/xml/xml-data-type-methods.md)。 其中包括**query （)**， **value （)**， **exist （)**，或者**modify （)**。 对生成 XML 的查询中所标识的 XML 实例执行 XQuery。  
  
 由执行 XQuery 所生成的 XML 可以包括从其他 Transact-SQL 变量或行集列中检索的值。 若要将非 XML 关系数据绑定到得到的 XML 上，则 SQL Server 将提供以下伪函数作为 XQuery 扩展插件：  
  
-   **sql:column()** function  
  
-   **sql:variable()** function  
  
 指定在 XQuery 时，可以使用这些 XQuery 扩展插件**query （)** 方法**xml**数据类型。 因此， **query （)** 方法可以生成将数据从 XML 和非结合起来的 XML-**xml**数据类型。  
  
 当你使用时，还可以使用这些函数**xml**数据类型方法**modify （)**， **value （)**， **query （)**，和**exist （)** 来显示 XML 内的关系值。  
  
 有关详细信息，请参阅[sql: column 函数 (XQuery)](../xquery/xquery-extension-functions-sql-column.md)并[sql:variable() 函数 (XQuery)](../xquery/xquery-extension-functions-sql-variable.md)。  
  
## <a name="see-also"></a>请参阅  
 [XML 数据 (SQL Server)](../relational-databases/xml/xml-data-sql-server.md)   
 [XQuery 语言参考 (SQL Server)](../xquery/xquery-language-reference-sql-server.md)   
 [XML 构造&#40;XQuery&#41;](../xquery/xml-construction-xquery.md)  
  
  
