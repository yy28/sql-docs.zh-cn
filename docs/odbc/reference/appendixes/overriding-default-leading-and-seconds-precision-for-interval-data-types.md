---
title: "Interval 数据类型的替代前导和秒精度 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data types [ODBC], interval data types
- precision [ODBC], interval data types
- seconds precision [ODBC]
- interval data type [ODBC], precision
- interval leading precision [ODBC]
- interval precision [ODBC]
ms.assetid: 3d65493f-dce7-4d29-9f59-c63a4e47918c
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 70ae232ed09ab7bd04a2474b5798dd4ed581df39
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="overriding-default-leading-and-seconds-precision-for-interval-data-types"></a>间隔数据类型中重写默认前导和秒精度
当 ARD SQL_DESC_TYPE 字段设置为 datetime 或间隔 C 类型，通过调用**SQLBindCol**或**SQLSetDescField**，SQL_DESC_PRECISION 字段 （其中包含间隔 （秒）精度） 设置为以下默认值：  
  
-   6 的时间戳和与第二个组件的所有 interval 数据类型。  
  
-   对于所有其他数据类型为 0。  
  
 对于所有间隔数据类型，SQL_DESC_DATETIME_INTERVAL_PRECISION 描述符字段，其中包含间隔前导字段精度，设置为默认值为 2。  
  
 当在 APD SQL_DESC_TYPE 字段设置为 datetime 或间隔 C 类型，通过调用**SQLBindParameter**或**SQLSetDescField**，SQL_DESC_PRECISION 和 SQL_DESC_DATETIME_INTERVAL_在 APD 精度字段设置为默认值前面给出。 这是 true 为输入参数而不是输入/输出或输出参数。  
  
 调用**SQLSetDescRec**设置以默认值的精度的间隔，但设置的值 （在 SQL_DESC_PRECISION 字段中） 的间隔秒精度其*精度*自变量。  
  
 如果给定的默认值任一以前不是可接受的应用程序，应用程序应通过调用设置 SQL_DESC_PRECISION 或 SQL_DESC_DATETIME_INTERVAL_PRECISION 字段**SQLSetDescField**。  
  
 如果应用程序调用**SQLGetData**为数据返回到日期时间或间隔 C 类型，使用默认时间间隔前导精度和时间间隔秒精度。 如果任一默认值是不可接受，应用程序必须调用**SQLSetDescField**设置其中一个描述符字段，或**SQLSetDescRec**设置 SQL_DESC_PRECISION。 调用**SQLGetData**应有*TargetType*的 SQL_ARD_TYPE 描述符字段中使用的值。  
  
 当**SQLPutData**称为，间隔前导精度和间隔秒精度从描述符记录对应的字段读取到的数据在执行参数或列，这是用于调用 APD 域到**SQLExecute**或**SQLExecDirect**，或调用的 ARD 字段**SQLBulkOperations**或**SQLSetPos**。
