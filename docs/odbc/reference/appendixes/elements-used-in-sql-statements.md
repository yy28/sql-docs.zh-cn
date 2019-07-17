---
title: 在 SQL 语句中使用的元素 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], elements supported
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
ms.assetid: 85777525-1555-4731-8309-63a464c6b43a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: caf8f68221c1ac14649bf10be0105e1e691c7482
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68129960"
---
# <a name="elements-used-in-sql-statements"></a>SQL 语句中使用的元素
在前面列出的 SQL 语句中使用以下元素。  
  
## <a name="element"></a>元素  
 *base-table-identifier* ::= *user-defined-name*  
  
 *base-table-name* ::= *base-table-identifier*  
  
 *一个布尔值身份*:: [NOT] =*主数据库的布尔值*  
  
 *boolean-primary* ::= comparison *-predicate* &#124; ( *search-condition* )  
  
 *一个布尔值术语*:: =*布尔值身份*[AND*布尔值术语*]  
  
 *character-string-literal* ::= ''{*character*}...'' (*字符*是驱动程序/数据源的字符集中的任何字符。 若要在字符字符串文本中包含文本的单引号字符 （"），使用两个文本引号字符 ['']。)  
  
 *列标识符*:: =*用户定义名称*  
  
 *列名称*:: = [*表名称*。]*列标识符*  
  
 *comparison-operator* ::= < &#124; > &#124; \<= &#124; >= &#124; = &#124; <>  
  
 *比较谓词*:: =*表达式*比较运算符表达式  
  
 *数据类型*:: =*字符字符串类型*(*字符字符串类型*是 SQLGetTypeInfo 返回的结果集中的""DATA_TYPE""列了任一 SQL_CHAR 的任何数据类型或SQL_VARCHAR。)  
  
 *digit* ::= 0 &#124; 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9  
  
 *dynamic-parameter* ::= ?  
  
 *expression* ::= term &#124; expression {+&#124;-} term  
  
 *factor* ::= [ *+* &#124; *-* ]*primary*  
  
 *insert-value* ::=  
  
 *dynamic-parameter*  
  
 &#124;*文本*  
  
 &#124; NULL  
  
 &#124; USER  
  
 *字母*:: =*写写字母&#124;上限大小写字母*  
  
 *literal* ::= *character-string-literal*  
  
 *写写字母*:: = &#124; b &#124; c &#124; d &#124; e &#124; f &#124; g &#124; h &#124; i &#124; j &#124; k &#124; l &#124; m &#124; n &#124; o &#124; p &#124; q &#124; r&#124; s &#124; t &#124; u &#124; v &#124; w &#124; x &#124; y &#124; z  
  
 *order by 子句*:: = ORDER BY*排序规范*[，*排序规范*]...  
  
 *主*:: =*列名称*  
  
 &#124; *dynamic-parameter*  
  
 &#124;*文本*  
  
 &#124; ( *expression* )  
  
 *搜索条件*:: =*布尔值术语*[或者*搜索条件*]  
  
 *选择列表*:: = \* &#124; *选择子列表*[，*选择子列表*]... (*选择列表*不能包含参数。)  
  
 *select-sublist* ::= *expression*  
  
 *排序规范*:: = {*无符号整数&#124;列名称*} [*ASC &#124; DESC*]  
  
 *table-identifier* ::= *user-defined-name*  
  
 *table-name* ::= *table-identifier*  
  
 *table-reference* ::= *table-name*  
  
 *table-reference-list* ::= *table-reference* [,*table-reference*]...  
  
 *term* ::= *factor* &#124; *term* {\*&#124; */* } *factor*  
  
 *无符号整数*:: = {*数字*}  
  
 *上限大小写字母*:: = *A &#124; B &#124; C &#124; D &#124; E &#124; F &#124; G&#124;小时&#124;我&#124;J &#124; K &#124; L &#124; M &#124; N &#124; O &#124; &#124;Q &#124; R &#124; S &#124; T &#124; U &#124; V &#124; W &#124; X &#124; Y &#124; Z*  
  
 *user-defined-name* ::= *letter*[*digit* &#124; *letter* &#124; *_* ]...
