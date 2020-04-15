---
title: 间隔数据类型的超控前导和秒精度 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], interval data types
- precision [ODBC], interval data types
- seconds precision [ODBC]
- interval data type [ODBC], precision
- interval leading precision [ODBC]
- interval precision [ODBC]
ms.assetid: 3d65493f-dce7-4d29-9f59-c63a4e47918c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1e60d5d8fc696ad8e2bd4cfb0c082ff214e066d0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303598"
---
# <a name="overriding-default-leading-and-seconds-precision-for-interval-data-types"></a>重写间隔数据类型的默认前导和秒精度
当 ARD 的SQL_DESC_TYPE字段设置为日期时间或间隔 C 类型时，通过调用**SQLBindCol**或**SQLSetDescField，SQL_DESC_PRECISION**字段（包含间隔秒精度）设置为以下默认值：  
  
-   6 表示时间戳和具有第二个组件的所有间隔数据类型。  
  
-   0 表示所有其他数据类型。  
  
 对于所有间隔数据类型，包含间隔前导字段精度SQL_DESC_DATETIME_INTERVAL_PRECISION描述符字段设置为默认值 2。  
  
 当 APD 中的SQL_DESC_TYPE字段设置为日期时间或间隔 C 类型时，通过调用**SQLBind 参数**或**SQLSetDescField，APD**中的SQL_DESC_PRECISION和SQL_DESC_DATETIME_INTERVAL_PRECISION字段设置为之前给出的默认值。 输入参数也是如此，但输入/输出或输出参数则不然。  
  
 对**SQLSetDescRec**的调用将间隔前导精度设置为默认值，但将间隔秒精度（在SQL_DESC_PRECISION字段中）设置为其*精度*参数的值。  
  
 如果以前给出的任一默认值都不允许应用程序接受，则应用程序应通过调用**SQLSetDescField**来设置SQL_DESC_PRECISION或SQL_DESC_DATETIME_INTERVAL_PRECISION字段。  
  
 如果应用程序调用**SQLGetData**将数据返回到日期时间或间隔 C 类型，则使用默认间隔前导精度和间隔秒精度。 如果任一默认值不可接受，则应用程序必须调用**SQLSetDescField**来设置描述符字段，或者**SQLSetDescRec**以设置SQL_DESC_PRECISION。 对**SQLGetData 的**调用应具有*一个目标类型*SQL_ARD_TYPE，用于使用描述符字段中的值。  
  
 当调用**SQLPutData**时，从对应于执行时的数据参数或列的描述符记录的字段读取间隔前导精度和间隔秒精度，这些字段是调用**SQLExecute**或**SQLExecDirect**的 APD 字段，或调用**SQLBulk 操作**或**SQLSetPos**的 ARD 字段。
