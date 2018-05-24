---
title: 字符串函数 |Microsoft 文档
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
- functions [ODBC], string functions
- string functions [ODBC]
ms.assetid: 270f669e-8aab-4db0-95a4-f2b3c69538b3
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 03f783cbc287d9c315844e1a9df53187e4e2ba28
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="string-functions"></a>字符串函数
下表列出的字符串操作函数。 应用程序可以确定由驱动程序支持哪些字符串函数，应调用**SQLGetInfo**与*信息类型*SQL_STRING_FUNCTIONS。  
  
## <a name="remarks"></a>注释  
 自变量表示为*string_exp*可以是某一列的名称*字符字符串文本*，或另一个标量函数，其中基础数据类型可以表示为 SQL_CHAR，SQL_ 的结果VARCHAR、 或 SQL_LONGVARCHAR。  
  
 自变量表示为*character_exp*是长度可变字符字符串。  
  
 自变量表示为*启动*，*长度*，或*计数*可以是*数字文本*的另一个标量函数，或结果其中基础数据类型可以表示为 SQL_TINYINT、 SQL_SMALLINT 或 SQL_INTEGER。  
  
 此处列出的字符串函数都是基于 1 的;也就是说，在字符串中的第一个字符是字符 1。  
  
 已在 ODBC 3.0 为了符合 SQL 92 添加 BIT_LENGTH、 CHAR_LENGTH、 CHARACTER_LENGTH、 OCTET_LENGTH 和位置字符串标量函数。  
  
