---
title: 64 位整数结构 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- C data types [ODBC], 64-bit integer structures
- data types [ODBC], C data types
- 64-bit integer structures [ODBC]
ms.assetid: ac80c798-d9b2-4430-85ed-bd2461db0ac7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1ecbe4dae4c1bd21ac3d542ee0d9b18169df0116
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307508"
---
# <a name="64-bit-integer-structures"></a>64 位整数结构
_int64，_int64 microsoft C 编译器上SQL_C_SBIGINT和SQL_C_UBIGINT数据类型标识符的 C 类型。 当使用 Microsoft 以外的编译器® C 编译器时，C 类型可能不同。 如果编译器本机支持 64 位整数，则驱动程序或应用程序应将 ODBCINT64 定义为本机 64 位整数类型。 如果编译器本机不支持 64 位整数，则应用程序或驱动程序可以定义以下结构，以确保它有权访问此数据：  
  
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
  
 这些结构应与 8 字节边界对齐，因为 64 位整数与 8 字节边界对齐。
