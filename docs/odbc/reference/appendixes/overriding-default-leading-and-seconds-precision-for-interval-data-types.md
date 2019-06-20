---
title: 间隔数据类型的替代前导和秒精度 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fdab9e6e60311aca4ce0ae35f92e38c45fdf3702
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63018472"
---
# <a name="overriding-default-leading-and-seconds-precision-for-interval-data-types"></a>重写间隔数据类型的默认前导和秒精度
如果 ARD 的 SQL_DESC_TYPE 字段设置为 datetime 或间隔 C 类型，通过调用**SQLBindCol**或**SQLSetDescField**，SQL_DESC_PRECISION 字段 （其中包含间隔 （秒）精度） 设置以下默认值为：  
  
-   6 为时间戳以及与第二个组件的所有间隔数据类型。  
  
-   对于所有其他数据类型为 0。  
  
 对于所有的时间间隔数据类型，SQL_DESC_DATETIME_INTERVAL_PRECISION 描述符字段，其中包含时间间隔前导字段精度，设置为默认值为 2。  
  
 当 APD 中的 SQL_DESC_TYPE 字段设置为 datetime 或间隔 C 类型，通过调用**SQLBindParameter**或**SQLSetDescField**，SQL_DESC_PRECISION 和 SQL_DESC_DATETIME_INTERVAL_APD 中的精度字段设置为前面给出的默认值。 这是 true 为输入参数而不是输入/输出或输出参数。  
  
 调用**SQLSetDescRec**将设置到默认起始精度的时间间隔，但设置的值 （在 SQL_DESC_PRECISION 字段中） 的间隔秒精度及其*精度*参数。  
  
 如果任何一个给定的默认值以前是不可接受的应用程序，该应用程序应通过调用设置的 SQL_DESC_PRECISION 或 SQL_DESC_DATETIME_INTERVAL_PRECISION 字段**SQLSetDescField**。  
  
 如果应用程序调用**SQLGetData**为将数据返回到 datetime 或间隔 C 类型，使用默认时间间隔前导精度和间隔的秒精度。 如果默认值是不可接受，应用程序必须调用**SQLSetDescField**若要设置其中一个描述符字段，或**SQLSetDescRec**设置 SQL_DESC_PRECISION。 在调用**SQLGetData**应有*TargetType*的 SQL_ARD_TYPE 若要使用中的描述符字段的值。  
  
 当**SQLPutData**调用时，间隔起始精度和时间间隔 （秒） 精度从相对应的描述符记录字段读取到执行时数据参数或列，这是用于调用 APD 域向**SQLExecute**或**SQLExecDirect**，或对的调用 ARD 字段**SQLBulkOperations**或者**SQLSetPos**。
