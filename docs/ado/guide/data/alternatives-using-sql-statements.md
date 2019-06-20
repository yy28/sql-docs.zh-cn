---
title: 替代方法：使用 SQL 语句 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ADO]
- editing data [ADO], sql statements
- ADO, SQL statements
ms.assetid: 8b528b23-063d-45ea-8dea-6a90d4060b20
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c85f6ec6ce130d6bcb10db5f137a16f0cd102475
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66701062"
---
# <a name="alternatives-using-sql-statements"></a>替代方法：使用 SQL 语句
ADO 还允许使用作为其内置属性和编辑数据的方法的替代命令。 根据您的提供程序，此部分中提到的所有操作也都可将命令传递给您的数据源。 例如，使用 SQL UPDATE 语句来修改数据而无需使用**值**的属性**字段**。 SQL INSERT 语句可用于将新记录添加到数据源，而不是 ADO 方法**AddNew**。 有关 SQL 或您的提供程序的数据操作语言的详细信息，请参阅您的数据源的文档。  
  
 例如，可以传递包含到数据库，DELETE 语句的 SQL 字符串，如下面的代码中所示：  
  
```  
'BeginSQLDelete  
strSQL = "DELETE FROM Shippers WHERE ShipperID = " & intId  
objConn1.Execute strSQL, , adCmdText + adExecuteNoRecords  
'EndSQLDelete  
```
