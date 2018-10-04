---
title: 从 C 到 SQL： 二进制 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- binary data type [ODBC]
- data conversions from C to SQL types [ODBC], binary
- binary data transfers [ODBC]
- converting data from c to SQL types [ODBC], binary
ms.assetid: 3e9083f3-357b-41aa-833c-2c8aac2226cd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 76c2e4673d9b561aeb5af3e61e1e4dc8532195d6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47849125"
---
# <a name="c-to-sql-binary"></a>从 C 到 SQL：二进制
是二进制的 ODBC C 数据类型的标识符：  
  
 SQL_C_BINARY  
  
 下表显示 ODBC SQL 数据类型可能会转换为 C 的二进制数据。 列和表中的条款的说明，请参阅[转换将数据从 C 到 SQL 数据类型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
|SQL 类型标识符|测试|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|数据的字节长度 < = 列的字节长度<br /><br /> 数据的字节长度 > 列的字节长度|不适用<br /><br /> 22001|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|字符数据的长度 < = 列的字符长度<br /><br /> 字符数据的长度 > 列的字符长度|不适用<br /><br /> 22001|  
|SQL_DECIMAL<br /><br /> SQL_NUMERIC<br /><br /> SQL_TINYINT<br /><br /> SQL_SMALLINT<br /><br /> SQL_INTEGER<br /><br /> SQL_BIGINT<br /><br /> SQL_REAL<br /><br /> SQL_FLOAT<br /><br /> SQL_DOUBLE<br /><br /> SQL_BIT SQL_TYPE_DATE<br /><br /> SQL_TYPE_TIME<br /><br /> SQL_TYPE_TIMESTAMP|数据的字节长度 = SQL 数据长度<br /><br /> 数据 <> SQL 数据长度的字节长度|不适用<br /><br /> 22003|  
|SQL_BINARY<br /><br /> SQL_VARBINARY<br /><br /> SQL_LONGVARBINARY|数据的长度 < = 列长度<br /><br /> 数据的长度 > 列长度|不适用<br /><br /> 22001|
