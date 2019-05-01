---
title: 使用元组表达式 |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f5fae4c4351cc8e443523e54e2bc8b88f89ad098
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63251501"
---
# <a name="using-tuple-expressions"></a>使用元组表达式


  元组由多维数据集中包含的每个维度的一个成员组成。 因此，一个元组唯一标识多维数据集内的一个单元。  
  
> [!NOTE]  
>  引用一个或多个无效成员的元组称为“空元组”。  
  
 元组标识符的完整表达式由一个或多个用括号括起的显式指定的成员组成：  
  
 (*Member_expression* [，*Member_expression* ...])  
  
 元组可以是完全限定的，可以包含多个隐式成员，也可以只包含一个成员。  
  
## <a name="tuples-and-implicit-members"></a>元组和隐式成员  
 显式指定多维数据集内包含的每个维度的一个成员的元组称为“完全限定元组”。 但是，元组没有必要是完全限定的。  
  
 元组内没有显式引用的任何维度都被隐式引用。 隐式引用的维度的成员取决于维度的结构和在维度内定义的属性关系。 如果显式引用的层次结构所在的维度与隐式引用的层次结构所在的维度相同，并且显式引用的层次结构和隐式引用的层次结构之间定义了直接或间接关系，则元组的行为就好像它包含的隐式引用的层次结构上的成员与显式引用的层次结构上的成员一起存在。 例如，如果多维数据集包含具有“市县”和“国家(地区)”属性的“客户”维度，并且这两个属性之间定义了关系（即一个市县有一个国家（地区），一个国家（地区）可以包含多个市县），则在元组中显式包含市县“伦敦”将隐式引用国家（地区）“英国”。 但是，如果没有定义属性关系、关系的方向相反（例如，尽管“市县”与“国家(地区)”可能存在关系，但是您无法仅从某个人居住的国家（地区）来确定其居住的市县），或者定义的这两个属性之间没有直接关系（从“客户”到“市县”和从“客户”到“国家(地区)”可能定义了关系，但“市县”和“国家(地区)”之间没有定义关系），则以下规则适用：  
  
-   如果隐式引用的层次结构有默认成员，则将该默认成员添加到元组中。  
  
-   如果隐式引用的层次结构没有默认成员， **（全部）** 使用默认层次结构的成员。  
  
-   如果隐式引用的层次结构没有默认成员，则使用该层次结构最上层的第一个成员。  
  
## <a name="one-member-tuples"></a>一个成员的元组  
 如果元组表达式仅有一个成员，MDX 将把该成员转换为单成员元组，以计算该表达式。 换言之，使用成员表达式 `[Measures].[TestMeasure]`（而不是元组表达式）与使用元组表达式 `( [Measures].[TestMeasure] ).` 的效果相同。  
  
## <a name="see-also"></a>请参阅  
 [表达式&#40;MDX&#41;](../mdx/expressions-mdx.md)   
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
