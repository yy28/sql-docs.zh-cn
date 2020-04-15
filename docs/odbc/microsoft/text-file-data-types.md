---
title: 文本文件数据类型 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], data types
- ODBC desktop database drivers [ODBC], text file driver
- desktop database drivers [ODBC], text file driver
- text file data types [ODBC]
- Jet-based ODBC drivers [ODBC], text file driver
ms.assetid: e113112e-ae42-469e-8e4b-a365a10d9071
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7864dc81eaa3dd37f3d0053b2329c8842e445c8d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302655"
---
# <a name="text-file-data-types"></a>文本文件数据类型
下表显示了文本数据类型如何映射到 ODBC SQL 数据类型。 请注意，ODBC 文本驱动程序并非支持所有 ODBC SQL 数据类型。  
  
|文本数据类型|ODBC 数据类型|  
|--------------------|--------------------|  
|CHAR|SQL_VARCHAR|  
|DATETIME|SQL_TIMESTAMP|  
|FLOAT|SQL_DOUBLE|  
|INTEGER|SQL_INTEGER|  
|朗查尔|SQL_LONGVARCHAR|  
  
> [!NOTE]  
>  **SQLGetTypeInfo**返回 ODBC 数据类型。 对于上表中列出的 SQL 数据类型，支持*ODBC 程序员参考*附录 D 中的所有转换。  
  
 下表显示了对文本数据类型的限制。  
  
|数据类型|描述|  
|---------------|-----------------|  
|CHAR|创建零或未指定长度的 CHAR 列实际上返回 255 位列。<br /><br /> 在分隔文件中，CHAR 列在开头和结尾可能具有双引号分隔符，也可能没有双引号分隔符;在固定长度文件中，双引号不用作分隔符。|  
|DATETIME|MM-DD-YY（例如，01-17-92）<br /><br /> MMM-DD-YY（例如，1月17-92日）<br /><br /> DD-MMM-YY（例如，1月17日-92）<br /><br /> YYYY-MM-DD（例如，1992-01-17）<br /><br /> YYYY-MMM-DD（例如，1992年-1月-17日）<br /><br /> 不允许在表中混合日期分隔符。<br /><br /> "文本 ISAM"以美国或欧洲格式设置 DATETIME 字段，具体取决于 Windows 控制面板中的"国际"设置。|  
|FLOAT|最大宽度包括符号和小数点。 在 Schema.ini 中，宽度表示如下：<br /><br /> 14.083 是 FLOAT 宽度 6<br /><br /> -14.083 是 FLOAT 宽度 7<br /><br /> +14.083 是 FLOAT 宽度 7<br /><br /> 14083. 是 FLOAT 宽度 6<br /><br /> ODBC 始终为 FLOAT 列返回 8。<br /><br /> FLOAT 列也可以使用科学记数法，例如：<br /><br /> -3.04E+2 是浮动宽度 8<br /><br /> 25E4 是浮动宽度 4<br /><br /> **注意**十进制和科学记数法不能混合在列中。<br /><br /> NULL 值由固定长度文件中的空白填充字符串表示，并在分隔文件中省略。<br /><br /> 浮动数据可以使用前导空格填充。|  
|INTEGER|INTEGER 列的有效值为 32767 到 -32766。<br /><br /> 在 Schema.ini 中，宽度表示如下：<br /><br /> 14083 是 INTEGER 宽度 5<br /><br /> 0 是集成宽度 1<br /><br /> ODBC 始终为 INTEGER 列返回 4。<br /><br /> 最大宽度包括一个符号。 INTEGER 列的最大宽度为 11，尽管由于固定格式表中允许的空白，宽度可能更大。|  
|朗查尔|固定长度或分隔表中 LONGCHAR 列宽度的理论限制为 65500K。 文本 ISAM 更有可能提供高达 32K 的可靠支持。|  
  
 数据类型的更多限制可以在[数据类型限制](../../odbc/microsoft/data-type-limitations.md)中找到。
