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
author: rothja
ms.author: jroth
ms.openlocfilehash: f1e80dd692b234b88d2b63ed0a43d956152e2e2b
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82761263"
---
# <a name="alternatives-using-sql-statements"></a>替代方法：使用 SQL 语句
ADO 还允许使用命令作为其内置属性的替代方法和用于编辑数据的方法。 根据您的提供程序，本部分中提到的所有操作也可以通过将命令传递到您的数据源来实现。 例如，可以使用 SQL UPDATE 语句来修改数据，而无需使用**字段**的**Value**属性。 SQL INSERT 语句可用于向数据源添加新记录，而不是 ADO 方法**AddNew**。 有关 SQL 或提供程序的数据操作语言的详细信息，请参阅数据源的文档。  
  
 例如，可以将包含 DELETE 语句的 SQL 字符串传递到数据库，如以下代码所示：  
  
```  
'BeginSQLDelete  
strSQL = "DELETE FROM Shippers WHERE ShipperID = " & intId  
objConn1.Execute strSQL, , adCmdText + adExecuteNoRecords  
'EndSQLDelete  
```
