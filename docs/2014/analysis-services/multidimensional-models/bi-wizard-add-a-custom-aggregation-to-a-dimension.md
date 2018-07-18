---
title: 向维度中添加自定义聚合 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- dimensions [Analysis Services], Business Intelligence enhancements
- Business Intelligence enhancements [Analysis Services], custom aggregations
- aggregations [Analysis Services], custom
- unary operators
- custom aggregations [Analysis Services]
ms.assetid: 3199a6c2-a06d-47b9-bd1c-604dbb085318
caps.latest.revision: 28
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8567e17759af61b151a3fc27c05df0ed1df49b63
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37243947"
---
# <a name="add-a-custom-aggregation-to-a-dimension"></a>向维度中添加自定义聚合
  在多维数据集或维度中添加自定义聚合增强功能，以使用其他一元运算符替换与维度成员关联的默认聚合。 这种增强功能指定维度表中定义父子层次结构中的成员汇总的一元运算符列。 一元运算符对父子层次结构中的父属性进行操作。  
  
> [!NOTE]  
>  自定义聚合仅可用于基于现有数据源的维度。 对于不使用数据源创建的维度，必须先运行架构生成向导创建数据源视图，然后再添加自定义聚合。  
  
 若要添加自定义聚合，请使用商业智能向导，并在 **“选择增强功能”** 页中选择 **“指定一元运算符”** 选项。 然后，该向导引导您完成两个步骤：选择要应用自定义聚合的维度和标识自定义聚合。  
  
> [!NOTE]  
>  在运行商业智能向导添加自定义聚合之前，请确保要增强的维度包含父子属性层次结构。 有关详细信息，请参阅[父-子层次结构](parent-child-dimension.md)。  
  
## <a name="selecting-a-dimension"></a>选择维度  
 在向导的第一个 **“指定一元运算符”** 页中，指定要应用自定义聚合的维度。 已添加到该选定维度中的自定义聚合将会使维度发生更改。 所有包含选定维度的多维数据集都将继承这些更改。  
  
## <a name="adding-custom-aggregation-unary-operator"></a>添加自定义聚合（一元运算符）  
 在第二个 **“指定一元运算符”** 页中，为自定义聚合指定所需的父属性，并为一元运算符指定维度表中的源列。 **父属性**列出了具有的属性及其`Usage`属性设置为`Parent`。 如果具有多个父属性，则选择对应于要使用的父子关系的父属性。 如果没有列出父属性，则维度不存在有效的父子层次结构。  
  
 在 **“源列”** 中，选择包含一元运算符的字符串列。 (该选择将设置`UnaryOperatorColumn`父特性的属性。)维度表还应具有指定一元汇总运算符的字符串列。 该列中的字符串值应包含有效的聚合运算符。 如果某行为空，则通常计算对应的成员。 如果列中的公式无效，则当检索使用成员的单元值时，会出现运行时错误。 有关详细信息，请参阅 [父子维度中的一元运算符](parent-child-dimension-attributes-unary-operators.md)。  
  
  
