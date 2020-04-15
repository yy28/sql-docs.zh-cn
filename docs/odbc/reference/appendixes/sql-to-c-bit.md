---
title: SQL 到 C：位 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 57688f34c504b221f77c1b66792bf9ee9398df27
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296747"
---
# <a name="sql-to-c-bit"></a>从 SQL 到 C：位
位 ODBC SQL 数据类型的标识符是：  
  
 SQL_BIT  
  
 下表显示了可以转换为位 SQL 数据的 ODBC C 数据类型。 有关表中列和术语的说明，请参阅[将数据从 SQL 转换为 C 数据类型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  
  
|C 类型标识符|测试|**目标价值Ptr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR<br /><br /> SQL_C_WCHAR|*缓冲区长度*> 1<br /><br /> *缓冲区长度*<= 1|数据<br /><br /> Undefined|1<br /><br /> Undefined|不适用<br /><br /> 22003|  
|SQL_C_STINYINT<br /><br /> SQL_C_UTINYINT<br /><br /> SQL_C_TINYINT<br /><br /> SQL_C_SBIGINT<br /><br /> SQL_C_UBIGINT<br /><br /> SQL_C_SSHORT<br /><br /> SQL_C_USHORT<br /><br /> SQL_C_SHORT<br /><br /> SQL_C_SLONG<br /><br /> SQL_C_ULONG<br /><br /> SQL_C_LONG<br /><br /> SQL_C_FLOAT<br /><br /> SQL_C_DOUBLE<br /><br /> SQL_C_NUMERIC|无[a]|数据|C 数据类型的大小|不适用|  
|SQL_C_BIT|无[a]|数据|1[b]|不适用|  
|SQL_C_BINARY|*缓冲区长度*>= 1<br /><br /> *缓冲区长度*< 1|数据<br /><br /> Undefined|1<br /><br /> Undefined|不适用<br /><br /> 22003|  
  
 [a] 此转换将忽略*缓冲区长度*的值。 驱动程序假定 **目标价值Ptr*的大小是 C 数据类型的大小。  
  
 [b] 这是相应的 C 数据类型的大小。  
  
 当位 SQL 数据转换为字符 C 数据时，可能的值是"0"和"1"。
