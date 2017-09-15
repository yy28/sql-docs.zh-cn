---
title: "替代方法： 使用 SQL 语句 |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL statements [ADO]
- editing data [ADO], sql statements
- ADO, SQL statements
ms.assetid: 8b528b23-063d-45ea-8dea-6a90d4060b20
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6c1d1da58832a1fbbc133c17f58d940d46f5c6e1
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="alternatives-using-sql-statements"></a>替代方法： 使用 SQL 语句
ADO 还允许使用命令作为其内置属性和编辑数据的方法的替代。 根据你的提供程序，此部分中提到的所有操作也都可通过将命令传递给您的数据源。 例如，SQL UPDATE 语句可以用于修改数据而不使用**值**属性**字段**。 SQL INSERT 语句可以用于将新记录添加到数据源，而不是 ADO 方法**AddNew**。 有关 SQL 或你的提供商的数据操作语言的详细信息，请参阅您的数据源的文档。  
  
 例如，可以传递包含到数据库，DELETE 语句的 SQL 字符串，如下面的代码中所示：  
  
```  
'BeginSQLDelete  
strSQL = "DELETE FROM Shippers WHERE ShipperID = " & intId  
objConn1.Execute strSQL, , adCmdText + adExecuteNoRecords  
'EndSQLDelete  
```
