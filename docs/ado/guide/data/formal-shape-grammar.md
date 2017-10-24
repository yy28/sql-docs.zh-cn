---
title: "正式形状语法 |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- shape commands [ADO], shape grammar
- data shaping [ADO], shape grammar
ms.assetid: ea691475-0f03-4abe-a785-b77e77712d1d
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ae47b751e9e62d84188927186f186c6c9d344ce0
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

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
|\<形状命令 >|形状 [\<表 exp > [[AS]\<别名 >]] [\<形状操作 >]|  
|\<表 exp >|{\<提供程序命令文本 >} &#124;<br /><br /> (\<形状命令 >) &#124;<br /><br /> 表\<带引号名称 > &#124;<br /><br /> \<带引号名称 >|  
|\<形状操作 >|追加\<别名字段列表 > &#124;<br /><br /> 计算\<别名字段列表 > [BY\<字段列表 >]|  
|\<使用别名字段列表 >|\<使用别名字段 > [， \<...别名字段 >]|  
|\<使用别名字段 >|\<字段 exp > [[AS]\<别名 >]|  
|\<字段 exp >|(\<关系 exp >) &#124;<br /><br /> \<计算 exp > &#124;<br /><br /> \<聚合 exp > &#124;<br /><br /> \<新 exp >|  
|< relation_exp >|\<表 exp > [[AS]\<别名 >]<br /><br /> 建立关系\<关系条件列表 >|  
|\<关系条件列表 >|\<关系条件 > [，\<关系条件 >...]|  
|\<关系条件 >|\<字段名称 > 收件人\<子 ref >|  
|\<子 ref >|\<字段名称 > &#124;<br /><br /> 参数\<param ref >|  
|\<param ref >|\<数量 >|  
|\<字段列表 >|\<字段名称 > [，\<字段名称 >]|  
|\<聚合 exp >|SUM (\<限定字段名称 >) &#124;<br /><br /> AVG (\<限定字段名称 >) &#124;<br /><br /> 最小值 (\<限定字段名称 >) &#124;<br /><br /> 最大 (\<限定字段名称 >) &#124;<br /><br /> 计数 (\<限定别名 > &#124;\<限定名称 >) &#124;<br /><br /> STDEV (\<限定字段名称 >) &#124;<br /><br /> 任何 (\<限定字段名称 >)|  
|\<计算 exp >|CALC (\<表达式 >)|  
|\<限定字段名称 >|\<别名 >。[\<别名 >...]\<字段名称 >|  
|\<别名 >|\<带引号名称 >|  
|\<字段名称 >|\<带引号名称 > [[AS]\<别名 >]|  
|\<带引号名称 >|"\<字符串 >"&#124;<br /><br /> \<字符串 > &#124;<br /><br /> [\<字符串 >] &#124;<br /><br /> \<名称 >|  
|\<限定名称 >|别名 [.alias...]|  
|\<名称 >|alpha [字母 &#124; 数字 &#124; _ &#124; # &#124;: &#124;...]|  
|\<数量 >|数字 [...数字]|  
|\<新 exp >|新\<字段类型 > [(\<数 > [，\<数 >])]|  
|\<字段类型 >|OLE DB 或 ADO 数据类型。|  
|\<字符串 >|unicode char [unicode char...]|  
|\<表达式 >|Visual Basic 应用程序表达式其操作数都是同一行中的其他非计算列。|  
  
## <a name="see-also"></a>另请参阅  
 [访问在分层记录集中的行](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)   
 [数据调整概述](../../../ado/guide/data/data-shaping-overview.md)   
 [所需的提供程序，供你调整数据](../../../ado/guide/data/required-providers-for-data-shaping.md)   
 [形状 APPEND 子句](../../../ado/guide/data/shape-append-clause.md)   
 [在常规的形状命令](../../../ado/guide/data/shape-commands-in-general.md)   
 [形状 COMPUTE 子句](../../../ado/guide/data/shape-compute-clause.md)   
 [Visual Basic 应用程序函数](../../../ado/guide/data/visual-basic-for-applications-functions.md)

