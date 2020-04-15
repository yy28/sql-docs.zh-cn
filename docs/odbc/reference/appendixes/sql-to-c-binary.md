---
title: SQL 到 C： 二进制 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 70b0ce72f650e61b83ec99b0727752612d18da52
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298817"
---
# <a name="sql-to-c-binary"></a>从 SQL 到 C：二进制
二进制 ODBC SQL 数据类型的标识符包括：  
  
 SQL_BINARY  
  
 SQL_VARBINARY  
  
 SQL_LONGVARBINARY  
  
 下表显示了可转换为二进制 SQL 数据的 ODBC C 数据类型。 有关表中列和术语的说明，请参阅[将数据从 SQL 转换为 C 数据类型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  
  
|C 类型标识符|测试|**目标价值Ptr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|（数据字节长度）\* 2 <*缓冲区长度*<br /><br /> （数据字节长度）\* 2 >=*缓冲区长度*|数据<br /><br /> 截断的数据|以字节为单位的数据长度<br /><br /> 以字节为单位的数据长度|不适用<br /><br /> 01004|  
|SQL_C_WCHAR|（数据字符长度）\* 2 <*缓冲区长度*<br /><br /> （数据字符长度）\* 2 >=*缓冲区长度*|数据<br /><br /> 截断的数据|字符中的数据长度<br /><br /> 字符中的数据长度|不适用<br /><br /> 01004|  
|SQL_C_BINARY|数据<字节长度 =*缓冲区长度*<br /><br /> >*缓冲区长度*的数据字节长度|数据<br /><br /> 截断的数据|以字节为单位的数据长度<br /><br /> 以字节为单位的数据长度|不适用<br /><br /> 01004|  
  
 当二进制 SQL 数据转换为字符 C 数据时，源数据的每个字节（8 位）表示为两个 ASCII 字符。 这些字符是十六进制形式数字的 ASCII 字符表示形式。 例如，二进制 00000001 转换为"01"，二进制 11111111 转换为"FF"。  
  
 驱动程序始终将单个字节转换为十六进制数字对，并且使用空字节终止字符字符串。 因此，如果*BufferLength*是偶数且小于转换数据的长度，则不使用 **TargetValuePtr*缓冲区的最后一个字节。 （转换后的数据需要偶数字节，倒数第二个字节为空字节，无法使用最后一个字节。  
  
> [!NOTE]  
>  禁止应用程序开发人员将二进制 SQL 数据绑定到字符 C 数据类型。 此转换通常效率低下且速度缓慢。
