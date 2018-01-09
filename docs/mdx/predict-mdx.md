---
title: "预测 (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: PREDICT
dev_langs: kbMDX
helpviewer_keywords: Predict function
ms.assetid: a82f3edd-249b-4559-98d3-6e10d81a095d
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: d7266e462167dcae27a30b033c368f910b6dfc0f
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="predict-mdx"></a>Predict (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

    
> [!CAUTION]  
>  此函数由于内部不一致而正被删除。  
>   
>  有关使用 DMX 表达式的解决方法，请查看示例部分。  
  
 返回用数值表达式对数据挖掘模型求得的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
Predict(Mining_Model_Name,String_Expression)   
```  
  
## <a name="arguments"></a>参数  
 *Mining_Model_Name*  
 表示挖掘模型名称的有效字符串表达式。  
  
 *String_Expression*  
 计算结果为指定挖掘模型的有效 DMX 表达式的有效字符串表达式。  
  
## <a name="remarks"></a>Remarks  
 **预测**函数的计算结果指定的挖掘模型的上下文中的指定的字符串表达式。  
  
 在数据挖掘表达式 (DMX) 参考中提供了数据挖掘语法和函数。  
  
## <a name="example"></a>示例  
 下面的示例使用 Customer Clusters 挖掘模型预测群集的名称以及与特定客户的距离：  
  
```  
WITH MEMBER MEASURES.CLNAME AS   
PREDICT("Customer Clusters", "Cluster()")  
MEMBER MEASURES.CLDISTANCE AS   
PREDICT("Customer Clusters", "ClusterDistance(Cluster())")  
SELECT {MEASURES.CLNAME, MEASURES.CLDISTANCE} ON 0   
FROM [Adventure Works]  
WHERE([Customer].[Customer Geography].[Customer].&[12012])  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
