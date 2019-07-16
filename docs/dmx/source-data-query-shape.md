---
title: 形状 (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: c928d4c96917479f8c37415d5ebe2db9b7f9eb98
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67938117"
---
# <a name="ltsource-data-querygt---shape"></a>&lt;源数据查询&gt;-形状
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  将多个数据源中的查询合并到一个层次结构表中（即具有嵌套表的表），该表将成为挖掘模型的事例表。  
  
 完整语法**形状**命令记录在[!INCLUDE[msCoName](../includes/msconame-md.md)]数据访问组件 (MDAC) 软件开发工具包 (SDK)。  
  
## <a name="syntax"></a>语法  
  
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
  
## <a name="remarks"></a>备注  
 必须按与父表和子表都相关的列对查询排序。  
  
## <a name="examples"></a>示例  
 可以使用下面的示例中[INSERT INTO &#40;DMX&#41; ](../dmx/insert-into-dmx.md)语句来训练某个模型包含嵌套的表。 中的两个表**形状**通过相关语句**OrderNumber**列。  
  
```  
SHAPE {  
    OPENQUERY([Adventure Works DW Multidimensional 2012],'SELECT OrderNumber  
    FROM vAssocSeqOrders ORDER BY OrderNumber')  
} APPEND (  
    {OPENQUERY([Adventure Works DW Multidimensional 2012],'SELECT OrderNumber, model FROM   
    dbo.vAssocSeqLineItems ORDER BY OrderNumber, Model')}  
  RELATE OrderNumber to OrderNumber)   
```  
  
## <a name="see-also"></a>请参阅  
 [&#60;源数据查询&#62;](../dmx/source-data-query.md)   
 [数据挖掘扩展插件&#40;DMX&#41;数据定义语句](../dmx/dmx-statements-data-definition.md)   
 [数据挖掘扩展插件&#40;DMX&#41;数据操作语句](../dmx/dmx-statements-data-manipulation.md)   
 [数据挖掘扩展插件 (DMX) 语句引用](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
