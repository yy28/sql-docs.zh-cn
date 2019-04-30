---
title: 重写的数值数据类型默认精度和小数位数 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5f071cf4391c760f7d269382537c3cd4f2b758c3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63278310"
---
# <a name="overriding-default-precision-and-scale-for-numeric-data-types"></a>重写数字数据类型的默认精度和小数位数
如果 ARD 中的 SQL_DESC_TYPE 字段设置为 SQL_C_NUMERIC，通过调用**SQLBindCol**或**SQLSetDescField**中 ARD, SQL_DESC_SCALE 字段设置为 0 并且 SQL_DESC_PRECISION 字段设置为驱动程序定义的默认精度。 这也是如此 APD 中的 SQL_DESC_TYPE 字段设置为 SQL_C_NUMERIC，通过调用时**SQLBindParameter**或**SQLSetDescField**。 这适用于输入、 输入/输出或输出参数。  
  
 如果所述的默认值的任何一个以前不接受的应用程序，该应用程序应通过调用设置 SQL_DESC_SCALE 或 SQL_DESC_PRECISION 字段**SQLSetDescField**或**SQLSetDescRec**.  
  
 如果应用程序调用**SQLGetData**为了将数据返回到 SQL_C_NUMERIC 结构，使用了默认 SQL_DESC_SCALE 和 SQL_DESC_PRECISION 字段。 如果不接受默认设置的应用程序必须调用**SQLSetDescRec**或**SQLSetDescField**若要设置的字段，然后调用**SQLGetData**与*TargetType*的 SQL_ARD_TYPE 若要使用中的描述符字段的值。  
  
 当**SQLPutData**是调用，调用使用对应于执行时数据参数或列，描述符记录的 SQL_DESC_SCALE 和 SQL_DESC_PRECISION 字段是对的调用 APD 字段**SQLExecute**或**SQLExecDirect**，或对的调用 ARD 字段**SQLBulkOperations**或**SQLSetPos**。
