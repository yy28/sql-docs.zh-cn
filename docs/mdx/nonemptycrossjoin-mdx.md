---
title: "NonEmptyCrossjoin (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: NONEMPTYCROSSJOIN
dev_langs: kbMDX
helpviewer_keywords: NonEmptyCrossjoin function
ms.assetid: 3dc9522d-9126-4f7a-b587-216fa7a06c62
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: dcc37d637de69f912fd3a9c6e51c3e0a55e01a1a
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="nonemptycrossjoin-mdx"></a>NonEmptyCrossjoin (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回包含一个或多个集的叉积的集，不包括空元组以及无相关事实数据表数据的元组。  
  
## <a name="syntax"></a>语法  
  
```  
  
NonEmptyCrossjoin(Set_Expression1 [ ,Set_Expression2,...] [,Count ] )  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression1*  
 返回集的有效多维表达式 (MDX)。  
  
 *Set_Expression2*  
 返回集的有效多维表达式 (MDX)。  
  
 *计数*  
 指定返回集的数量的有效数值表达式。  
  
## <a name="remarks"></a>注释  
 **NonEmptyCrossjoin**函数集，而无需提供的基础事实数据表的数据中排除空元组或元组的形式返回两个或多个集的叉积。 由于如何**NonEmptyCrossjoin**函数工作原理，所有计算成员将自动排除。  
  
 如果*计数*未指定，跨函数联接所有指定的集，并将空成员排除在结果集。 如果指定了集的数量，该函数将从第一个指定的集开始，交叉联接指定数量的集。 **NonEmptyCrossjoin**函数使用任何剩余的集，指定在后续的指定集，但尚未交叉联接来确定哪些成员都被视为在交叉联接集产生非空。 **NonEmptyCrossjoin**函数方面**NON_EMPTY_BEHAVIOR**的计算度量值设置。  
  
> [!IMPORTANT]  
>  不推荐使用此函数并且不应使用它，保留此函数仅是为了维护向后兼容性。 相反，应使用[存在 (MDX)](../mdx/exists-mdx.md)具有度量值组名称自变量函数或[NonEmpty (MDX)](../mdx/nonempty-mdx.md)函数。  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
