---
title: "To SQL 的 C: GUID |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- converting data from c to SQL types [ODBC], guid
- data conversions from C to SQL types [ODBC], guid
- GUID data type [ODBC]
ms.assetid: 9168b0b6-a828-4fef-b8cd-bdf439776f23
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9a393aefa101bef2738e15ed12b0f1679e4a6c9c
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="c-to-sql-guid"></a>To SQL 的 C: GUID
GUID ODBC C 数据类型的标识符是：  
  
 SQL_C_GUID  
  
 下表显示 ODBC SQL GUID C 数据可能转换到的目标的数据类型。 列和表中的条款的说明，请参阅[C 中为 SQL 数据类型的转换的数据](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
|SQL 类型标识符|测试|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR|列字节长度 > = 36|不适用|  
|SQL_VARCHAR|列字节长度 < 36|22001|  
|SQL_LONGVARCHAR|数据值不是有效的 GUID|22018|  
|SQL_WCHAR|列的字符长度 > = 36|不适用|  
|SQL_WVARCHAR|列字符长度 < 36|22001|  
|SQL_WLONGVARCHAR|数据值不是有效的 GUID|22018|  
|SQL_GUID|无 [a]|不适用|  
  
 [a] 所有的十六进制值都作为 GUID 无效。  
  
 该驱动程序时将数据从 GUID C 数据类型转换忽略长度/指示器值，并假定数据缓冲区的大小为 GUID C 数据类型的大小。 长度/指示器值将传递中*StrLen_or_Ind*中的参数**SQLPutData**和中与指定的缓冲区*StrLen_or_IndPtr*中参数**SQLBindParameter**。 使用指定的数据缓冲区*DataPtr*中的参数**SQLPutData**和*ParameterValuePtr*中的参数**SQLBindParameter**.
