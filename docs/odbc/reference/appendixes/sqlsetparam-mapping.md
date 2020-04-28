---
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
ms.openlocfilehash: 4d8e632412965664e5cdd9c87dc1e26787dcdab2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300527"
---
# <a name="sqlsetparam-mapping"></a>SQLSetParam 映射
**SQLSetParam**继续作为 ODBC 2 中的**SQLBindParameter**上的映射。*x*。 尽管它在概念上类似于**SQLBindParam**，但驱动程序管理器不会将**SQLSetParam**映射到**SQLBindParam**。 这是因为某些现有的 ODBC 2。*x*驱动程序使用当驱动程序管理器将**SQLSetParam**映射到**SQLBindParameter**时所生成的特殊值*BufferLength* （SQL_SETPARAM_VALUE_MAX）来确定它是由1调用的。*x* ODBC 应用程序。  
  
 调用  
  
```  
SQLSetParam(hstmt, ipar, fCType, fSqlType, cbColDef, ibScale, rgbValue, pcbValue)  
```  
  
 将导致以下内容：  
  
```  
SQLBindParameter(StatementHandle, ParameterNumber, SQL_PARAM_INPUT_OUTPUT, ValueType, ParameterType, ColumnSize, DecimalDigits, ParameterValuePtr, SQL_SETPARAM_VALUE_MAX, StrLen_or_IndPtr)  
```
