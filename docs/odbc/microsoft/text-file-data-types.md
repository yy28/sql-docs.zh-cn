---
title: 文本文件数据类型 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], data types
- ODBC desktop database drivers [ODBC], text file driver
- desktop database drivers [ODBC], text file driver
- text file data types [ODBC]
- Jet-based ODBC drivers [ODBC], text file driver
ms.assetid: e113112e-ae42-469e-8e4b-a365a10d9071
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 87707e3fe68c506d6774ffaa9aceb8ddc5a18223
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="text-file-data-types"></a>文本文件数据类型
下表显示如何将文本数据类型映射到 ODBC SQL 数据类型。 请注意，并非所有 ODBC SQL 数据类型都受 ODBC 文本驱动程序。  
  
|文本数据类型|ODBC 数据类型|  
|--------------------|--------------------|  
|CHAR|SQL_VARCHAR|  
|DATETIME|SQL_TIMESTAMP|  
|FLOAT|SQL_DOUBLE|  
|整数|SQL_INTEGER|  
|LONGCHAR|SQL_LONGVARCHAR|  
  
> [!NOTE]  
>  **SQLGetTypeInfo**返回 ODBC 数据类型。 附录 D 中的所有转换*ODBC 程序员参考*对上表中列出的 SQL 数据类型的支持。  
  
 下表显示对文本数据类型的限制。  
  
|数据类型|Description|  
|---------------|-----------------|  
|CHAR|创建零 CHAR 列或未指定的长度实际返回 255 位列。<br /><br /> CHAR 列可能或可能没有在起点和终点; 双引号分隔符分隔文件中在固定长度文件中，两个双引号不用作分隔符。|  
|DATETIME|MM-DD-YY （例如，01-17-92）<br /><br /> MMM DD YY (例如，年 1 月-17-92)<br /><br /> DD-MMM-YY (例如，17 年 1 月 92)<br /><br /> YYYY-月-日 （例如，1992年-01-17）<br /><br /> YYYY-MMM-日 （例如，1992 年 1 月 17）<br /><br /> 表中不允许混合的日期分隔符。<br /><br /> 文本 ISAM 格式具体 Windows 控制面板中的国际设置取决于在美国或欧洲格式中，DATETIME 字段。|  
|FLOAT|最大宽度包括的符号和小数点。 Schema.ini，宽度表示，如下所示：<br /><br /> 14.083 为 FLOAT 宽度 6<br /><br /> -14.083 为 FLOAT 宽度 7<br /><br /> +14.083 为 FLOAT 宽度 7<br /><br /> 14083。 为 FLOAT 宽度为 6<br /><br /> ODBC 始终返回 8 FLOAT 列。<br /><br /> FLOAT 列还可以采用科学记数法，例如：<br /><br /> -3.04E + 2 是 Float 宽度 8<br /><br /> 25E4 为 Float 宽度 4<br /><br /> **请注意**十进制和科学表示法不能混合在某一列。<br /><br /> NULL 值由固定长度文件中的空白填充字符串，并且在带分隔符的文件中省略。<br /><br /> 可以用前导空格填充浮点数据。|  
|整数|整数列的有效值是介于-32766 到 32767。<br /><br /> Schema.ini，宽度表示，如下所示：<br /><br /> 14083 为整数宽度 5<br /><br /> 0 表示整数宽度 1<br /><br /> ODBC 始终返回整数列的 4。<br /><br /> 最大宽度包括一个符号。 一个整数列的最大宽度是 11 中，但宽度可能会由于格式固定的表中允许的空白更高。|  
|LONGCHAR|理论上限制在 LONGCHAR 列的宽度固定长度或分隔的表为 65500 K。 文本 ISAM 是更倾向于提供最多约 32k 可靠的支持。|  
  
 了解更多限制对数据类型可在[数据类型限制](../../odbc/microsoft/data-type-limitations.md)。
