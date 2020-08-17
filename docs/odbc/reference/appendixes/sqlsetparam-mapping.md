---
description: SQLSetParam 映射
title: SQLSetParam 映射 |Microsoft Docs
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
ms.openlocfilehash: e2c16f942920b5fefff664cc647f4edfc9ab6d13
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88339293"
---
# <a name="sqlsetparam-mapping"></a>SQLSetParam 映射
**SQLSetParam** 继续作为 ODBC 2 中的 **SQLBindParameter** 上的映射。*x*。 尽管它在概念上类似于 **SQLBindParam**，但驱动程序管理器不会将 **SQLSetParam** 映射到 **SQLBindParam**。 这是因为某些现有的 ODBC 2。*x* 驱动程序使用 *BufferLength* (SQL_SETPARAM_VALUE_MAX 的特殊值) 当驱动程序管理器将 **SQLSetParam** 映射到 **SQLBindParameter** 上时生成的值，以确定它是由1调用的。*x* ODBC 应用程序。  
  
 调用  
  
```  
SQLSetParam(hstmt, ipar, fCType, fSqlType, cbColDef, ibScale, rgbValue, pcbValue)  
```  
  
 将导致以下内容：  
  
```  
SQLBindParameter(StatementHandle, ParameterNumber, SQL_PARAM_INPUT_OUTPUT, ValueType, ParameterType, ColumnSize, DecimalDigits, ParameterValuePtr, SQL_SETPARAM_VALUE_MAX, StrLen_or_IndPtr)  
```
