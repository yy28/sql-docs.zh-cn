---
title: 确定受影响的行数 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- updating data [ODBC], number of rows affected
- number of rows affected by update [ODBC]
- data updates [ODBC], number of rows affected
ms.assetid: 1e56297d-a786-415e-b66d-b42d1b2a8d45
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 156a5fe41d2c9b57a33bbc2bdb4540d1f5b00340
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305888"
---
# <a name="determining-the-number-of-affected-rows"></a>确定受影响的行数
在应用程序更新、删除或插入行后，它可以调用**SQLRowCount**以确定受影响的行数。 **SQLRowCount**通过执行定位的更新或删除语句，或者调用**SQLSetPos**来返回此值，无论行是否通过执行**更新**、删除或插入语句来更新、**删除**或**插入**。  
  
 如果执行一批 SQL 语句，则受影响行的计数可能是批处理中所有语句或批处理中每个语句的单个计数的总计数。 有关详细信息，请参阅[SQL 语句的批处理](../../../odbc/reference/develop-app/batches-of-sql-statements.md)和[多个结果](../../../odbc/reference/develop-app/multiple-results.md)。  
  
 在与语句句柄关联的诊断区域中，SQL_DIAG_ROW_COUNT诊断标头字段中也会返回受影响的行数。 但是，此字段中的数据在相同的语句句柄上的每个函数调用后重置，而**SQLRowCount**返回的值保持不变，直到调用**SQLBulk 操作**、SQLExecute、SQLExecDirect、SQLPrepare 或**SQLPrepare** **SQLSetPos**。 **SQLExecute** **SQLExecDirect**
