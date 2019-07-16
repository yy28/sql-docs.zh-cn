---
title: 文本文件数据类型 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 829f924d8d4893d45a48c193cd27fdd7ac261e3d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67939715"
---
# <a name="text-file-data-types"></a>文本文件数据类型
下表显示了如何将文本数据类型映射到 ODBC SQL 数据类型。 请注意，并非所有 ODBC SQL 数据类型都支持 ODBC 文本驱动程序。  
  
|Text 数据类型|ODBC 数据类型|  
|--------------------|--------------------|  
|CHAR|SQL_VARCHAR|  
|DATETIME|SQL_TIMESTAMP|  
|FLOAT|SQL_DOUBLE|  
|整数|SQL_INTEGER|  
|LONGCHAR|SQL_LONGVARCHAR|  
  
> [!NOTE]  
>  **SQLGetTypeInfo**返回的 ODBC 数据类型。 所有转换中的附录 D *ODBC 程序员参考*上表中列出的 SQL 数据类型支持。  
  
 下表显示对文本数据类型的限制。  
  
|数据类型|描述|  
|---------------|-----------------|  
|CHAR|创建零对 CHAR 列或未指定的长度实际上返回一个 255 bit 列。<br /><br /> 在带分隔符的文件，CHAR 列可能会或可能没有双引号分隔符开头和结尾;在固定长度的文件，作为分隔符不使用双引号引起来。|  
|DATETIME|月-日-年 （例如，01-17-92）<br /><br /> MMM DD YY (例如，年 1 月-17-92)<br /><br /> DD-MMM-YY (例如，17 年 1 月 92)<br /><br /> 年-月-日 （例如，1992年-01-17）<br /><br /> 年-MMM-日 （例如，从 1992 年 1 月 17）<br /><br /> 在表中不允许混合的日期分隔符。<br /><br /> 文本 ISAM 格式取决于在 Windows 控制面板中的国际设置在美国或欧洲格式中，日期时间字段。|  
|FLOAT|最大宽度包括符号和小数点。 Schema.ini，宽度表示，如下所示：<br /><br /> 14.083 为 FLOAT 宽度 6<br /><br /> -14.083 是 FLOAT 宽度 7<br /><br /> +14.083 是 FLOAT 宽度 7<br /><br /> 14083。 是 FLOAT 宽度为 6<br /><br /> ODBC 始终返回 8 FLOAT 列。<br /><br /> FLOAT 列还可以采用科学记数法，例如：<br /><br /> -3.04E + 2 是 Float 宽度 8<br /><br /> 25E4 是 Float 宽度 4<br /><br /> **请注意**Decimal 和科学记数法表示法不能在列中。<br /><br /> NULL 值固定长度的文件，在空白填充的字符串表示，并且在带分隔符的文件中省略。<br /><br /> 可以使用前导空格填充的 float 数据。|  
|整数|对于整数列的有效值为介于-32766 到 32767。<br /><br /> Schema.ini，宽度表示，如下所示：<br /><br /> 14083 为整数宽度 5<br /><br /> 0 表示整数宽度 1<br /><br /> ODBC 始终返回 4 表示整数列。<br /><br /> 最大宽度包括一个符号。 一个整数列的最大宽度为 11，尽管宽度可能会由于固定格式的表中允许的空格更。|  
|LONGCHAR|理论上限制在 LONGCHAR 列的宽度固定长度或分隔的表为 65500 K。 文本 ISAM 是更倾向于提供最多大约 32k 可靠的支持。|  
  
 了解更多限制，对数据类型可在[数据类型限制](../../odbc/microsoft/data-type-limitations.md)。
