---
title: "形状 (DMX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SHAPE
dev_langs:
- DMX
helpviewer_keywords:
- SHAPE statement
- multiple data sources
ms.assetid: b9526ec2-40bc-4bf5-b4e5-774f71075065
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: dcd4940769fc52852b1d48feb453f1393c754084
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="ltsource-data-querygt---shape"></a>&lt;源数据查询&gt;的形状
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  将多个数据源中的查询合并到一个层次结构表中（即具有嵌套表的表），该表将成为挖掘模型的事例表。  
  
 完整语法**形状**命令记录在[!INCLUDE[msCoName](../includes/msconame-md.md)]数据访问组件 (MDAC) 软件开发工具包 (SDK)。  
  
## <a name="syntax"></a>語法  
  
```  
  
SHAPE {<master query>}  
APPEND ({ <child table query> }   
     RELATE <master column> TO <child column>)   
          AS <column table name>  
[  
     ({ <child table query> }   
     RELATE <master column> TO <child column>)   
          AS < column table name>  
...  
]       
```  
  
## <a name="arguments"></a>参数  
 *主查询*  
 返回父表的查询。  
  
 *子表查询*  
 返回嵌套表的查询。  
  
 *主列*  
 父表中的列，用于标识来自子表查询结果的子行。  
  
 *子列*  
 子表中的列，用于标识来自主查询结果的父行。  
  
 *列的表名称*  
 在父表中为嵌套表新追加的列名。  
  
## <a name="remarks"></a>備註  
 必须按与父表和子表都相关的列对查询排序。  
  
## <a name="examples"></a>示例  
 你可以使用下面的示例中[INSERT INTO &#40; DMX &#41;](../dmx/insert-into-dmx.md)语句来训练某个模型包含嵌套的表。 中的两个表**形状**通过相关联的语句**OrderNumber**列。  
  
```  
SHAPE {  
    OPENQUERY([Adventure Works DW Multidimensional 2012],'SELECT OrderNumber  
    FROM vAssocSeqOrders ORDER BY OrderNumber')  
} APPEND (  
    {OPENQUERY([Adventure Works DW Multidimensional 2012],'SELECT OrderNumber, model FROM   
    dbo.vAssocSeqLineItems ORDER BY OrderNumber, Model')}  
  RELATE OrderNumber to OrderNumber)   
```  
  
## <a name="see-also"></a>另請參閱  
 [&#60; 源数据查询 &#62;](../dmx/source-data-query.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;数据定义语句](../dmx/dmx-statements-data-definition.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;数据操作语句](../dmx/dmx-statements-data-manipulation.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;语句引用](../dmx/data-mining-extensions-dmx-statements.md)  
  
  

