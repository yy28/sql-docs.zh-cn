---
title: C 到 SQL： GUID |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from c to SQL types [ODBC], guid
- data conversions from C to SQL types [ODBC], guid
- GUID data type [ODBC]
ms.assetid: 9168b0b6-a828-4fef-b8cd-bdf439776f23
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b3b559499273e885e23da10d9093a0ce9ff92393
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306618"
---
# <a name="c-to-sql-guid"></a>从 C 到 SQL：GUID
GUID ODBC C 数据类型的标识符是：  
  
 SQL_C_GUID  
  
 下表显示了 GUID C 数据可以转换为的 ODBC SQL 数据类型。 有关表中列和术语的说明，请参阅[将数据从 C 转换为 SQL 数据类型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
|SQL 类型标识符|测试|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR|列字节长度>= 36|不适用|  
|SQL_VARCHAR|柱字节长度< 36|22001|  
|SQL_LONGVARCHAR|数据值不是有效的 GUID|22018|  
|SQL_WCHAR|列字符长度>= 36|不适用|  
|SQL_WVARCHAR|列字符长度< 36|22001|  
|SQL_WLONGVARCHAR|数据值不是有效的 GUID|22018|  
|SQL_GUID|无[a]|不适用|  
  
 [a] 所有十六进制值都作为 GUID 有效。  
  
 驱动程序在从 GUID C 数据类型转换数据时忽略长度/指示器值，并假定数据缓冲区的大小是 GUID C 数据类型的大小。 长度/指标值在**SQLPutData**中的*StrLen_or_Ind*参数中传递，在**SQLBind 参数**中用*StrLen_or_IndPtr*参数指定的缓冲区中传递。 数据缓冲区使用**SQLPutData**中的*DataPtr*参数和**SQLBind 参数**中的*参数ValuePtr*参数指定。
