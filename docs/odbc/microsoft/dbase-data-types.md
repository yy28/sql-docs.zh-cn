---
title: dBASE 数据类型 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], DBasedriver
- desktop database drivers [ODBC], DBasedriver
- DBase driver [ODBC], data types
- data types [ODBC], DBase driver
- dbase data types [ODBC]
- ODBC desktop database drivers [ODBC], DBasedriver
ms.assetid: a0e31e6b-d02b-4ee2-9b37-5baf6a11c0a6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 17b96ad0b6674a2d120ef46d9bfa221e8df6d140
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307688"
---
# <a name="dbase-data-types"></a>dBASE 数据类型
下表显示了如何将 dBASE 数据类型映射到 ODBC SQL 数据类型。 请注意，并非所有 ODBC SQL 数据类型都受支持。  
  
|dBASE 数据类型|ODBC 数据类型|  
|---------------------|--------------------|  
|CHAR|SQL_VARCHAR|  
|DATE|SQL_DATE|  
|浮点[1]|SQL_DOUBLE|  
|逻辑|SQL_BIT|  
|备忘录|SQL_LONGVARCHAR|  
|数字 （BCD）|SQL_DOUBLE|  
|OLEOBJECT[1]|SQL_LONGBINARY|  
  
 [1] 仅适用于 dBASE 版本 5。*x*  
  
 dBASE III 中的精度允许具有最多两位指数的数字，以及最多三位指数的 dBASE IV 数字。 由于数字存储为文本，因此它们将转换为数字。 如果要转换的数字不适合字段，则可能会出现无法解释的结果。  
  
 虽然 dBASE 允许使用 NUMERIC 数据类型指定精度和比例，但 ODBC dBASE 驱动程序不支持它。 ODBC dBASE 驱动程序始终返回数字数据类型的精度为 15 和 0 的比例。  
  
 使用 ODBC dBASE 驱动程序创建的使用数字数据类型创建的列映射到 SQL_DOUBLE ODBC 数据类型。 因此，此列中的数据需要四舍五入。 此行为与 dBASE（类型 N）中的数字数据类型不同，后者为二进制编码十进制十进制 （BCD）。  
  
> [!NOTE]  
>  **SQLGetTypeInfo**返回 ODBC SQL 数据类型。 本主题前面列出的 ODBC SQL 数据类型都支持*ODBC 程序员参考*附录 D 中的所有转换。  
  
 下表显示了对 dBASE 数据类型的限制。  
  
|数据类型|描述|  
|---------------|-----------------|  
|CHAR|创建零或未指定长度的 CHAR 列实际上返回 254 字节列。|  
|加密数据|dBASE 驱动程序不支持加密的 dBASE 表。|  
|逻辑|dBASE 驱动程序无法在"逻辑"列上创建索引。|  
|备忘录|MEMO 列的最大长度为 65，500 字节。|  
  
 数据类型的更多限制可以在[数据类型限制](../../odbc/microsoft/data-type-limitations.md)中找到。
