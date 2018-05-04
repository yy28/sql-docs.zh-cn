---
title: 确定受影响的行数 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- updating data [ODBC], number of rows affected
- number of rows affected by update [ODBC]
- data updates [ODBC], number of rows affected
ms.assetid: 1e56297d-a786-415e-b66d-b42d1b2a8d45
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2b826520d76b36eefab78de7e1d9db34ed202fb6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="determining-the-number-of-affected-rows"></a>确定受影响的行数
应用程序更新、 删除或插入行后，它可以调用**SQLRowCount**来确定受影响的行数。 **SQLRowCount**返回此值，指示是否已更新、 删除，或者通过执行插入行**更新**，**删除**，或**插入**语句，通过执行定位更新或删除语句，或通过调用**SQLSetPos**。  
  
 如果执行一批 SQL 语句，则受影响的行的计数可能是批处理中的所有语句的总数或个批处理中每个语句的计数。 有关详细信息，请参阅[SQL 语句的批处理](../../../odbc/reference/develop-app/batches-of-sql-statements.md)和[多个结果](../../../odbc/reference/develop-app/multiple-results.md)。  
  
 在诊断与语句句柄关联的区域中的 SQL_DIAG_ROW_COUNT 诊断标头字段中还返回受影响的行数。 但是，此字段中的数据重置后每个函数调用上相同的语句句柄，而返回的值**SQLRowCount**之前调用中保持不变**SQLBulkOperations**， **SQLExecute**， **SQLExecDirect**， **SQLPrepare**，或**SQLSetPos**。
