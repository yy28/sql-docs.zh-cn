---
title: "文本文件格式 （文本文件驱动程序） |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- delimited text lines
- fixed-width text files
- text format [ODBC]
- text file driver [ODBC], text format
ms.assetid: f53cd4b5-0721-4562-a90f-4c55e6030cb9
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b7d111fee1ae82fc3dbb1fff3eec2dd9dff53465
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="text-file-format-text-file-driver"></a>文本文件格式 （文本文件驱动程序）
ODBC 文本驱动程序支持这两个分隔和固定宽度的文本文件。 文本文件由可选的标头行和零个或多个文本行组成。  
  
 标头行使用相同的格式，如其他行的文本文件中，尽管 ODBC 文本驱动程序将作为列名称，不是数据解释标头行条目。  
  
 带分隔符的文本行包含由分隔符分隔的一个或多个数据值： 逗号、 制表符或自定义分隔符。 在整个文件，必须使用相同的分隔符。 由它们之间没有数据行中的两个分隔符表示 null 数据值。 带分隔符的文本行中的字符字符串可以括在双引号 ("")。 之前或之后分隔的值，可以进行没有空白。  
  
 架构中指定了固定宽度的文本行中每个数据条目的宽度。 由空格表示 null 数据值。  
  
 表仅限于最多 255 个域。 字段名称限制为 64 个字符，并且字段宽度被限制为 32766 个字符。 记录仅限于 65000 字节。  
  
 可以只为单个用户打开一个文本文件。 不支持多个用户。  
  
 以下语法，为程序员，编写定义可由 ODBC 文本驱动程序读取的文本文件的格式：  
  
|“格式”|表示|  
|------------|--------------------|  
|非斜体|必须按所示方式输入的字符|  
|*斜体*|在语法中其他位置定义的自变量|  
|方括号 ([])|可选项|  
|大括号 （{}）|互相排斥的选项列表|  
|垂直图条 (&#124;)|单独互相排斥的选择|  
|省略号 （...）|一个或多个时间可以重复的项|  
  
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
>  为带分隔符的文件，NULL 不表示两个分隔符之间的任何数据。  
  
```  
fixed-width-null ::= <SPACE>...  
```  
  
> [!NOTE]  
>  对于固定宽度文件，由空格表示 null 值。
