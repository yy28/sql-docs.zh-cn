---
title: 确定受影响的行数 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a6a1bebf7d5cfb85e49fb0e382dacc4f4464054e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039980"
---
# <a name="determining-the-number-of-affected-rows"></a>确定受影响的行数
应用程序更新、 删除或插入行后，它可以调用**SQLRowCount**来确定受影响行数。 **SQLRowCount**返回此值，指示是否已更新、 删除，或由执行插入的行**更新**，**删除**，或**插入**语句，通过执行定位更新或 delete 语句，或通过调用**SQLSetPos**。  
  
 如果执行一批 SQL 语句，则受影响的行计数可能总数的批处理中的所有语句或批处理中每个语句的单独计数。 有关详细信息，请参阅[SQL 语句的批处理](../../../odbc/reference/develop-app/batches-of-sql-statements.md)并[多个结果](../../../odbc/reference/develop-app/multiple-results.md)。  
  
 在诊断与语句句柄关联的区域中的 SQL_DIAG_ROW_COUNT 诊断标头字段中也返回受影响的行数。 但是，此字段中的数据后重置在同一语句句柄上的每个函数调用而返回的值**SQLRowCount**的调用之前将保持不变**SQLBulkOperations**， **SQLExecute**， **SQLExecDirect**， **SQLPrepare**，或者**SQLSetPos**。
