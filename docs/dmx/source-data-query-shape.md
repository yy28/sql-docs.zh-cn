---
description: '&lt;源数据查询 &gt; -形状'
title: 形状 (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 16fff086514facbb8197d8d6f27b72b81f67c2e2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500766"
---
# <a name="ltsource-data-querygt---shape"></a>&lt;源数据查询 &gt; -形状
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  将多个数据源中的查询合并到一个层次结构表中（即具有嵌套表的表），该表将成为挖掘模型的事例表。  
  
 **SHAPE** [!INCLUDE[msCoName](../includes/msconame-md.md)] 数据访问组件 (MDAC) 软件开发工具包 (SDK) 中介绍了 SHAPE 命令的完整语法。  
  
## <a name="syntax"></a>语法  
  
```  
  
SHAPE {<primary query>}  
APPEND ({ <child table query> }   
     RELATE <primary column> TO <child column>)   
          AS <column table name>  
[  
     ({ <child table query> }   
     RELATE <primary column> TO <child column>)   
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
 子表中的列，用于根据主查询的结果来标识父行。  
  
 *列表名称*  
 在父表中为嵌套表新追加的列名。  
  
## <a name="remarks"></a>备注  
 必须按与父表和子表都相关的列对查询排序。  
  
## <a name="examples"></a>示例  
 您可以在 [INSERT INTO &#40;DMX&#41;](../dmx/insert-into-dmx.md) 语句中使用下面的示例来训练包含嵌套表的模型。 **SHAPE**语句中的两个表通过**OrderNumber**列相关。  
  
```  
SHAPE {  
    OPENQUERY([Adventure Works DW Multidimensional 2012],'SELECT OrderNumber  
    FROM vAssocSeqOrders ORDER BY OrderNumber')  
} APPEND (  
    {OPENQUERY([Adventure Works DW Multidimensional 2012],'SELECT OrderNumber, model FROM   
    dbo.vAssocSeqLineItems ORDER BY OrderNumber, Model')}  
  RELATE OrderNumber to OrderNumber)   
```  
  
## <a name="see-also"></a>另请参阅  
 [&#60;源数据查询&#62;](../dmx/source-data-query.md)   
 [数据挖掘扩展插件 &#40;DMX&#41; 数据定义语句](../dmx/dmx-statements-data-definition.md)   
 [数据挖掘扩展插件 &#40;DMX&#41; 数据操作语句](../dmx/dmx-statements-data-manipulation.md)   
 [数据挖掘扩展插件 (DMX) 语句引用](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
