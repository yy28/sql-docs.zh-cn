---
title: "EntityContainer 元素 (CSDLBI) |Microsoft 文档"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: e328558e-16b0-4d4a-a79a-fdd3c9493595
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: abb371783474c7a0580d5694e7ad2afeabce3a4c
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="entitycontainer-element-csdlbi"></a>EntityContainer 元素 (CSDLBI)
  EntityContainer 元素是一种复杂类型，它基于 CSDL 类型 EntityContainer，用于定义单个数据模型中的实体集合。 在商业智能应用程序中，EntityContainer 表示的数据模型可能包含多个其列按关系相互关联的表以及计算、度量值和 KPI。 它在概念上类似于数据库或数据源。  
  
 EntityContainer 必须指定数据模型中包含的每种实体类型，包括表和关系。 有关这些模型实体的信息是通过列出此类型的 Entity 元素的子实体指定的。 有关详细信息，请参阅 [EntityType 元素 (CSDLBI)](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/entitytype-element-csdlbi.md)。  
  
 诸如排序规则和语言等属性是在 EntityContainer（而非各个对象）的级别定义的。 但是，模型内的列和文本属性在其他语言中可能具有标题或翻译。  
  
## <a name="elements-and-attributes"></a>元素和属性  
 下表列出了用于定义 EntityContainer 的元素和属性。  
  
|名称|是否必需|Description|  
|----------|-----------------|-----------------|  
|名称|是|数据模型的名称。|  
|Caption|“否”|数据库或数据模型的说明。|  
|Culture|是|一个字符串，该字符串包含请求的 LCID。|  
|CompareOptions|是|模型的特定于语言的排序和字符串比较选项。|  
|DirectQueryMode|“否”|指示当模型正在使用 DirectQuery 模式时的查询模式的枚举。|  
|EntitySet 元素|是|[EntitySet 元素 &#40;CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/entityset-element-csdlbi.md)|  
|AssociationSet 元素|是|[AssociationSet 元素 &#40;CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/associationset-element-csdlbi.md)|  
  
## <a name="compareoptions-element"></a>CompareOptions 元素  
 CompareOptions 属性定义应用于数据模型的排序规则属性。 CompareOptions 定义的属性派生自在模型设计时在 Analysis Services 数据库中设置的排序顺序、区分假名和区分大小写的设置。 下表描述了作为 CompareOptions 属性的一部分包含的值。  
  
|“值”|Description|  
|-----------|-----------------|  
|IgnoreCase|指示字符串比较是否应忽略大小写的布尔值。|  
|IgnoreNonSpace|一个布尔值，指示字符串比较是否应忽略非空格组合字符（如标注字符）。|  
|IgnoreKanaType|指示字符串比较是否应忽略假名类型的布尔值。|  
|IgnoreWidth|指示字符串比较是否应忽略字符宽度的布尔值。|  
  
## <a name="directquerymode"></a>DirectQueryMode  
 **DirectQueryMode**  
  
 简单类型 DirectQueryMode 定义的是：当启用模型直接从关系数据源中检索数据时，默认情况下使用的查询类型。 此属性只适用于在 DirectQuery 模式下运行的表格模型。 下表列出了 DirectQuery 模式枚举的可能值。  
  
|“值”|Description|  
|-----------|-----------------|  
|InMemory|指示针对模型的查询将使用缓存中的数据。|  
|InMemoryWithDirectQuery|指示默认情况下，针对模型的查询将使用关系数据源中的数据。|  
|DirectQueryWithInMemory|指示默认情况下，针对模型的查询将使用缓存中的数据。|  
|DirectQuery|指示针对模型的查询将只使用关系数据源中的数据。|  
  
## <a name="example"></a>示例  
 **表格**  
  
 下面的示例（在 CSDLBI 版本 1.1 中）表示 AdventureWorks 表格数据模型的一部分。  
  
```  
  
<EntityContainer   
     Name="Sandbox">  
   <EntitySet   
       Name="DimEmployee"   
       EntityType="Sandbox.DimEmployee">  
   <bi:EntitySet />  
   </EntitySet>  
  
   <EntitySet   
     Name="DimProduct"   
       EntityType="Sandbox.DimProduct">  
    <bi:EntitySet />  
    </EntitySet>  
  
<bi:EntityContainer Caption="AWSimple" Culture="en-US">  
  
```  
  
## <a name="example"></a>示例  
 **多维**  
  
 下面的示例（在 CSDLBI 版本 1.1 中）是 Contoso Operations 多维数据集中的摘录。  
  
```  
  
<EntityContainer   
     Name="Sandbox">  
   <EntitySet   
      Name="Bike"   
      EntityType="Sandbox.Bike">  
    <bi:EntitySet Hidden="true" />  
   </EntitySet>  
…  
<bi:EntityContainer   
   Caption="CSDLTest"   
   Culture="en-US">  
<bi:CompareOptions   
   IgnoreCase="true" />  
</bi:EntityContainer>  
</EntityContainer>  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [EntitySet 元素 &#40;CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/entityset-element-csdlbi.md)  
  
  
