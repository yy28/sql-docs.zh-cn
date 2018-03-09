---
title: "正式形状语法 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- shape commands [ADO], shape grammar
- data shaping [ADO], shape grammar
ms.assetid: ea691475-0f03-4abe-a785-b77e77712d1d
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f9eb99feba381701f7e590add3906cd0285b2720
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
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
|\<table-exp>|{\<provider-command-text>} &#124;<br /><br /> (\<形状命令 >) &#124;<br /><br /> 表\<带引号名称 > &#124;<br /><br /> \<quoted-name>|  
|\<shape-action>|追加\<别名字段列表 > &#124;<br /><br /> 计算\<别名字段列表 > [BY\<字段列表 >]|  
|\<aliased-field-list>|\<aliased-field> [, \<aliased-field...>]|  
|\<aliased-field>|\<field-exp> [[AS] \<alias>]|  
|\<field-exp>|(\<关系 exp >) &#124;<br /><br /> \<calculated-exp> &#124;<br /><br /> \<aggregate-exp> &#124;<br /><br /> \<new-exp>|  
|<relation_exp>|\<table-exp> [[AS] \<alias>]<br /><br /> RELATE \<relation-cond-list>|  
|\<relation-cond-list>|\<relation-cond> [, \<relation-cond>...]|  
|\<relation-cond>|\<field-name> TO \<child-ref>|  
|\<child-ref>|\<字段名称 > &#124;<br /><br /> PARAMETER \<param-ref>|  
|\<param-ref>|\<number>|  
|\<field-list>|\<field-name> [, \<field-name>]|  
|\<aggregate-exp>|SUM (\<限定字段名称 >) &#124;<br /><br /> AVG (\<限定字段名称 >) &#124;<br /><br /> 最小值 (\<限定字段名称 >) &#124;<br /><br /> 最大 (\<限定字段名称 >) &#124;<br /><br /> 计数 (\<限定别名 > &#124;\<限定名称 >) &#124;<br /><br /> STDEV(\<qualified-field-name>) &#124;<br /><br /> ANY(\<qualified-field-name>)|  
|\<calculated-exp>|CALC(\<expression>)|  
|\<qualified-field-name>|\<alias>.[\<alias>...]\<field-name>|  
|\<alias>|\<quoted-name>|  
|\<field-name>|\<带引号名称 > [[AS]\<别名 >]|  
|\<quoted-name>|"\<string>" &#124;<br /><br /> '\<string>' &#124;<br /><br /> [\<string>] &#124;<br /><br /> \<name>|  
|\<qualified-name>|alias[.alias...]|  
|\<name>|alpha [字母 &#124; 数字 &#124; _ &#124; # &#124;: &#124;...]|  
|\<number>|digit [digit...]|  
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
