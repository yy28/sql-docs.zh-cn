---
title: 数字数据类型的压倒默认精度和缩放 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- numeric data type [ODBC], precision and scale
- precision [ODBC], numeric data types
- data types [ODBC], numeric data types
- numeric data type [ODBC]
- numeric literals [ODBC]
ms.assetid: 84292334-0e33-4a1b-84de-8c018dd787f3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 365c5f69d21dd3a4ad8e89805d81f1b3b0c9dcba
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303588"
---
# <a name="overriding-default-precision-and-scale-for-numeric-data-types"></a>重写数字数据类型的默认精度和小数位数
当 ARD 中的SQL_DESC_TYPE字段设置为SQL_C_NUMERIC，通过调用**SQLBindCol**或**SQLSetDescField，ARD**中的SQL_DESC_SCALE字段设置为 0，SQL_DESC_PRECISION字段设置为驱动程序定义的默认精度。 当 APD 中的SQL_DESC_TYPE字段设置为SQL_C_NUMERIC时，通过调用**SQLBind 参数**或**SQLSetDescField，** 也是如此。 对于输入、输入/输出或输出参数，情况也是如此。  
  
 如果应用程序不能接受前面描述的任一默认值，则应用程序应通过调用**SQLSetDescField**或**SQLSetDescRec**来设置SQL_DESC_SCALE或SQL_DESC_PRECISION字段。  
  
 如果应用程序调用**SQLGetData**将数据返回到SQL_C_NUMERIC结构中，则使用默认SQL_DESC_SCALE和SQL_DESC_PRECISION字段。 如果默认值不可接受，则应用程序必须调用**SQLSetDescRec**或**SQLSetDescField**来设置字段，然后使用*目标类型*SQL_ARD_TYPE调用**SQLGetData**以使用描述符字段中的值。  
  
 调用**SQLPutData**时，调用使用与执行时的数据参数或列对应的描述符记录SQL_DESC_SCALE和SQL_DESC_PRECISION字段，这些字段是调用**SQLExecute**或**SQLExecDirect**的 APD 字段，或调用**SQLBulk 操作**或**SQLSetPos**的 ARD 字段。
