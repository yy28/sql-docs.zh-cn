---
title: Microsoft Access 数据类型 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], Access driver
- Jet-based ODBC drivers [ODBC], Access driver
- desktop database drivers [ODBC], Access driver
- Access driver [ODBC], data types
- access data types [ODBC]
- data types [ODBC], Access driver
ms.assetid: b537348a-bea0-4bd6-84a4-52a75292957f
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7c12bee02bd747b5f44ce5c9651b26a3cdcc3080
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32905122"
---
# <a name="microsoft-access-data-types"></a>Microsoft Access 数据类型
下表显示 Microsoft Access 数据类型、 用于创建表的数据类型和 ODBC SQL 数据类型。  
  
|Microsoft Access 数据类型|数据类型 (CREATETABLE)|ODBC SQL 数据类型|  
|--------------------------------|-------------------------------|------------------------|  
|BIGBINARY [1]|长二进制|SQL_LONGVARBINARY|  
|BINARY|BINARY|SQL_BINARY|  
|BIT|BIT|SQL_BIT|  
|计数器|计数器|SQL_INTEGER|  
|货币|货币|SQL_NUMERIC|  
|日期/时间|DATETIME|SQL_TIMESTAMP|  
|GUID|GUID|SQL_GUID|  
|长度的二进制|长二进制|SQL_LONGVARBINARY|  
|长文本|长文本|SQL_LONGVARCHAR [2] SQL_WLONGVARCHAR [3]|  
|备注|长文本|SQL_LONGVARCHAR [2] SQL_WLONGVARCHAR [3]|  
|数 (字段大小 = 单)|单个|SQL_REAL|  
|数 (字段大小 = 双精度型)|DOUBLE|SQL_DOUBLE|  
|数 (字段大小 = 字节)|无符号的字节|SQL_TINYINT|  
|数 (字段大小 = 整数)|短|SQL_SMALLINT|  
|数 (字段大小 = 长整型)|LONG|SQL_INTEGER|  
|NUMERIC|NUMERIC|SQL_NUMERIC|  
|OLE|长二进制|SQL_LONGVARBINARY|  
|TEXT|VARCHAR|SQL_VARCHAR [1] SQL_WVARCHAR [2]|  
ARBINARY|VARBINARY|SQL_VARBINARY|  
  
 [1] 访问仅限于 4.0 的应用程序。 最大长度为 4000 字节。 行为类似于长二进制。  
  
 [2] ANSI 仅限于应用程序。  
  
 [Unicode 3] 和访问 4.0 仅限于应用程序。  
  
> [!NOTE]  
>  **SQLGetTypeInfo**返回 ODBC 数据类型。 如果多个 Microsoft Access 类型映射到相同的 ODBC SQL 数据类型，它将不会返回所有 Microsoft Access 数据类型。 附录 D 中的所有转换*ODBC 程序员参考*对上表中列出的 SQL 数据类型的支持。  
  
 下表显示了有关 Microsoft Access 数据类型的限制。  
  
|数据类型|Description|  
|---------------|-----------------|  
|BINARY、 VARBINARY 和 VARCHAR|创建二进制、 VARBINARY 或 VARCHAR 列的零或未指定的长度实际返回 510 字节的列。|  
|BYTE|即使 Microsoft 访问号码字段与等于字节字段大小未签名，负数可以插入到的字段中，使用 Microsoft Access 驱动程序时。|  
|CHAR、 LONGVARCHAR 和 VARCHAR|字符的字符串文本可以包含任何 ANSI 字符 （1-255 个十进制）。 使用两个连续单引号 （'） 来表示一个单引号 （'）。<br /><br /> 过程应该用于使用字符数据类型列中的任何特殊字符时，将传递字符数据。|  
|DATE|必须根据 ODBC 规范的日期格式分隔或由日期时间分隔符 （"#"） 分隔日期值。 否则为 Microsoft Access 会将值视为算术表达式，并且不会引发警告或错误。<br /><br /> 例如，日期"1996 年 3 月 5 日"必须表示为 {d ' 1996年-03-05} 或 #03/05/1996年 #;否则，如果仅提交 03/05/1993年，Microsoft Access 计算此如 3 除以 5 除以 1996年。 此值将向上舍入为整数 0，，和零天将映射到 1899年-12-31，因为这是使用的日期。<br /><br /> 管道字符 (&#124;) 不能在一个日期值，即使括在返回引号。|  
|GUID|限制为 Microsoft 访问 4.0 的数据类型。|  
|NUMERIC|限制为 Microsoft 访问 4.0 的数据类型。|  
  
 了解更多限制对数据类型可在[数据类型限制](../../odbc/microsoft/data-type-limitations.md)。
