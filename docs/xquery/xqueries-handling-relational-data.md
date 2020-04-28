---
title: Xquery 处理关系数据 |Microsoft Docs
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
ms.openlocfilehash: ed4583b30ed1e4538a36079f9f7794704b819cda
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "67946160"
---
# <a name="xqueries-handling-relational-data"></a>处理关系数据的 XQuery
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  使用[Xml 数据类型方法](../t-sql/xml/xml-data-type-methods.md)之一对**xml**类型列或变量指定 XQuery。 其中包括**query （）**、 **value （）**、**存在（）** 或**修改（）**。 对生成 XML 的查询中所标识的 XML 实例执行 XQuery。  
  
 由执行 XQuery 所生成的 XML 可以包括从其他 Transact-SQL 变量或行集列中检索的值。 若要将非 XML 关系数据绑定到得到的 XML 上，则 SQL Server 将提供以下伪函数作为 XQuery 扩展插件：  
  
-   **sql:column()** function  
  
-   **sql:variable()** function  
  
 在**xml**数据类型的**query （）** 方法中指定 xquery 时，可以使用这些 xquery 扩展。 因此， **query （）** 方法可以生成结合 xml 和非**xml**数据类型的数据的 XML。  
  
 当使用**xml**数据类型方法**modify （）**、 **value （）**、 **query （）****和 use （）** 来公开 xml 中的关系值时，您还可以使用这些函数。  
  
 有关详细信息，请参阅[sql： column （）函数（xquery）](../xquery/xquery-extension-functions-sql-column.md)和[sql： variable （）函数（xquery）](../xquery/xquery-extension-functions-sql-variable.md)。  
  
## <a name="see-also"></a>另请参阅  
 [XML Data &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [XQuery 语言参考 &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)   
 [XML 构造 &#40;XQuery&#41;](../xquery/xml-construction-xquery.md)  
  
  
