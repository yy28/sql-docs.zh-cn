---
title: 从 C 到 SQL：GUID | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5863935ddf595409d48be79dc646c0994ddeb0b8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68019320"
---
# <a name="c-to-sql-guid"></a>从 C 到 SQL：GUID
GUID ODBC C 数据类型的标识符是：  
  
 SQL_C_GUID  
  
 下表显示 ODBC SQL GUID C 数据可能会转换成的数据类型。 列和表中的条款的说明，请参阅[转换将数据从 C 到 SQL 数据类型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
|SQL 类型标识符|测试|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR|列的字节长度 > = 36|不适用|  
|SQL_VARCHAR|列字节长度 < 36|22001|  
|SQL_LONGVARCHAR|数据值不是有效的 GUID|22018|  
|SQL_WCHAR|列的字符长度 > = 36|不适用|  
|SQL_WVARCHAR|列的字符长度 < 36|22001|  
|SQL_WLONGVARCHAR|数据值不是有效的 GUID|22018|  
|SQL_GUID|无 [a]|不适用|  
  
 [a] 所有的十六进制值都有效以 GUID 形式表示。  
  
 该驱动程序将数据从 GUID C 数据类型转换时将忽略此长度/指示器值，并假定数据缓冲区的大小是 GUID C 数据类型的大小。 中传递的长度/指示器值*StrLen_or_Ind*中的参数**SQLPutData**并使用指定的缓冲区中*StrLen_or_IndPtr*中参数**SQLBindParameter**。 使用指定的数据缓冲区*DataPtr*中的参数**SQLPutData**并*ParameterValuePtr*中的参数**SQLBindParameter**.
