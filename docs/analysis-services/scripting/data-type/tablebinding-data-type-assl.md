---
title: "TableBinding 数据类型 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- TableBinding Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- TableBinding
helpviewer_keywords:
- TableBinding data type
ms.assetid: 3195dca4-82bf-46b7-a31f-5383586e3573
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 680587b7bd9154cf8f32ecbebe34e68c39e4c04a
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

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
  
|特征|说明|  
|--------------------|-----------------|  
|基本数据类型|[TabularBinding](../../../analysis-services/scripting/data-type/tabularbinding-data-type-assl.md)|  
|派生数据类型|无|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|无|  
|子元素|[DataSourceID](../../../analysis-services/scripting/properties/datasourceid-element-assl.md)， [DbSchemaName](../../../analysis-services/scripting/properties/dbschemaname-element-assl.md)， [DbTableName](../../../analysis-services/scripting/properties/dbtablename-element-assl.md)|  
|派生元素|请参阅[绑定](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)|  
  
## <a name="remarks"></a>注释  
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
  
 有关详细信息**绑定**类型，包括 Analysis Services 脚本语言 (ASSL) 类型的对象表**绑定**和的继承层次结构**绑定**类型，请参阅[绑定数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/binding-data-type-assl.md).  
  
 ASSL 中数据绑定的概述，请参阅[数据源和绑定 &#40;SSAS 多维 &#41;](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.TableBinding>。  
  
## <a name="see-also"></a>另请参阅  
 [绑定数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)   
 [数据源和绑定 &#40;SSAS 多维 &#41;](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)   
 [Analysis Services 脚本语言 XML 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  

