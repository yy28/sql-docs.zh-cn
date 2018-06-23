---
title: Property 元素 (CSDLBI) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: f0770c5e-6420-4d0c-a5bf-b94eaf6877ca
caps.latest.revision: 7
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: a4d1ab0082c4b5475e0fc54127e7b80f63a9b983
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36026874"
---
# <a name="property-element-csdlbi"></a>Property 元素 (CSDLBI)
  CSDLBI 中的 Property 元素是一种复杂类型，它向 CSDL 中的 Property 元素提供附加内容，以便支持商业智能数据模型。  
  
## <a name="elements-and-attributes"></a>元素和属性  
 下表列出了用于定义 CSDLBI 的 Property 元素的元素和属性。  
  
|“属性”|是否必需|Description|  
|----------|-----------------|-----------------|  
|目录|“否”|一个字符串，该字符串包含请求的 LCID。|  
|DefaultAggregationFunction|是|一个字符串，当对属性执行计算且没有指定任何其他函数时，该字符串指定应使用的聚合函数。<br /><br /> 如果未指定，则使用模型的默认聚合，通常是 SUM。|  
|GroupingBehavior|“否”|指定如何对查询结果进行分组的值。 属性的内容由 TGroupingBehavior 简单类型定义（请参阅下面的表）。|  
|OrderBy|“否”|对模型内用于定义该属性值的排序顺序的其他属性的引用。<br /><br /> 这两个属性的值“应”具有 1 对 1 映射。 否则，未定义排序行为。<br /><br /> 如果忽略此元素，则基于属性的值对属性排序。|  
|稳定性|“否”|一个指定刷新操作之间的属性值的稳定性的特性。<br /><br /> 此属性不是由用户设置，而是由设计时环境仅针对不稳定的值发出。 它始终应用于包含行号的列以及所包含的公式生成不确定结果的列，如 NOW() 或 RAND()。<br /><br /> 此属性的值在下面用于说明 Stabilitysimple 类型的表中定义。|  
  
## <a name="groupingbehavior"></a>GroupingBehavior  
 下表列出 GroupingBehavior 简单类型的值。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|GroupOnValue|按属性的值分组。|  
|GroupOnEntityKey|按实体键分组。|  
  
 下面的示例阐述了这两个值的用法。 假设查询旨在返回特定用户（按名称指定）的工资扣减额。 假设数据库包含两个同名但具有不同数据库标识符的用户，则查询结果将不同，具体取决于将哪个属性值应用于此列：  
  
-   `GroupOnValue`：查询结果包含这两个用户的工资扣减额总计。  
  
-   `GroupOnEntityKey`：查询结果包含每个用户的工资扣减额，但单独列出。  
  
## <a name="stability"></a>稳定性  
 下表列出 `Stability` 简单类型的值。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|Stable|属性在刷新操作之间保持不变。|  
|RowNumber|属性包含行号。|  
|Volatile|属性在刷新操作之间可能不保持不变。|  
  
## <a name="example"></a>示例  
 **表格**  
  
 以下 XML 显示 AdventureWorks 表格模型示例中某些属性的 CSDLBI 版本 1.1 表示形式。  
  
```  
  
<EntityType   
   Name="DimEmployee">  
   <Key>  
      <PropertyRef   
      Name="RowNumber" />  
   </Key>  
  
   <Property   
      Name="RowNumber"   
      Type="Int64"   
      Nullable="false">  
   <bi:Property   
      Hidden="true"   
      Contents="RowNumber"   
      Stability="RowNumber" />  
   </Property>  
  
   <Property   
      Name="EmployeeKey"   
      Type="Int64">  
   <bi:Property />  
   </Property>  
….  
</bi:EntityType>  
</EntityType>  
  
```  
  
## <a name="example"></a>示例  
 **多维**  
  
 以下示例（在 CSDLBI 版本 1.1 中）显示数据模型中表示 Contoso Operations 多维数据集的列的某些属性。 请注意，对于大多数列，不要求也不应用 BI 注释，BI 注释只适用于那些要求在表示层进行特殊处理的列。  
  
```  
  
<EntityType   
   Name="Bike">  
  
   <Key>  
      <PropertyRef Name="RowNumber" />  
   </Key>  
  
   <Property   
      Name="RowNumber"   
      Type="Int64"   
      Nullable="false">  
   <bi:Property   
      Hidden="true"   
      Contents="RowNumber"   
      Stability="RowNumber"   
   />  
   </Property>  
  
   <Property   
      Name="ProductAlternateKey"   
      Type="String"   
      MaxLength="Max"   
      Unicode="true"   
      FixedLength="false">  
   <bi:Property />  
   </Property>  
  
```  
  
## <a name="see-also"></a>请参阅  
 [用于商业智能的 CSDL 注释技术参考](technical-reference-for-bi-annotations-to-csdl.md)  
  
  