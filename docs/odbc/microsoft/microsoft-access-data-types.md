---
title: 微软访问数据类型 |微软文档
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], Access driver
- Jet-based ODBC drivers [ODBC], Access driver
- desktop database drivers [ODBC], Access driver
- Access driver [ODBC], data types
- access data types [ODBC]
- data types [ODBC], Access driver
ms.assetid: b537348a-bea0-4bd6-84a4-52a75292957f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 024fb65b6fdc81ae0a8e007d1cee150c6a35b91c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307726"
---
# <a name="microsoft-access-data-types"></a>Microsoft Access 数据类型
下表显示了 Microsoft Access 数据类型、用于创建表的数据类型和 ODBC SQL 数据类型。  
  
|微软访问数据类型|数据类型（创建表）|ODBC SQL 数据类型|  
|--------------------------------|-------------------------------|------------------------|  
|大二进制[1]|长二进制|SQL_LONGVARBINARY|  
|BINARY|BINARY|SQL_BINARY|  
|BIT|BIT|SQL_BIT|  
|计数器|计数器|SQL_INTEGER|  
|货币|货币|SQL_NUMERIC|  
|日期/时间|DATETIME|SQL_TIMESTAMP|  
|GUID|GUID|SQL_GUID|  
|长二进制|长二进制|SQL_LONGVARBINARY|  
|长文本|长文本|SQL_LONGVARCHAR[2] SQL_WLONGVARCHAR[3]|  
|备忘录|长文本|SQL_LONGVARCHAR[2] SQL_WLONGVARCHAR[3]|  
|编号（字段大小= 单）|单|SQL_REAL|  
|编号（字段大小= 双）|DOUBLE|SQL_DOUBLE|  
|编号（字段大小= 字节）|未签名字节|SQL_TINYINT|  
|数量（字段大小= 整数）|SHORT|SQL_SMALLINT|  
|数量（字段大小= 长整数）|LONG|SQL_INTEGER|  
|NUMERIC|NUMERIC|SQL_NUMERIC|  
|OLE|长二进制|SQL_LONGVARBINARY|  
|TEXT|VARCHAR|SQL_VARCHAR[1] SQL_WVARCHAR[2]|  
|VARBINARY|VARBINARY|SQL_VARBINARY|  
  
 [1] 仅访问 4.0 应用程序。 最大长度为 4000 字节。 类似于 LONGBINARY 的行为。  
  
 [2] 仅限 ANSI 应用程序。  
  
 [3] 仅 Unicode 和访问 4.0 应用程序。  
  
> [!NOTE]  
>  **SQLGetTypeInfo**返回 ODBC 数据类型。 如果将多个 Microsoft Access 类型映射到相同的 ODBC SQL 数据类型，则不会返回所有 Microsoft Access 数据类型。 对于上表中列出的 SQL 数据类型，支持*ODBC 程序员参考*附录 D 中的所有转换。  
  
 下表显示了对 Microsoft Access 数据类型的限制。  
  
|数据类型|描述|  
|---------------|-----------------|  
|BINARY、VARBINARY 和 VARCHAR|创建零或未指定长度的 BINARY、VARBINARY 或 VARCHAR 列实际上返回一个 510 字节的列。|  
|BYTE|即使字段大小等于 BYTE 的 Microsoft 访问编号字段是无符号的，但在使用 Microsoft Access 驱动程序时，也可以将负数插入到该字段中。|  
|查尔、朗瓦尔查尔和瓦尔查尔|字符串文本可以包含任何 ANSI 字符（1-255 位小数）。 使用两个连续的单引号 （''） 表示一个单引号 （'）。<br /><br /> 在字符数据类型列中使用任何特殊字符时，应使用过程来传递字符数据。|  
|DATE|日期值必须根据 ODBC 规范日期格式进行分隔，或者由日期时间分隔符 （"*"）分隔。 否则，Microsoft Access 会将该值视为算术表达式，不会引发警告或错误。<br /><br /> 例如，"1996年3月5日"的日期必须表示为[d'1996-03-05']或#03/05/1996];否则，如果只提交 03/05/1993，Microsoft Access 将对此进行评估为 3 除以 5 除以 1996。 此值舍入到整数 0，并且由于零日映射到 1899-12-31，这是使用的日期。<br /><br /> 管道字符 （&#124;） 不能用于日期值，即使包含在后引号中也是如此。|  
|GUID|数据类型仅限于 Microsoft 访问 4.0。|  
|NUMERIC|数据类型仅限于 Microsoft 访问 4.0。|  
  
 数据类型的更多限制可以在[数据类型限制](../../odbc/microsoft/data-type-limitations.md)中找到。
