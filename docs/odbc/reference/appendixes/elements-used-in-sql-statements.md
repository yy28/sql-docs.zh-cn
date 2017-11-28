---
title: "用于 SQL 语句中的元素 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL statements [ODBC], elements supported
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
ms.assetid: 85777525-1555-4731-8309-63a464c6b43a
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 955b214ef035bf957ecf68a2481d85fdf3ec7956
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="elements-used-in-sql-statements"></a>用于 SQL 语句中的元素
在前面列出的 SQL 语句中使用以下元素。  
  
## <a name="element"></a>元素  
 *基本表标识符*:: =*用户定义名称*  
  
 *基本表名*:: =*基本表标识符*  
  
 *布尔值因素*:: [NOT] =*布尔值主*  
  
 *布尔值主*:: = 比较*-谓词*&#124;(*搜索条件*)  
  
 *布尔值术语*:: =*布尔值因素*[AND*布尔值术语*]  
  
 *字符字符串文本*:: = ' {*字符*}...' (*字符*是驱动程序中的数据源的字符集中的任何字符。 若要在字符字符串文本中包含文本单引号字符 （"），使用两个文本的引号字符 ['']。)  
  
 *列标识符*:: =*用户定义名称*  
  
 *列名称*:: = [*表名*。]*列标识符*  
  
 *比较运算符*:: = < &#124; > &#124;\<= &#124; > = &#124; = &#124; <>  
  
 *比较谓词*:: =*表达式*比较运算符表达式  
  
 *数据类型*:: =*字符字符串类型*(*字符字符串类型*是为其 SQLGetTypeInfo 所返回的结果集的""DATA_TYPE""列是任一 SQL_CHAR 任何数据类型或 SQL_VARCHAR。）  
  
 *数字*:: = 0 &#124; 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9  
  
 *动态参数*:: =？  
  
 *表达式*:: = 术语 &#124; 表达式 {+ &#124; –} 术语  
  
 *因素*:: = [*+*&#124;*–*]*主*  
  
 *插入值*:: =  
  
 *动态参数*  
  
 &#124;*文本*  
  
 &#124;NULL  
  
 &#124;用户  
  
 *字母*:: =*写写字母 &#124; 上限小写字母*  
  
 *文本*:: =*字符字符串文本*  
  
 *写写字母*:: = &#124; b &#124; c &#124; &#124; e &#124; f &#124; &#124; h &#124; i &#124; j &#124; k &#124; l &#124; &#124; n &#124; &#124; p &#124; q &#124; r&#124;&#124;&#124;&#124;v &#124;&#124;x &#124;y &#124;z  
  
 *order by 子句*:: ORDER BY =*排序规范*[，*排序规范*]...  
  
 *主*:: =*列名称*  
  
 &#124;*动态参数*  
  
 &#124;*文本*  
  
 &#124;(*表达式*)  
  
 *搜索条件*:: =*布尔值术语*[或者*搜索条件*]  
  
 *选择列表*:: = \* &#124;*选择子列表*[，*选择子列表*]... (*选择列表*不能包含参数。)  
  
 *选择子列表*:: =*表达式*  
  
 *排序规范*:: = {*无符号整数 &#124; 列名称*} [*ASC &#124;DESC*]  
  
 *表标识符*:: =*用户定义名称*  
  
 *表名*:: =*表标识符*  
  
 *表引用*:: =*表名称*  
  
 *表引用列表*:: =*表引用*[，*表引用*]...  
  
 *术语*:: =*因素*&#124;*术语*{\*&#124;*/* }*因素*  
  
 *无符号整数*:: = {*数字*}  
  
 *上限小写字母*:: = *A &#124;B &#124;C &#124;D &#124;E &#124;F &#124;&#124;H &#124;我 &#124;J &#124;K &#124;L &#124;&#124;N &#124;&#124;P &#124;问： &#124;&#124;&#124;&#124;&#124;V &#124;&#124;X &#124;Y &#124;Z*  
  
 *用户定义名称*:: =*字母*[*数字*&#124;*字母*&#124;*_*]...
