---
title: 文本文件格式（文本文件驱动程序） |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5801433e0180bb07cb2d09a59db2bb74be012cdf
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303088"
---
# <a name="text-file-format-text-file-driver"></a>文本文件格式（文本文件驱动程序）
ODBC 文本驱动程序支持带分隔符和固定宽度的文本文件。 文本文件由可选的标头行和零个或多个文本行组成。  
  
 尽管标题行使用与文本文件中其他行相同的格式，但 ODBC 文本驱动程序将标题行项解释为列名称，而不是数据。  
  
 分隔的文本行包含一个或多个以分隔符分隔的数据值：逗号、制表符或自定义分隔符。 必须在整个文件中使用相同的分隔符。 Null 数据值由行中没有数据的行中的两个分隔符表示。 带分隔符的文本行中的字符串可以用双引号（""）引起来。 分隔值前后不能出现空白。  
  
 在架构中指定固定宽度文本行中每个数据输入的宽度。 Null 数据值由空白表示。  
  
 表最多可以有255个字段。 字段名称限制为64个字符，并且字段宽度限制为32766个字符。 记录限制为65000个字节。  
  
 只能为单个用户打开文本文件。 不支持多个用户。  
  
 以下为程序员编写的语法定义了 ODBC 文本驱动程序可以读取的文本文件的格式：  
  
|格式|表示|  
|------------|--------------------|  
|非斜体|必须按如下所示输入的字符|  
|*效果*|语法中其他地方定义的参数|  
|方括号（[]）|可选项|  
|大括号{}（）|互斥选项的列表|  
|竖线（&#124;）|单独的互斥选项|  
|省略号 (...)|可以重复一次或多次的项|  
  
 文本文件的格式为：  
  
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
>  在 schema.ini 文件中指定固定宽度文本文件中每一列的宽度。  
  
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
>  在 schema.ini 文件中指定自定义分隔文本文件中的分隔符。  
  
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
>  对于带分隔符的文件，NULL 在两个分隔符之间不会有数据表示。  
  
```  
fixed-width-null ::= <SPACE>...  
```  
  
> [!NOTE]  
>  对于固定宽度的文件，空值由空格表示。
