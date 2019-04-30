---
title: 从 SQL 到 C：Bit | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to c types [ODBC], bit
- bit data type [ODBC]
- data conversions from SQL to C types [ODBC], bit
ms.assetid: 0eeaab8b-ad82-4a36-b464-9a1211d5f72c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f7ff0bd2988460596623eb47ded276392dc3d443
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63270981"
---
# <a name="sql-to-c-bit"></a>从 SQL 到 C：bit
对于 ODBC SQL 数据类型是的位标识符：  
  
 SQL_BIT  
  
 下表显示 ODBC C 数据类型位的 SQL 数据可能会转换为。 列和表中的条款的说明，请参阅[从 SQL 到 C 数据类型的转换的数据](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  
  
|C 类型标识符|测试|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR<br /><br /> SQL_C_WCHAR|*BufferLength* > 1<br /><br /> *BufferLength* <= 1|数据<br /><br /> 未定义|1<br /><br /> 未定义|不适用<br /><br /> 22003|  
|SQL_C_STINYINT<br /><br /> SQL_C_UTINYINT<br /><br /> SQL_C_TINYINT<br /><br /> SQL_C_SBIGINT<br /><br /> SQL_C_UBIGINT<br /><br /> SQL_C_SSHORT<br /><br /> SQL_C_USHORT<br /><br /> SQL_C_SHORT<br /><br /> SQL_C_SLONG<br /><br /> SQL_C_ULONG<br /><br /> SQL_C_LONG<br /><br /> SQL_C_FLOAT<br /><br /> SQL_C_DOUBLE<br /><br /> SQL_C_NUMERIC|None[a]|数据|C 数据类型的大小|不适用|  
|SQL_C_BIT|None[a]|数据|1[b]|不适用|  
|SQL_C_BINARY|*BufferLength* >= 1<br /><br /> *BufferLength* < 1|数据<br /><br /> 未定义|1<br /><br /> 未定义|不适用<br /><br /> 22003|  
  
 [a] 的值*BufferLength*忽略此转换。 驱动程序假定的大小 **TargetValuePtr*是 C 数据类型的大小。  
  
 [b] 这是相应的 C 数据类型的大小。  
  
 当位 SQL 数据转换为 C 字符数据时，可能的值为"0"和"1"。
