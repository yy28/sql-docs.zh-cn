---
title: "配置属性层次结构的“(全部)”级别 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "“全部”成员"
  - "IsAggregatable 属性"
  - "最上层的 [Analysis Services]"
  - "“(全部)”级别"
  - "AttributeAllMemberName 属性"
  - "级别 [Analysis Services]"
  - "成员 [Analysis Services], 全部"
  - "AllMemberName 属性"
ms.assetid: 0cb35e6f-b10f-483d-b893-78f6ca3979fd
caps.latest.revision: 33
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# 配置属性层次结构的“(全部)”级别
  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中，“(全部)”级别是一个系统生成的可选级别。 该级别只包含一个成员，该成员的值是直接从属级别中所有成员值的聚合。 该成员称为“全部”成员。 该成员是系统生成的成员，在维度表中不包含该成员。 由于“(全部)”级别中的成员位于层次结构的顶层，因此成员的值是层次结构中所有成员值合并计算的聚合。 “全部”成员通常作为层次结构的默认成员。  
  
 属性层次结构中是否存在“(全部)”级别取决于特性的 **IsAggregatable** 属性设置，用户定义层次结构中是否存在“(全部)”级别取决于用户定义层次结构最顶层级别的特性的 **IsAggregatable** 属性。 如果将 **IsAggregatable** 属性设置为 **True**，则存在“(全部)”级别。 如果将 **IsAggregatable** 属性设置为 **False**，则层次结构中没有“(全部)”级别。  
  
## 建立最顶层级别  
 如果在层次结构中将某级别的源特性的 **IsAggregatable** 属性设置为 **False** ，则该级别上面的层次结构中不会出现可聚合级别。 不可聚合的级别必须是任意层次结构的最顶层级别，或者该级别上面的所有级别的源特性的 **IsAggregatable** 属性必须也设置为 **False**。  
  
## “全部”成员和“(全部)”级别  
 “(全部)”级别中的单个成员称为“全部”成员。 维度的 **AttributeAllMemberName** 属性指定维度中属性的“全部”成员的名称。 层次结构的 **AllMemberName** 属性指定层次结构的“全部”成员的名称。  
  
## 另请参阅  
 [定义默认成员](../../analysis-services/multidimensional-models/define-a-default-member.md)  
  
  