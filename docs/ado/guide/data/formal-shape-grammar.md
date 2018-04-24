---
title: 正式形状语法 |Microsoft 文档
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO], shape grammar
- data shaping [ADO], shape grammar
ms.assetid: ea691475-0f03-4abe-a785-b77e77712d1d
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0273d30952b35a4796e65cf0138d449a9f04185c
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="formal-shape-grammar"></a>正式形状语法
这是用于创建任何形状的命令的正式语法：  
  
-   所需语法的条款是由命令的尖括号 ("<>") 分隔的文本字符串。  
  
-   可选条款由方括号 ("[]") 分隔。  
  
-   替代项以竖线 ("&#124;")。  
  
-   重复的替代项由省略号 （"..."）。  
  
-   *Alpha*指示按字母顺序排列的字母的字符串。  
  
-   *数字*指示数字的字符串。  
  
-   *Unicode 数字*指示 unicode 数字的字符串。  
  
 所有其他条款是文本。  
  
|术语|定义|  
|----------|----------------|  
|\<shape-command>|SHAPE [\<table-exp> [[AS] \<alias>]][\<shape-action>]|  
|\<table-exp>|{\<提供程序命令文本 >}&#124;<br /><br /> (\<形状命令 >)&#124;<br /><br /> 表\<带引号名称 >&#124;<br /><br /> \<带引号名称 >|  
|\<shape-action>|追加\<别名字段列表 >&#124;<br /><br /> 计算\<别名字段列表 > [BY\<字段列表 >]|  
|\<aliased-field-list>|\<使用别名字段 > [， \<...别名字段 >]|  
|\<使用别名字段 >|\<field-exp> [[AS] \<alias>]|  
|\<field-exp>|(\<关系 exp >)&#124;<br /><br /> \<计算 exp >&#124;<br /><br /> \<聚合 exp >&#124;<br /><br /> \<new-exp>|  
|<relation_exp>|\<表 exp > [[AS]\<别名 >]<br /><br /> 建立关系\<关系条件列表 >|  
|\<relation-cond-list>|\<关系条件 > [，\<关系条件 >...]|  
|\<关系条件 >|\<字段名称 > 收件人\<子 ref >|  
|\<child-ref>|\<字段名称 >&#124;<br /><br /> 参数\<param ref >|  
|\<param-ref>|\<number>|  
|\<field-list>|\<字段名称 > [，\<字段名称 >]|  
|\<aggregate-exp>|SUM (\<限定字段名称 >)&#124;<br /><br /> AVG (\<限定字段名称 >)&#124;<br /><br /> 最小值 (\<限定字段名称 >)&#124;<br /><br /> 最大 (\<限定字段名称 >)&#124;<br /><br /> 计数 (\<限定别名 > &#124; \<限定名称 >)&#124;<br /><br /> STDEV (\<限定字段名称 >)&#124;<br /><br /> 任何 (\<限定字段名称 >)|  
|\<calculated-exp>|CALC(\<expression>)|  
|\<qualified-field-name>|\<alias>.[\<alias>...]\<field-name>|  
|\<别名 >|\<带引号名称 >|  
|\<field-name>|\<带引号名称 > [[AS]\<别名 >]|  
|\<带引号名称 >|"\<string>" &#124;<br /><br /> \<字符串 >&#124;<br /><br /> [\<string>] &#124;<br /><br /> \<名称 >|  
|\<qualified-name>|alias[.alias...]|  
|\<名称 >|alpha [字母&#124;数字&#124;_ &#124; # &#124; : &#124; ...]|  
|\<number>|数字 [...数字]|  
|\<new-exp>|新\<字段类型 > [(\<数 > [，\<数 >])]|  
|\<field-type>|OLE DB 或 ADO 数据类型。|  
|\<string>|unicode char [unicode char...]|  
|\<expression>|Visual Basic 应用程序表达式其操作数都是同一行中的其他非计算列。|  
  
## <a name="see-also"></a>另请参阅  
 [访问在分层记录集中的行](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)   
 [数据调整概述](../../../ado/guide/data/data-shaping-overview.md)   
 [所需的提供程序，供你调整数据](../../../ado/guide/data/required-providers-for-data-shaping.md)   
 [形状 APPEND 子句](../../../ado/guide/data/shape-append-clause.md)   
 [在常规的形状命令](../../../ado/guide/data/shape-commands-in-general.md)   
 [形状 COMPUTE 子句](../../../ado/guide/data/shape-compute-clause.md)   
 [Visual Basic for Applications 函数](../../../ado/guide/data/visual-basic-for-applications-functions.md)
