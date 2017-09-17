---
title: "确定受影响的行数 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- updating data [ODBC], number of rows affected
- number of rows affected by update [ODBC]
- data updates [ODBC], number of rows affected
ms.assetid: 1e56297d-a786-415e-b66d-b42d1b2a8d45
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b2f030be011864be17c8539d8ab94f6980f0f791
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="determining-the-number-of-affected-rows"></a>确定受影响的行数
应用程序更新、 删除或插入行后，它可以调用**SQLRowCount**来确定受影响的行数。 **SQLRowCount**返回此值，指示是否已更新、 删除，或者通过执行插入行**更新**，**删除**，或**插入**语句，通过执行的定位的更新或 delete 语句，或通过调用**SQLSetPos**。  
  
 如果执行一批 SQL 语句，则受影响的行的计数可能是批处理中的所有语句的总数或个批处理中每个语句的计数。 有关详细信息，请参阅[SQL 语句的批处理](../../../odbc/reference/develop-app/batches-of-sql-statements.md)和[多个结果](../../../odbc/reference/develop-app/multiple-results.md)。  
  
 在诊断与语句句柄关联的区域中的 SQL_DIAG_ROW_COUNT 诊断标头字段中还返回受影响的行数。 但是，此字段中的数据重置后每个函数调用上相同的语句句柄，而返回的值**SQLRowCount**之前调用中保持不变**SQLBulkOperations**， **SQLExecute**， **SQLExecDirect**， **SQLPrepare**，或**SQLSetPos**。
