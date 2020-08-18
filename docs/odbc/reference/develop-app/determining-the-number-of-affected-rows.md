---
description: 确定受影响的行数
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 14114700c4d79f83f0388509056dd0b49bb21a8d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483070"
---
# <a name="determining-the-number-of-affected-rows"></a>确定受影响的行数
在应用程序更新、删除或插入行后，它可以调用 **SQLRowCount** 来确定受影响的行数。 **SQLRowCount** 返回此值，无论是通过执行 " **更新**"、" **删除**" 或 " **插入** " 语句、执行定位的 Update 或 delete 语句，还是通过调用 **SQLSetPos**来更新、删除或插入行。  
  
 如果执行了一批 SQL 语句，受影响的行的计数可能为批处理中的所有语句的总计数或批处理中每个语句的单个计数。 有关详细信息，请参阅 [SQL 语句的批处理](../../../odbc/reference/develop-app/batches-of-sql-statements.md) 和 [多个结果](../../../odbc/reference/develop-app/multiple-results.md)。  
  
 受影响的行数也将在与语句句柄关联的诊断区域的 "SQL_DIAG_ROW_COUNT 诊断标头" 字段中返回。 但是，在对同一语句句柄调用每个函数后，此字段中的数据将重置，而 **SQLRowCount** 返回的值将保持不变，直到调用 **SQLBulkOperations**、 **SQLExecute**、 **SQLExecDirect**、 **SQLPrepare**或 **SQLSetPos**。
