---
title: 预测（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 165d03b886ad8e9beeb09bf5a835c879cc23a2a4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68055584"
---
# <a name="predict-mdx"></a>Predict (MDX)


    
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
  
## <a name="remarks"></a>备注  
 **Predict**函数计算指定挖掘模型上下文中指定字符串表达式的值。  
  
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
 [Mdx 函数引用 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
