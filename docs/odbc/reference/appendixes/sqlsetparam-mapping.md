---
title: SQLSetParam Mapping | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c5d420bc68c4704705018a37c6459181481b1d7d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63297464"
---
# <a name="sqlsetparam-mapping"></a>SQLSetParam 映射
**SQLSetParam**的映射将继续**SQLBindParameter**如 ODBC 2 中所示。*x*。 即使它是从概念上讲类似于**SQLBindParam**，驱动程序管理器不会映射**SQLSetParam**到**SQLBindParam**。 这是因为某些现有的 ODBC 2。*x*驱动程序使用的特殊值*BufferLength* (SQL_SETPARAM_VALUE_MAX) 驱动程序管理器时，生成它映射**SQLSetParam**顶部的**SQLBindParameter**以便确定一个 1 时调用它。*x* ODBC 应用程序。  
  
 对的调用  
  
```  
SQLSetParam(hstmt, ipar, fCType, fSqlType, cbColDef, ibScale, rgbValue, pcbValue)  
```  
  
 将导致以下：  
  
```  
SQLBindParameter(StatementHandle, ParameterNumber, SQL_PARAM_INPUT_OUTPUT, ValueType, ParameterType, ColumnSize, DecimalDigits, ParameterValuePtr, SQL_SETPARAM_VALUE_MAX, StrLen_or_IndPtr)  
```
