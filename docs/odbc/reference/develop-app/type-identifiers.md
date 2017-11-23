---
title: "类型标识符 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data types [ODBC], identifiers
- type identifiers [ODBC]
- identifiers [ODBC], type
- type identifiers [ODBC], about type identifiers
ms.assetid: 1d9fdfa2-e378-44fe-ac66-9743d9bbdd5a
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7abb798241e26114425911e86756bc31d3489257
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="type-identifiers"></a>类型标识符
若要描述 SQL 和 C 数据类型，ODBC 定义两套*类型标识符*。 类型标识符描述的 SQL 列或 C 缓冲区的类型。 它是**#define**值，和是通常作为函数自变量传递或在元数据中返回。  
  
 例如，以下调用**SQLBindParameter**将 SQL_DATE_STRUCT 类型的变量绑定到的 SQL 语句中的日期参数。 C 类型标识符 SQL_C_TYPE_DATE 指定的一种*日期*变量，且 SQL 类型标识符 SQL_TYPE_DATE，则指定动态参数的类型。  
  
```  
SQL_DATE_STRUCT Date;  
SQLINTEGER  DateInd = 0;  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_TYPE_DATE, SQL_TYPE_DATE, 0, 0,  
                  &Date, 0, &DateInd);  
```
