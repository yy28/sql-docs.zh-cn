---
title: 字符串函数 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], string functions
- string functions [ODBC]
ms.assetid: 270f669e-8aab-4db0-95a4-f2b3c69538b3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d9323809028ad170a4811b1af8b6e276cdbb4293
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302838"
---
# <a name="string-functions"></a>字符串函数
下表列出了字符串操作函数。 应用程序可以通过使用*SQL_STRING_FUNCTIONS的信息类型*调用**SQLGetInfo**来确定驱动程序支持哪些字符串函数。  
  
## <a name="remarks"></a>备注  
 表示为*string_exp*的参数可以是列的名称、*字符串文本*的名称或其他标量函数的结果，其中基础数据类型可以表示为SQL_CHAR、SQL_VARCHAR或SQL_LONGVARCHAR。  
  
 表示为*character_exp*的参数是可变长度字符串。  
  
 表示为*起始*、*长度*或*计数*的参数可以是*数字文本*或另一个标量函数的结果，其中基础数据类型可以表示为SQL_TINYINT、SQL_SMALLINT 或SQL_INTEGER。  
  
 此处列出的字符串函数基于 1;也就是说，字符串中的第一个字符是字符 1。  
  
 在 ODBC 3.0 中添加了BIT_LENGTH、CHAR_LENGTH、CHARACTER_LENGTH、OCTET_LENGTH 和位置字符串标量函数，以便与 SQL-92 对齐。  
  
