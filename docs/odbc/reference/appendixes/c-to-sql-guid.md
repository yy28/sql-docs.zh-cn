---
description: 从 C 到 SQL：GUID
title: C 到 SQL： GUID |Microsoft Docs
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
ms.openlocfilehash: 3fca2ba20df65222eaf1ce6f4384f449a1524334
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499980"
---
# <a name="c-to-sql-guid"></a>从 C 到 SQL：GUID
GUID ODBC C 数据类型的标识符是：  
  
 SQL_C_GUID  
  
 下表显示了可将 GUID C 数据转换为的 ODBC SQL 数据类型。 有关表中的列和字词的说明，请参阅 [将数据从 C 转换为 SQL 数据类型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
|SQL 类型标识符|测试|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR|列字节长度 >= 36|不适用|  
|SQL_VARCHAR|列字节长度 < 36|22001|  
|SQL_LONGVARCHAR|数据值不是有效的 GUID|22018|  
|SQL_WCHAR|列字符长度 >= 36|不适用|  
|SQL_WVARCHAR|列字符长度 < 36|22001|  
|SQL_WLONGVARCHAR|数据值不是有效的 GUID|22018|  
|SQL_GUID|None [a]|不适用|  
  
 [a] 所有十六进制值都有效，作为 GUID。  
  
 驱动程序在转换 GUID C 数据类型的数据时忽略长度/指示器值，并假定数据缓冲区的大小为 GUID C 数据类型的大小。 长度/指示器值传入**SQLPutData**中的*StrLen_or_Ind*参数和在**SQLBindParameter**中通过*StrLen_or_IndPtr*参数指定的缓冲区中。 数据缓冲区是通过**SQLPutData**中的*DataPtr*参数和**SQLBindParameter**中的*ParameterValuePtr*参数指定的。
