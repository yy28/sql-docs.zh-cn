---
title: Microsoft Access 数据类型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 11f45698a5ad8b7fd05052cbb2d23520790c425a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47692975"
---
# <a name="microsoft-access-data-types"></a>Microsoft Access 数据类型
下表显示了 Microsoft Access 数据类型、 用于创建表的数据类型和 ODBC SQL 数据类型。  
  
|Microsoft Access 数据类型|数据类型 (CREATETABLE)|ODBC SQL 数据类型|  
|--------------------------------|-------------------------------|------------------------|  
|BIGBINARY [1]|LONGBINARY|SQL_LONGVARBINARY|  
|BINARY|BINARY|SQL_BINARY|  
|BIT|BIT|SQL_BIT|  
|计数器|计数器|SQL_INTEGER|  
|货币|货币|SQL_NUMERIC|  
|日期/时间|DATETIME|SQL_TIMESTAMP|  
|GUID|GUID|SQL_GUID|  
|长度的二进制|LONGBINARY|SQL_LONGVARBINARY|  
|长文本|长文本|SQL_WLONGVARCHAR SQL_LONGVARCHAR [2] [3]|  
|备注|长文本|SQL_WLONGVARCHAR SQL_LONGVARCHAR [2] [3]|  
|数字 (字段大小 = 单)|单个|SQL_REAL|  
|数字 (字段大小 = 双精度型)|DOUBLE|SQL_DOUBLE|  
|数字 (字段大小 = BYTE)|无符号的字节|SQL_TINYINT|  
|数字 (字段大小 = 整数)|短|SQL_SMALLINT|  
|数字 (字段大小 = 长整型)|LONG|SQL_INTEGER|  
|NUMERIC|NUMERIC|SQL_NUMERIC|  
|OLE|LONGBINARY|SQL_LONGVARBINARY|  
|TEXT|VARCHAR|[1] SQL_VARCHAR SQL_WVARCHAR [2]|  
ARBINARY|VARBINARY|SQL_VARBINARY|  
  
 [1] 访问仅限于 4.0 应用程序。 最大长度为 4000 字节。 与 LONGBINARY 相似的行为。  
  
 [2] ANSI 仅限于应用程序。  
  
 [Unicode 3] 和访问 4.0 仅限于应用程序。  
  
> [!NOTE]  
>  **SQLGetTypeInfo**返回的 ODBC 数据类型。 如果多个 Microsoft Access 类型映射到相同的 ODBC SQL 数据类型，它不会返回所有 Microsoft Access 数据类型。 所有转换中的附录 D *ODBC 程序员参考*上表中列出的 SQL 数据类型支持。  
  
 下表显示有关 Microsoft Access 数据类型的限制。  
  
|数据类型|Description|  
|---------------|-----------------|  
|二进制、 VARBINARY 和 VARCHAR|创建 BINARY、 VARBINARY 或 VARCHAR 列的零或未指定的长度实际上返回一个 510 字节的列。|  
|BYTE|即使 Microsoft 访问号码字段与字段大小等于字节无符号，负号可以插入到的字段中，使用 Microsoft Access 驱动程序时。|  
|CHAR、 LONGVARCHAR 和 VARCHAR|字符的字符串文本可以包含任何 ANSI 字符 （1-255 十进制）。 使用两个连续单引号 （'） 来表示一个单引号 （'）。<br /><br /> 应使用过程将传递字符数据，在字符数据类型列中使用任何特殊字符时。|  
|DATE|日期值必须分隔根据 ODBC 规范的日期格式或以日期时间分隔符 （"#"） 分隔。 否则为 Microsoft Access 将值视为算术表达式，并且不会引发警告或错误。<br /><br /> 例如，"1996 年 3 月 5 日"必须表示为日期 {d 1996年-03-05} 或 #03/05/1996年 #;否则，如果仅提交 03/05/1993年，Microsoft Access 计算此为 3 除以 5 除以 1996年。 此值将向上舍入为整数 0，并且由于零天将映射到 1899年-12-31，这是使用的日期。<br /><br /> 竖线字符 (&#124;) 不能使用的日期值中，即使后退用引号引起来。|  
|GUID|限于 Microsoft 访问 4.0 数据类型。|  
|NUMERIC|限于 Microsoft 访问 4.0 数据类型。|  
  
 了解更多限制，对数据类型可在[数据类型限制](../../odbc/microsoft/data-type-limitations.md)。
