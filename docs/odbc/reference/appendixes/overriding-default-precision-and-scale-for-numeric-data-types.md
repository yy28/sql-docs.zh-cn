---
title: "对于数字数据类型中重写默认精度和小数位数 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- numeric data type [ODBC], precision and scale
- precision [ODBC], numeric data types
- data types [ODBC], numeric data types
- numeric data type [ODBC]
- numeric literals [ODBC]
ms.assetid: 84292334-0e33-4a1b-84de-8c018dd787f3
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 613ec65d838a525251b6682cca477c5c8d24a162
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="overriding-default-precision-and-scale-for-numeric-data-types"></a>对于数字数据类型中重写默认精度和小数位数
当在 ARD SQL_DESC_TYPE 字段设置为 SQL_C_NUMERIC，通过调用**SQLBindCol**或**SQLSetDescField**、 ARD 中的 SQL_DESC_SCALE 字段设置为 0 和 SQL_DESC_PRECISION 字段设置为驱动程序定义的默认精度。 这也是如此 APD 中的 SQL_DESC_TYPE 字段设置为 SQL_C_NUMERIC，通过调用时**SQLBindParameter**或**SQLSetDescField**。 这适用于输入、 输入/输出或输出参数。  
  
 如果任何一种所述的默认设置以前不为应用程序可接受，应用程序应通过调用设置 SQL_DESC_SCALE 或 SQL_DESC_PRECISION 字段**SQLSetDescField**或**SQLSetDescRec**.  
  
 如果应用程序调用**SQLGetData**为了在 SQL_C_NUMERIC 结构返回的数据，使用了默认 SQL_DESC_SCALE 和 SQL_DESC_PRECISION 字段。 如果默认值不是可接受的应用程序必须调用**SQLSetDescRec**或**SQLSetDescField**以设置字段，然后调用**SQLGetData**与*TargetType*的 SQL_ARD_TYPE 描述符字段中使用的值。  
  
 当**SQLPutData**是调用的调用使用 SQL_DESC_SCALE 和 SQL_DESC_PRECISION 记录的字段的描述符对应于数据在执行参数或列中，这是对调用的 APD 字段**SQLExecute**或**SQLExecDirect**，或调用的 ARD 字段**SQLBulkOperations**或**SQLSetPos**。