|函数|Description|  
|--------------|-----------------|  
|**ASCII (** *string_exp* **)** (ODBC 1.0)|返回的最左侧字符的 ASCII 代码值*string_exp*数值类型为整数。|  
|**BIT_LENGTH (** *string_exp* **)** (ODBC 3.0)|返回字符串表达式的长度（以位为单位）。<br /><br /> 不只对字符串数据类型不起作用，因此将不隐式转换*string_exp*字符串而是将返回它会获得任何数据类型 （内部） 大小。|  
|**CHAR (** *代码* **)** (ODBC 1.0)|返回具有 ASCII 字符的代码指定值*代码*。 值*代码*应为介于 0 和 255 之间; 否则，返回值为数据源而定。|  
|**CHAR_LENGTH (** *string_exp* **)** (ODBC 3.0)|以字符为单位的字符串表达式，返回的长度，如果字符串表达式的字符数据类型;否则，返回的长度以字节为单位的字符串表达式 （的最小整数不小于除以 8 的比特数）。 （此函数是 CHARACTER_LENGTH 函数相同。）|  
|**CHARACTER_LENGTH (** *string_exp* **)** (ODBC 3.0)|以字符为单位的字符串表达式，返回的长度，如果字符串表达式的字符数据类型;否则，返回的长度以字节为单位的字符串表达式 （的最小整数不小于除以 8 的比特数）。 （此函数是 CHAR_LENGTH 函数相同。）|  
|**CONCAT (** *string_exp1*，*string_exp2 * * *)** (ODBC 1.0)|返回字符串的串联结果*string_exp2*到*string_exp1*。 生成的字符串依赖于 DBMS。 例如，如果列由*string_exp1*包含 NULL 值，则 DB2 将返回 NULL 但 SQL Server 将返回非 NULL 字符串。|  
|**差异 (** *string_exp1*，*string_exp2 * * *)** (ODBC 2.0)|返回一个整数值，该值指示的 SOUNDEX 函数返回的值之间的差异*string_exp1*和*string_exp2*。|  
|**插入 (** *string_exp1*，*启动*，*长度*， *string_exp2 * * *)** (ODBC 1.0)|返回一个字符字符串位置*长度*从已删除字符*string_exp1*开始，*启动*，以及在何处*string_exp2*已插入到*string_exp，* 开始*启动*。|  
|**LCASE (** *string_exp* **)** (ODBC 1.0)|返回一个字符串等于，在*string_exp*，所有大写字符转换为小写字符。|  
|**左 (** *string_exp*，*计数 * * *)** (ODBC 1.0)|返回最左边*计数*字符*string_exp*。|  
|**长度 (** *string_exp* **)** (ODBC 1.0)|返回中的字符数*string_exp，* 不包括尾随空格。<br /><br /> **长度**仅接受字符串。 因此将隐式转换*string_exp*为字符串，然后返回此字符串 （不内部的数据类型大小） 的长度。|  
|**找到 (** *string_exp1*， *string_exp2*[，*启动*]**)** (ODBC 1.0)|返回的第一个匹配项的起始位置*string_exp1*内*string_exp2*。 第一个匹配项的搜索*string_exp1*开头的第一个字符位置在*string_exp2*除非可选参数，*启动*，指定。 如果*启动*的值指示的字符位置开始执行搜索的指定*启动*。 第一个字符置于*string_exp2*由值 1。 如果*string_exp1*中找不到*string_exp2*，返回值 0。<br /><br /> 如果应用程序可以调用具有的定位标量函数*string_exp1*， *string_exp2*，和*启动*自变量，该驱动程序返回 SQL_FN_STR_LOCATE 时**SQLGetInfo**使用调用*选项*SQL_STRING_FUNCTIONS。 如果应用程序可以调用具有唯一的定位标量函数*string_exp1*和*string_exp2*自变量，该驱动程序返回 SQL_FN_STR_LOCATE_2 时**SQLGetInfo**使用调用*选项*SQL_STRING_FUNCTIONS。 调用具有两个或三个参数的查找函数的支持返回 SQL_FN_STR_LOCATE 和 SQL_FN_STR_LOCATE_2 的驱动程序。|  
|**LTRIM (** *string_exp* **)** (ODBC 1.0)|返回的字符*string_exp*，用前导空白已删除。|  
|**OCTET_LENGTH (** *string_exp* **)** (ODBC 3.0)|返回字符串表达式的长度（以字节为单位）。 结果为不小于位数除以 8 所得数的最小整数。<br /><br /> 不只对字符串数据类型不起作用，因此将不隐式转换*string_exp*字符串而是将返回它会获得任何数据类型 （内部） 大小。|  
|**位置 (** *character_exp* **IN** *character_exp * * *)** (ODBC 3.0)|返回第二个的字符表达式中的第一个字符表达式的位置。 结果是精确数值与实现定义的精度和小数位数为 0。|  
|**重复 (** *string_exp，* *计数 * * *)** (ODBC 1.0)|返回字符字符串组成*string_exp*重复*计数*时间。|  
|**替换 (** *string_exp1*， *string_exp2*， *string_exp3 * * *)** (ODBC 1.0)|搜索*string_exp1*的 foroccurrences *string_exp2*，并将替换*string_exp3*。|  
|**右 (** *string_exp*，*计数 * * *)** (ODBC 1.0)|返回最右边*计数*字符*string_exp*。|  
|**RTRIM (** *string_exp* **)** (ODBC 1.0)|返回的字符*string_exp*尾随空白已删除。|  
|**SOUNDEX (** *string_exp* **)** (ODBC 2.0)|返回一个表示中单词的声音的数据源 – 相关的字符字符串*string_exp*。 例如，SQL Server 返回 4 位数字的 SOUNDEX 代码;Oracle 返回每个单词的拼音表示。|  
|**空间 (** *计数* **)** (ODBC 2.0)|返回一个包含的字符字符串*计数*空格。|  
|**子字符串 (** *string_exp*，*启动*，长度 **)** (ODBC 1.0)|返回派生自的字符字符串*string_exp*中由指定的字符位置开始，*启动*为*长度*字符。|  
|**UCASE (** *string_exp* **)** (ODBC 1.0)|返回一个字符串等于，在*string_exp*，所有小写字符转换为大写形式。|
