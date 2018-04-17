---
title: SQLSetParam 映射 |Microsoft 文档
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
ms.topic: article
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLSetParam
- SQLSetParam function [ODBC], mapping
ms.assetid: 022dfbc0-8d18-4c35-8a28-d9eb16063188
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a784ec60a7b88f3ace601a8ce18ff05263803441
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sqlsetparam-mapping"></a>SQLSetParam 映射
**SQLSetParam**继续映射的顶部**SQLBindParameter**如 ODBC 2 所示。*x*。 即使它是从概念上讲类似于**SQLBindParam**，驱动程序管理器未映射**SQLSetParam**到**SQLBindParam**。 这是因为某些现有的 ODBC 2。*x*驱动程序使用的特殊值*BufferLength* (SQL_SETPARAM_VALUE_MAX) 驱动程序管理器时，生成它映射**SQLSetParam**之上**SQLBindParameter**以便确定一个 1 时调用它。*x* ODBC 应用程序。  
  
 对的调用  
  
```  
SQLSetParam(hstmt, ipar, fCType, fSqlType, cbColDef, ibScale, rgbValue, pcbValue)  
```  
  
 将导致以下：  
  
```  
SQLBindParameter(StatementHandle, ParameterNumber, SQL_PARAM_INPUT_OUTPUT, ValueType, ParameterType, ColumnSize, DecimalDigits, ParameterValuePtr, SQL_SETPARAM_VALUE_MAX, StrLen_or_IndPtr)  
```
