---
title: "为 c： 二进制 SQL |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- converting data from SQL to c types [ODBC], binary
- binary data type [ODBC]
- data conversions from SQL to C types [ODBC], binary
- binary data transfers [ODBC]
ms.assetid: 8c519072-ae4c-4d32-9d4e-775e3d3d6389
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: cf5191b9fa41af5c0e180f9ad605f9563cbcf8bc
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="sql-to-c-binary"></a>为 c： 二进制 SQL
二进制 ODBC SQL 数据类型的标识符都是：  
  
 SQL_BINARY  
  
 SQL_VARBINARY  
  
 SQL_LONGVARBINARY  
  
 下表显示 ODBC C 数据类型二进制 SQL 数据可能转换到的目标。 列和表中的条款的说明，请参阅[转换数据从 SQL C 数据类型到](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  
  
|C 类型标识符|测试|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|（数据的字节长度）\* 2 < *BufferLength*<br /><br /> （数据的字节长度）\* 2 > = *BufferLength*|data<br /><br /> 截断的数据|以字节为单位的数据的长度<br /><br /> 以字节为单位的数据的长度|不适用<br /><br /> 01004|  
|SQL_C_WCHAR|（字符长度的数据）\* 2 < *BufferLength*<br /><br /> （字符长度的数据）\* 2 > = *BufferLength*|data<br /><br /> 截断的数据|以字符为单位的数据的长度<br /><br /> 以字符为单位的数据的长度|不适用<br /><br /> 01004|  
|SQL_C_BINARY|数据的字节长度 < = *BufferLength*<br /><br /> 数据的字节长度 > *BufferLength*|data<br /><br /> 截断的数据|以字节为单位的数据的长度<br /><br /> 以字节为单位的数据的长度|不适用<br /><br /> 01004|  
  
 当二进制 SQL 数据转换为字符 C 数据时，源数据的每个字节 （8 位） 都表示为两个 ASCII 字符。 这些字符是数字的 ASCII 字符表示形式中其十六进制格式。 例如，二进制 00000001 转换为"01"，二进制 11111111 转换为"FF"。  
  
 该驱动程序始终将单个字节转换为十六进制数字的对，并终止 null 字节字符字符串。 因此，如果*BufferLength*为偶数并且转换的数据的最后一个字节的长度少于 **TargetValuePtr*不会使用缓冲区。 （转换后的数据需要偶数个字节下, 一步至最后一字节是一个 null 字节，和不能使用的最后一个字节。）  
  
> [!NOTE]  
>  应用程序开发人员从二进制 SQL 将数据绑定到字符 C 数据类型建议不要使用。 此转换通常是效率低下，而且很慢。
