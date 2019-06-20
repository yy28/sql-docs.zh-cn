---
title: 文本文件格式 （文本文件驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- delimited text lines
- fixed-width text files
- text format [ODBC]
- text file driver [ODBC], text format
ms.assetid: f53cd4b5-0721-4562-a90f-4c55e6030cb9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cd2bc95e6fe5468e88fc61dd8ed4adcd985ec052
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62633012"
---
# <a name="text-file-format-text-file-driver"></a>文本文件格式（文本文件驱动程序）
ODBC 文本驱动程序支持这两个分隔和固定宽度的文本文件。 文本文件包含可选的标头行和零个或多个文本行。  
  
 尽管标头行的文本文件中的其他行作为使用相同的格式，但 ODBC 文本驱动程序将标头行条目解释为列名称，不是数据。  
  
 带分隔符的文本行包含由分隔符分隔的一个或多个数据值： 逗号、 制表符或自定义分隔符。 在整个文件，必须使用相同的分隔符。 由它们之间没有数据行中的两个分隔符表示 null 数据值。 带分隔符的文本行中的字符字符串可以包含在双引号 ("")。 没有空格可以出现之前或之后带分隔符的值。  
  
 在架构中指定的固定宽度文本行中每个数据条目的宽度。 由空格表示 null 数据值。  
  
 表被限制为最多为 255 个字段。 字段名称限制为 64 个字符，并且字段宽度被限制为 32,766 个字符。 记录仅限于 65,000 个字节。  
  
 可以仅为单个用户打开一个文本文件。 不支持多个用户。  
  
 以下语法，为程序员编写定义 ODBC 文本驱动程序可以读取文本文件的格式：  
  
|格式|表示|  
|------------|--------------------|  
|非斜体|根据所示，必须输入的字符|  
|*italics*|在语法中其他位置定义的参数|  
|brackets ([])|可选项|  
|大括号 ({})|互相排斥的选项列表|  
|垂直条 (&#124;)|单独互斥选项|  
|省略号 （...）|可以重复的一个或多个时间的项|  
  
 将文本文件的格式为：  
  
```  
text-file ::=  
   [delimited-header-line] [delimited-text-line]... end-of-file |  
   [fixed-width-header-line] [fixed-width-text-line]... end-of-file  
delimited-header-line ::= delimited-text-line  
delimited-text-line ::=  
   blank-line |  
   delimited-data [delimiter delimited-data]... end-of-line  
fixed-width-header-line ::= fixed-width-text-line  
fixed-width-text-line ::=  
   blank-line |  
   fixed-width-data [fixed-width-data]... end-of-line  
end-of-file ::= <EOF>  
blank-line ::= end-of-line  
delimited-data ::= delimited-string | number | date | delimited-null  
fixed-width-data ::= fixed-width-string | number | date | fixed-width-null  
```  
  
> [!NOTE]  
>  Schema.ini 文件中指定的固定宽度的文本文件中每个列的宽度。  
  
```  
  
      end-of-line ::= <CR> | <LF> | <CR><LF>  
delimited-string ::= unquoted-string | quoted-stringunquoted-string ::= [character | digit] [character | digit | quote-character]...  
quoted-string ::=  
   quote-character  
   [character | digit | delimiter | end-of-line | embedded-quoted-string]...  
   quote-characterembedded-quoted-string ::=   quote-characterquote-character  
   [character | digit | delimiter | end-of-line]  
   quote-characterquote-characterfixed-width-string ::= [character | digit | delimiter | quote-character] ...  
character ::= any character except:  
   delimiterdigitend-of-fileend-of-linequote-characterdigit ::= 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9  
delimiter ::= , | <TAB> |   
custom-delimitercustom-delimiter ::= any character except:  
   end-of-fileend-of-linequote-character  
```  
  
> [!NOTE]  
>  Schema.ini 文件中指定自定义分隔的文本文件中的分隔符。  
  
```  
quote-character ::= "  
number ::= exact-number | approximate-number  
exact-number ::= [+ | -] {unsigned-integer[.unsigned-integer] |  
   unsigned-integer. |  
   .unsigned-integer}  
approximate-number ::= exact-number{e | E}[+ | -]unsigned-integer  
unsigned-integer ::= {digit}...  
date ::=  
   mm date-separator dd date-separator yy |  
   mmm date-separator dd date-separator yy |  
   dd date-separator mmm date-separator yy |  
   yyyy date-separator mm date-separator dd |  
   yyyy date-separator mmm date-separator dd  
mm ::= digit [digit]  
dd ::= digit [digit]  
yy ::= digit digit  
yyyy ::= digit digit digit digit  
mmm ::= Jan | Feb | Mar | Apr | May | Jun | Jul | Aug | Sep | Oct | Nov | Dec  
date-separator ::= - | / | .  
delimited-null ::=  
```  
  
> [!NOTE]  
>  对于带分隔符的文件，由两个分隔符之间没有数据表示为空。  
  
```  
fixed-width-null ::= <SPACE>...  
```  
  
> [!NOTE]  
>  对于固定宽度文件，由空格表示为空。
