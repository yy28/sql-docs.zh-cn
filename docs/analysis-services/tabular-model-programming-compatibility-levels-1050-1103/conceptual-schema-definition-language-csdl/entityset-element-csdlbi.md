---
title: EntitySet 元素 (CSDLBI) |Microsoft 文档
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0a38bf011a6a98ca89b8b574323b522060ff4620
ms.sourcegitcommit: 1aedef909f91dc88dc741748f36eabce3a04b2b1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2018
---
# <a name="entityset-element-csdlbi"></a>EntitySet 元素 (CSDLBI)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  EntitySet 元素定义 CSDLBI 数据模型中特定类型的实体集合。  
  
 EntitySet 必须指定数据模型中包含的每种实体类型。 有关这些模型实体的信息是通过列出此类型的 Entity 元素的子实体指定的。 有关详细信息，请参阅 [EntityType 元素 (CSDLBI)](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/entitytype-element-csdlbi.md)。  
  
 诸如排序规则和语言等属性是在 EntityContainer（而非各个对象）的级别定义的。 但是，模型内的列和文本属性在其他语言中可能具有标题或翻译。  
  
## <a name="elements-and-attributes"></a>元素和属性  
 下表列出了用于定义 EntitySet 元素的元素和属性。  
  
|属性名称|是否必需|Description|  
|--------------------|-----------------|-----------------|  
|Caption|“否”|实体集的用户友好说明。|  
|CollectionCaption|“否”|一个包含实体的复数名称的字符串。|  
|ReferenceName|“否”|包含实体的未合并的完全限定名称。 在多维模型中，这对应于 CubeDimension 名称。|  
|Hidden|“否”|指示该实体是否隐藏。 默认情况下不隐藏实体。|  
  
## <a name="example"></a>示例  
 **表格**  
  
 以下示例（在 CSDLBI 版本 1.1 中）显示 AdventureWorks 表格模型中的 Date 表和 Geography 表的定义。  
  
```  
  
<EntitySet   
   Name="Date"   
   EntityType="Sandbox. Date">  
<bi:EntitySet />  
</EntitySet>  
  
<EntitySet   
   Name="Geography"   
   EntityType="Sandbox.Geography">  
<bi:EntitySet />  
</EntitySet>  
```  
  
## <a name="example"></a>示例  
 **多维**  
  
 以下示例（在 CSDLBI 版本 1.1 中）显示来自 Contoso Retail Operations 多维数据集的若干 EntitySet 元素。  
  
```  
  
<EntitySet Name="Outage" EntityType="Sandbox.Outage">  
       <bi:EntitySet />  
</EntitySet>  
  
<EntitySet Name="Store" EntityType="Sandbox.Store">  
     <bi:EntitySet />  
</EntitySet>  
```  
  
## <a name="see-also"></a>另请参阅  
 [BI 批注的 CSDL 的技术参考](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/technical-reference-for-bi-annotations-to-csdl.md)  
  
  
