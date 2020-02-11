---
title: 64位整数结构 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 93d9e6fd01d6b9ef98ebb10f6728ec4ba205fbb5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67996254"
---
# <a name="64-bit-integer-structures"></a>64 位整数结构
Microsoft C 编译器上的 SQL_C_SBIGINT 和 SQL_C_UBIGINT 数据类型标识符 _int64 的 C 类型。 使用 Microsoft® C 编译器以外的编译器时，C 类型可能不同。 如果编译器以本机方式支持64位整数，则驱动程序或应用程序应将 ODBCINT64 定义为本机64位整数类型。 如果编译器不以本机方式支持64位整数，则应用程序或驱动程序可以定义以下结构，以确保它有权访问此数据：  
  
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
  
 这些结构应与8字节边界对齐，因为64位整数与8字节边界对齐。
