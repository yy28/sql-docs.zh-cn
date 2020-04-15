---
title: 类型标识符 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a274a19eaa0a2fdf98bcaa9ef42406ee8a6b6461
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306428"
---
# <a name="type-identifiers"></a>类型标识符
为了描述 SQL 和 C 数据类型，ODBC 定义了两组*类型标识符*。 类型标识符描述 SQL 列或 C 缓冲区的类型。 它是**一个#define**值，通常作为函数参数传递或在元数据中返回。  
  
 例如，以下对**SQLBind 参数**的调用将类型SQL_DATE_STRUCT变量绑定到 SQL 语句中的日期参数。 C 类型标识符SQL_C_TYPE_DATE指定*Date*变量的类型，SQL 类型标识符SQL_TYPE_DATE指定动态参数的类型。  
  
```  
SQL_DATE_STRUCT Date;  
SQLINTEGER  DateInd = 0;  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_TYPE_DATE, SQL_TYPE_DATE, 0, 0,  
                  &Date, 0, &DateInd);  
```
