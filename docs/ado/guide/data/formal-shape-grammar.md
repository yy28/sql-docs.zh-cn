---
title: 正式形状语法 |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: ce65f6961502a5bfe43278e4a29a11c4210d4af8
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82758253"
---
# <a name="formal-shape-grammar"></a>正式 Shape 语法
这是用于创建任何 shape 命令的正式语法：  
  
-   必需的语法术语是用尖括号（"<>"）分隔的文本字符串。  
  
-   可选字词由方括号（"[]"）分隔。  
  
-   替代项通过扭转（"&#124;"）来表示。  
  
-   重复的替代项用省略号（"..."）表示。  
  
-   *Alpha*表示字母数字的字符串。  
  
-   *数字*表示数字的字符串。  
  
-   *Unicode 数字*表示 unicode 数字的字符串。  
  
 所有其他字词均为文本。  
  
|术语|定义|  
|----------|----------------|  
|\<形状-命令>|SHAPE [ \< 表 exp> [[AS] \< alias>]] [ \< 形状-操作>]|  
|\<表-exp>|{ \< provider-command>} &#124;<br /><br /> （ \< 形状>） &#124;<br /><br /> \<引用的表-名称> &#124;<br /><br /> \<带引号的>|  
|\<形状-操作>|追加 \< 化名> &#124;<br /><br /> 计算 \< 别名字段列表> [按 \< 字段列表>]|  
|\<化名字段列表>|\<化名字段> [， \< 化名为字段 >]|  
|\<化名字段>|\<字段 exp> [[AS] \< 别名>]|  
|\<字段 exp>|（ \< 关系-exp>） &#124;<br /><br /> \<计算-exp> &#124;<br /><br /> \<聚合-exp> &#124;<br /><br /> \<新的-exp>|  
|<relation_exp>|\<表-exp> [[AS] \< alias>]<br /><br /> \<关系关系-列出>|  
|\<关系-列出>|\<关系-导线> [， \< 关系-导线> ...]|  
|\<关系-导线>|\<字段名> \< 对子引用>|  
|\<子引用>|\<字段名> &#124;<br /><br /> 参数参数 \< -引用>|  
|\<param-引用>|\<数字>|  
|\<字段列表>|\<字段名> [， \< 字段名>]|  
|\<聚合-exp>|SUM （ \< 限定域名>） &#124;<br /><br /> AVG （ \< 限定域名>） &#124;<br /><br /> 最小值（ \< 限定域名>） &#124;<br /><br /> 最大值（ \< 限定域名>） &#124;<br /><br /> 计数（ \< 限定别名> &#124; \< 限定名>） &#124;<br /><br /> STDEV （ \< 限定域名>） &#124;<br /><br /> ANY （ \< 限定域名>）|  
|\<计算-exp>|CALC （ \< expression>）|  
|\<限定域名>|\<别名>。[ \< alias> ...] \<字段名>|  
|\<别名>|\<带引号的>|  
|\<字段名>|\<带引号> [[AS] \< alias>]|  
|\<带引号的>|" \< string>" &#124;<br /><br /> " \< string>" &#124;<br /><br /> [ \< 字符串>] &#124;<br /><br /> \<名称>|  
|\<限定名>|alias [alias ...]|  
|\<名称>|alpha [alpha &#124; 数字 &#124; _ &#124; # &#124;： &#124; ...]|  
|\<数字>|数字 [数字 ...]|  
|\<新的-exp>|新 \< 字段类型> [（ \< number> [， \< number>]）]|  
|\<字段类型>|OLE DB 或 ADO 数据类型。|  
|\<字符串>|unicode-char [unicode-char ...]|  
|\<expression>|一个 Visual Basic for Applications 表达式，其操作数为同一行中的其他非计算列。|  
  
## <a name="see-also"></a>另请参阅  
 [访问分层记录集中的行](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)   
 [数据定形概述](../../../ado/guide/data/data-shaping-overview.md)   
 [数据整理所需的提供程序](../../../ado/guide/data/required-providers-for-data-shaping.md)   
 [Shape APPEND 子句](../../../ado/guide/data/shape-append-clause.md)   
 [整体形状命令](../../../ado/guide/data/shape-commands-in-general.md)   
 [Shape 计算子句](../../../ado/guide/data/shape-compute-clause.md)   
 [Visual Basic for Applications 函数](../../../ado/guide/data/visual-basic-for-applications-functions.md)
