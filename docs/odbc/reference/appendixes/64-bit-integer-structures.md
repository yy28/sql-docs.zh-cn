---
title: "64 位整数结构 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- C data types [ODBC], 64-bit integer structures
- data types [ODBC], C data types
- 64-bit integer structures [ODBC]
ms.assetid: ac80c798-d9b2-4430-85ed-bd2461db0ac7
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b267e536535d0df75e1f7c048baa31099c97a704
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

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
