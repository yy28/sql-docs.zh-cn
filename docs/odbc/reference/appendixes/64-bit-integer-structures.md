---
title: 64 位整数结构 |Microsoft 文档
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
- C data types [ODBC], 64-bit integer structures
- data types [ODBC], C data types
- 64-bit integer structures [ODBC]
ms.assetid: ac80c798-d9b2-4430-85ed-bd2461db0ac7
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8760b771b4ef44f2728c0947504c46a3f7d28910
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="64-bit-integer-structures"></a>64 位整数结构
在 Microsoft C 编译器 SQL_C_SBIGINT 和 SQL_C_UBIGINT 的数据类型标识符的 C 类型是 _int64。 当使用 Microsoft® C 编译器其他编译器时，C 类型可能不同。 如果编译器支持本机 64 位整数，该驱动程序或应用程序应定义 ODBCINT64 本机 64 位整数类型。 如果编译器不以本机方式支持 64 位整数，则应用程序或驱动程序可以定义以下的结构，以确保它有权访问此数据：  
  
```  
typedef struct{  
SQLUINTEGER dwLowWord;  
SQLUINTEGER dwHighWord;  
} SQLUBIGINT  
  
typedef struct{  
SQLUINTEGER dwLowWord;  
SQLINTEGER sdwHighWord;  
} SQLBIGINT  
```  
  
 应为 8 字节边界对齐这些结构，因为与 8 字节边界对齐 64 位整数。
