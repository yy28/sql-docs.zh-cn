---
title: 类型标识符 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], identifiers
- type identifiers [ODBC]
- identifiers [ODBC], type
- type identifiers [ODBC], about type identifiers
ms.assetid: 1d9fdfa2-e378-44fe-ac66-9743d9bbdd5a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 79aa4de5d722208195477f7ffef53cac6c61a2de
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68093023"
---
# <a name="type-identifiers"></a>类型标识符
若要描述 SQL 和 C 数据类型，ODBC 定义的两个集*类型标识符*。 类型标识符描述 SQL 列或 C 缓冲区中的类型。 它是 **#define**值，并且是通常作为函数参数传递或返回元数据中。  
  
 例如，以下调用到**SQLBindParameter**将 SQL_DATE_STRUCT 类型的变量绑定到的 SQL 语句中的日期参数。 C 类型标识符 SQL_C_TYPE_DATE 指定的类型*日期*变量和 SQL 类型标识符 SQL_TYPE_DATE 指定的动态参数的类型。  
  
```  
SQL_DATE_STRUCT Date;  
SQLINTEGER  DateInd = 0;  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_TYPE_DATE, SQL_TYPE_DATE, 0, 0,  
                  &Date, 0, &DateInd);  
```
