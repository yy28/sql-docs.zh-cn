---
title: TableBinding 数据类型 (ASSL) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- TableBinding Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- TableBinding
helpviewer_keywords:
- TableBinding data type
ms.assetid: 3195dca4-82bf-46b7-a31f-5383586e3573
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: d0790fe5d8567c8ab23e3aaf39430d46675dcbdc
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36138515"
---
# <a name="tablebinding-data-type-assl"></a>TableBinding 数据类型 (ASSL)
  定义一个派生数据类型，该类型表示与表的绑定。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<TableBinding>  
   <!-- The following elements extend TabularBinding -->  
   <DataSourceID>...</DataSourceID>  
   <DbTableName>...</DbTableName>  
   <DbSchemaName>...</DbSchemaName>  
</TableBinding>  
```  
  
## <a name="data-type-characteristics"></a>数据类型特征  
  
|特征|Description|  
|--------------------|-----------------|  
|基本数据类型|[TabularBinding](binding-data-type-assl.md)|  
|派生数据类型|InclusionThresholdSetting|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|InclusionThresholdSetting|  
|子元素|[DataSourceID](../properties/id-element-assl.md)， [DbSchemaName](../properties/name-element-assl.md)， [DbTableName](../properties/dbtablename-element-assl.md)|  
|派生元素|请参阅[绑定](binding-data-type-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 请注意，在筛选表达式中通过使用嵌套 select 语句引用其他表可能会影响某些数据源的性能。 但设计器可以通过在数据源视图中定义一个命名查询并引用该查询来完全控制 SQL 表达式。  
  
 为分区定义绑定的方法与数据源视图中的分区表的用法无关。  
  
 例如，假设有一个度量值组，其默认表为“Sales”，具有 Date、Product ID、Qty、Price 和 Amount（在数据源视图中进行计算）列。 分区“Sales97”可使用带有筛选器“Year(Sales.Date) = 97”的表“Sales97”。  
  
 有效查询为：  
  
```  
SELECT Date, Product ID, Qty, Price, Qty * Price AS Amount   
   FROM Sales97 As Sales  
   WHERE Year(Sales.Date) = 97  
```  
  
 即使计算表达式使用限定的表名（例如 Sales.Qty），该表达式也仍然适用。 这同样适用如果表已改为通过某些查询"选择..."将替换为 上面的 FROM 子句将变为"从 SELECT...As Sales”。  
  
 有关详细信息`Binding`类型，包括 Analysis Services 脚本语言 (ASSL) 类型的对象表`Binding`和的继承层次结构`Binding`类型，请参阅[绑定数据类型&#40;ASSL&#41;](binding-data-type-assl.md).  
  
 ASSL 中数据绑定的概述，请参阅[数据源和绑定&#40;SSAS 多维&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)。  
  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.TableBinding>。  
  
## <a name="see-also"></a>请参阅  
 [绑定数据类型&#40;ASSL&#41;](binding-data-type-assl.md)   
 [数据源和绑定&#40;SSAS 多维&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)   
 [Analysis Services 脚本语言 XML 数据类型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  