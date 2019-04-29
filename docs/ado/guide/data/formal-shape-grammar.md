---
title: 正式 Shape 语法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO], shape grammar
- data shaping [ADO], shape grammar
ms.assetid: ea691475-0f03-4abe-a785-b77e77712d1d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3b26eaeb804f8d92a7122814641cadf5889b77b8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63161419"
---
# <a name="formal-shape-grammar"></a>正式 Shape 语法
这是用于创建任何形状的命令的正式语法：  
  
-   所需语法的条款是用尖括号 ("<>") 分隔的文本字符串。  
  
-   可选的条款由方括号 ("[]") 分隔。  
  
-   替代项以竖线 ("&#124;")。  
  
-   通过省略号 （"..."） 指示重复的替代项。  
  
-   *Alpha*指示一串字母。  
  
-   *数字*指示数字字符串。  
  
-   *Unicode 数字*指示 unicode 数字的字符串。  
  
 所有其他字词是文本。  
  
|术语|定义|  
|----------|----------------|  
|\<shape-command>|SHAPE [\<table-exp> [[AS] \<alias>]][\<shape-action>]|  
|\<table-exp>|{\<provider-command-text>} &#124;<br /><br /> (\<shape-command>) &#124;<br /><br /> 表\<带引号的名称 >&#124;<br /><br /> \<quoted-name>|  
|\<shape-action>|APPEND \<aliased-field-list> &#124;<br /><br /> 计算\<别名字段列表 > [BY\<字段列表 >]|  
|\<aliased-field-list>|\<aliased-field> [, \<aliased-field...>]|  
|\<aliased-field>|\<field-exp> [[AS] \<alias>]|  
|\<field-exp>|(\<relation-exp>) &#124;<br /><br /> \<calculated-exp> &#124;<br /><br /> \<aggregate-exp> &#124;<br /><br /> \<new-exp>|  
|<relation_exp>|\<table-exp> [[AS] \<alias>]<br /><br /> 建立关系\<关系条件列表 >|  
|\<relation-cond-list>|\<relation-cond> [, \<relation-cond>...]|  
|\<relation-cond>|\<字段名称 > TO\<子 ref >|  
|\<child-ref>|\<field-name> &#124;<br /><br /> 参数\<param ref >|  
|\<param-ref>|\<number>|  
|\<field-list>|\<field-name> [, \<field-name>]|  
|\<aggregate-exp>|SUM(\<qualified-field-name>) &#124;<br /><br /> AVG(\<qualified-field-name>) &#124;<br /><br /> MIN(\<qualified-field-name>) &#124;<br /><br /> MAX(\<qualified-field-name>) &#124;<br /><br /> COUNT(\<qualified-alias> &#124; \<qualified-name>) &#124;<br /><br /> STDEV(\<qualified-field-name>) &#124;<br /><br /> ANY(\<qualified-field-name>)|  
|\<calculated-exp>|CALC(\<expression>)|  
|\<qualified-field-name>|\<alias>.[\<alias>...]\<field-name>|  
|\<alias>|\<quoted-name>|  
|\<field-name>|\<quoted-name> [[AS] \<alias>]|  
|\<quoted-name>|"\<string>" &#124;<br /><br /> '\<string>' &#124;<br /><br /> [\<string>] &#124;<br /><br /> \<name>|  
|\<qualified-name>|alias[.alias...]|  
|\<name>|alpha [ alpha &#124; digit &#124; _ &#124; # &#124; : &#124; ...]|  
|\<number>|digit [digit...]|  
|\<new-exp>|NEW \<field-type> [(\<number> [, \<number>])]|  
|\<field-type>|OLE DB 或 ADO 数据类型。|  
|\<string>|unicode char [unicode char...]|  
|\<expression>|Visual Basic 应用程序其操作数都是同一行中的其他非计算列的表达式。|  
  
## <a name="see-also"></a>请参阅  
 [访问分层记录集中的行](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)   
 [数据整理概述](../../../ado/guide/data/data-shaping-overview.md)   
 [数据整理所需的提供程序](../../../ado/guide/data/required-providers-for-data-shaping.md)   
 [Shape APPEND 子句](../../../ado/guide/data/shape-append-clause.md)   
 [常用 shape 命令](../../../ado/guide/data/shape-commands-in-general.md)   
 [Shape COMPUTE 子句](../../../ado/guide/data/shape-compute-clause.md)   
 [Visual Basic for Applications 函数](../../../ado/guide/data/visual-basic-for-applications-functions.md)
