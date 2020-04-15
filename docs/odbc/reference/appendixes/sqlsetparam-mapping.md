---
title: SQLSetParam 映射 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLSetParam
- SQLSetParam function [ODBC], mapping
ms.assetid: 022dfbc0-8d18-4c35-8a28-d9eb16063188
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4d8e632412965664e5cdd9c87dc1e26787dcdab2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300527"
---
# <a name="sqlsetparam-mapping"></a>SQLSetParam 映射
**SQLSetParam**继续映射到**SQLBind 参数**之上，如 ODBC 2 中一样。*x*. . 尽管它在概念上与**SQLBindParam**类似，但驱动程序管理器不会将**SQLSetParam**映射到**SQLBindParam。** 这是因为某些现有的 ODBC 2。*x*驱动程序使用驱动程序管理器在**SQLBind 参数**顶部映射**SQLSetParam**时生成的缓冲区*长度*（SQL_SETPARAM_VALUE_MAX） 的特殊值来确定何时由 1 调用它。*x* ODBC 应用。  
  
 呼叫  
  
```  
SQLSetParam(hstmt, ipar, fCType, fSqlType, cbColDef, ibScale, rgbValue, pcbValue)  
```  
  
 将导致以下结果：  
  
```  
SQLBindParameter(StatementHandle, ParameterNumber, SQL_PARAM_INPUT_OUTPUT, ValueType, ParameterType, ColumnSize, DecimalDigits, ParameterValuePtr, SQL_SETPARAM_VALUE_MAX, StrLen_or_IndPtr)  
```
