---
title: "NavigationProperty 元素 (CSDLBI) |Microsoft 文档"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: a36b4d3b-6a6c-489b-8a46-2e6b925b568f
caps.latest.revision: "10"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 9bb3e255d24b989fa4d4e9217f16b7aacbbf0697
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="navigationproperty-element-csdlbi"></a>NavigationProperty 元素 (CSDLBI)
  NavigationProperty 元素是一种复杂类型，可扩展 CSDL 成员类型以便在商业智能数据模型中支持导航。  
  
> [!WARNING]  
>  此元素用于进行报告，您无法进行修改或控制。  
  
## <a name="elements-and-attributes"></a>元素和属性  
 下表列出了用于定义 NavigationProperty 元素的元素和属性。  
  
|名称|是否必需|Description|  
|----------|-----------------|-----------------|  
|CollectionCaption|“否”|用于引用一组导航属性实例的复数名称。<br /><br /> 如果忽略此属性，则使用基本 Member 的 Caption 属性。|  
  
## <a name="example"></a>示例  
 **表格**  
  
 以下示例说明了 CSDLBI 版本 1.1 中的一个导航属性，此属性描述表格模型中 Product SubCategory 表与 Product 表之间的关联。  
  
```  
  
<NavigationProperty   
    Name="Product_Sub_Category_ProductSubcategoryKey"      
    Relationship="Sandbox.Product_Product_Sub_Category_Product_Sub_Category_ProductSubcategoryKey"  
     FromRole="Product_ProductSubcategoryKey"   
    ToRole="Product_Sub_Category_ProductSubcategoryKey">  
<bi:NavigationProperty   
     ReferenceName="Product Sub-Category_ProductSubcategoryKey" />  
</NavigationProperty>  
```  
  
## <a name="example"></a>示例  
 **多维**  
  
 以下示例显示 CSDLBI 版本 1.1 中的一个导航属性，该属性描述 Contoso Operations 多维数据集中两个表之间的关系。 此关系在 Product Subcategory 表和 Bike Category 表之间建立关联。  
  
```  
  
<NavigationProperty   
     Name="BikeSubcategory_ProductSubcategoryKey"   
     Relationship="Sandbox.Bike_BikeSubcategory_BikeSubcategory_ProductSubcategoryKey"   
     FromRole="Bike_ProductSubcategoryKey"   
     ToRole="BikeSubcategory_ProductSubcategoryKey">  
   <bi:NavigationProperty />  
</NavigationProperty>  
```  
  
## <a name="see-also"></a>另请参阅  
 [了解表格对象模型在兼容性级别 1050年通过 1103](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)  
  
  