|函数|说明|  
|--------------|-----------------|  
|**ASCII（** _string_exp_ **）** （ODBC 1.0）|将*string_exp*最左侧字符的 ASCII 代码值作为整数返回。|  
|**BIT_LENGTH（string_exp** _string_exp_ **）** （ODBC 3.0）|返回字符串表达式的长度（以位为单位）。<br /><br /> 不仅适用于字符串数据类型，因此不会隐式地将*string_exp*转换为字符串，而是返回它所提供的任何数据类型的（内部）大小。|  
|**CHAR（**_代码_ **）（ODBC** 1.0）|返回具有*代码*指定的 ASCII 代码值的字符。 代码的值应介于 0 和 255 之间;*代码*的值应介于 0 和 255 之间。否则，返回值与数据源相关。|  
|**CHAR_LENGTH（** _string_exp_ **）** （ODBC 3.0）|如果字符串表达式是字符数据类型，则返回字符串表达式的长度。否则，返回字符串表达式的长度（最小整数不小于除以 8 的位数）。 （此函数与CHARACTER_LENGTH函数相同。|  
|**CHARACTER_LENGTH（string_exp** _string_exp_ **）** （ODBC 3.0）|如果字符串表达式是字符数据类型，则返回字符串表达式的长度。否则，返回字符串表达式的长度（最小整数不小于除以 8 的位数）。 （此函数与CHAR_LENGTH函数相同。|  
|**CONCAT（string_exp1，string_exp2）** _string_exp1_（ODBC 1.0）_string_exp2_**)**|返回将*string_exp2*串联到*string_exp1*的结果的字符串。 生成的字符串依赖于 DBMS。 例如，如果由*string_exp1*表示的列包含 NULL 值，DB2 将返回 NULL，但 SQL Server 将返回非 NULL 字符串。|  
|**差异**_（string_exp1，string_exp2__string_exp2_**）** （ODBC 2.0）|返回一个整数值，指示 SOUNDEX 函数为*string_exp1*和*string_exp2*返回的值之间的差异。|  
|**插入**_（string_exp1，_*开始*，*长度*， _string_exp2_**）** （ODBC 1.0）|返回一个字符串，其中*长度*字符从*string_exp1（**从开始）* 开始删除，*并且从**开始*将string_exp2插入到*string_exp中*。|  
|**LCASE（** _string_exp_ **）** （ODBC 1.0）|返回一个等于*string_exp*中的字符串，所有大写字符都转换为小写。|  
|**左（string_exp** _string_exp_，_计数_**）** （ODBC 1.0）|返回*string_exp*的最*左侧计数*字符。|  
|**长度（string_exp** _string_exp_ **）（ODBC** 1.0）|返回string_exp中的字符数 *，* 不包括尾随空格。<br /><br /> **长度**仅接受字符串。 因此，将隐式*string_exp*转换为字符串，并返回此字符串的长度（而不是数据类型的内部大小）。|  
|**位置（string_exp1** _string_exp1_ *，string_exp2*[，*开始***]** （ODBC 1.0）|返回*string_exp2**中第*一次string_exp1的起始位置。 除非指定了可选参数*start*，否则string_exp1的第一次出现*string_exp1的搜索*从*string_exp2*中的第一个字符位置开始。 如果指定*了"开始"，* 则搜索以起始值指示的字符位置*开始*。 *string_exp2*中的第一个字符位置由值 1 指示。 如果在*string_exp2*内找不到*string_exp1，* 则返回值 0。<br /><br /> 如果应用程序可以使用*string_exp1* *、string_exp2*调用 LOCATE 标量函数和*启动*参数调用，则当使用 SQL_STRING_FUNCTIONS*选项*调用**SQLGetInfo**时，驱动程序将返回SQL_FN_STR_LOCATE。 如果应用程序只能使用*string_exp1*和*string_exp2*参数调用 LOCATE 标量函数，则当使用 SQL_STRING_FUNCTIONS*选项*调用**SQLGetInfo**时，驱动程序将返回SQL_FN_STR_LOCATE_2。 支持使用两个或三个参数调用 LOCATE 函数的驱动程序返回SQL_FN_STR_LOCATE和SQL_FN_STR_LOCATE_2。|  
|**LTRIM（** _string_exp_ **）** （ODBC 1.0）|返回*string_exp*的字符，删除前导空格。|  
|**OCTET_LENGTH（string_exp** _string_exp_ **）** （ODBC 3.0）|返回字符串表达式的长度（以字节为单位）。 结果为不小于位数除以 8 所得数的最小整数。<br /><br /> 不仅适用于字符串数据类型，因此不会隐式地将*string_exp*转换为字符串，而是返回它所提供的任何数据类型的（内部）大小。|  
|**位置**_（character_expcharacter_exp_ **IN** _character_exp_**）** （ODBC 3.0）|返回第二个字符表达式中第一个字符表达式的位置。 结果是一个精确数值，实现定义的精度和比例为 0。|  
|**重复**_（string_exp，__计数_**）（ODBC** 1.0）|返回由*重复**计数*string_exp组成的字符串。|  
|**替换**_string_exp1_（string_exp1、string_exp2、string_exp3） （ODBC 1.0） _string_exp3_**)** *string_exp2*|搜索*string_exp1string_exp2**发生，* 然后替换为*string_exp3。*|  
|**右侧（string_exp** _string_exp_，_计数_**）** （ODBC 1.0）|返回*string_exp*的最右侧*计数*字符。|  
|**RTRIM（** _string_exp_ **）** （ODBC 1.0）|返回删除尾随空格的*string_exp*字符。|  
|**声音（string_exp** _string_exp_ **）** （ODBC 2.0）|返回一个数据源相关字符串，表示*string_exp*中单词的声音。 例如，SQL Server 返回 4 位 SOUNDEX 代码;Oracle 返回每个单词的语音表示形式。|  
|**空间（**_计数_ **）（ODBC** 2.0）|返回由*计数*空间组成的字符串。|  
|**SUBSTRING（string_exp** _string_exp_，*开始*， 长度 **）** （ODBC 1.0）|返回从*string_exp*派生的字符串，从*长度*字符*的起始*符指定的字符位置开始。|  
|**UCASE（** _string_exp_ **）** （ODBC 1.0）|返回一个等于*string_exp*中的字符串，所有小写字符转换为大写。|
