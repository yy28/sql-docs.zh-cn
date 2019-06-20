---
title: 从 SQL 到 C：二进制 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to c types [ODBC], binary
- binary data type [ODBC]
- data conversions from SQL to C types [ODBC], binary
- binary data transfers [ODBC]
ms.assetid: 8c519072-ae4c-4d32-9d4e-775e3d3d6389
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 16112ca3b66e0218efd54d3bf385e04cb654e3e4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63270961"
---
# <a name="sql-to-c-binary"></a>从 SQL 到 C：Binary
是二进制的 ODBC SQL 数据类型的标识符：  
  
 SQL_BINARY  
  
 SQL_VARBINARY  
  
 SQL_LONGVARBINARY  
  
 下表显示 ODBC C 数据类型可能会转换成 SQL 的二进制数据。 列和表中的条款的说明，请参阅[从 SQL 到 C 数据类型的转换的数据](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  
  
|C 类型标识符|测试|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|（数据的字节长度）\* 2 < *BufferLength*<br /><br /> （数据的字节长度）\* 2 > = *BufferLength*|数据<br /><br /> 截断的数据|以字节为单位的数据的长度<br /><br /> 以字节为单位的数据的长度|不适用<br /><br /> 01004|  
|SQL_C_WCHAR|（字符长度的数据）\* 2 < *BufferLength*<br /><br /> （字符长度的数据）\* 2 > = *BufferLength*|数据<br /><br /> 截断的数据|以字符为单位的数据的长度<br /><br /> 以字符为单位的数据的长度|不适用<br /><br /> 01004|  
|SQL_C_BINARY|数据的字节长度 < = *BufferLength*<br /><br /> 数据的字节长度 > *BufferLength*|数据<br /><br /> 截断的数据|以字节为单位的数据的长度<br /><br /> 以字节为单位的数据的长度|不适用<br /><br /> 01004|  
  
 当 SQL 的二进制数据转换为 C 字符数据时，源数据的每个字节 （8 位） 表示为两个 ASCII 字符。 这些字符是数字的 ASCII 字符表示形式中十六进制形式。 例如，二进制 00000001 转换为"01"，二进制 11111111 转换为"FF"。  
  
 驱动程序始终将单个字节转换为十六进制数字的对，并终止 null 字节字符字符串。 因此，如果*BufferLength*甚至是和转换后的数据的最后一个字节的长度小于 **TargetValuePtr*不使用缓冲区。 （转换后的数据需要偶数个字节下, 一步至最后一个字节是 null 字节，并且不能使用的最后一个字节。）  
  
> [!NOTE]  
>  应用程序开发人员不建议从二进制 SQL 将数据绑定到字符 C 数据类型。 此转换通常是效率低下，而且很慢。
