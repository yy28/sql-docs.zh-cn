---
title: 或者 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ae6b6602d7968bb444dcf4838537bb000b97dd53
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63278260"
---
# <a name="or-mdx"></a>OR (MDX)


  对数值表达式执行逻辑或运算。  
  
## <a name="syntax"></a>语法  
  
```  
  
Expression1 OR Expression2   
```  
  
#### <a name="parameters"></a>Parameters  
 Expression1  
 返回数值的有效多维表达式 (MDX) 表达式。  
  
 Expression2  
 返回数值的有效 MDX 表达式。  
  
## <a name="return-value"></a>返回值  
 一个布尔值，返回 **，则返回 true**如果一个或两个参数的计算结果为**true**; 否则为**false**。  
  
## <a name="remarks"></a>备注  
 **或者**运算符将这两个参数视为布尔值 (0 被作为**false**; 否则为**true**) 运算符执行逻辑或运算之前。 下表说明了如何**或**运算符执行逻辑或运算。  
  
|*Expression1*|*Expression2*|返回值|  
|-------------------|-------------------|------------------|  
|**true**|**true**|**true**|  
|**true**|**false**|**true**|  
|**false**|**true**|**true**|  
|**false**|**false**|**false**|  
  
## <a name="example"></a>示例  
 下面的查询包含返回的字符串"MARRIED OR MALE"如果客户维度的 Gender 层次结构上的当前成员为 Male 时或者在客户维度的 Marital Status 层次上的当前成员已婚; 一个计算度量值否则它将返回字符串"UNMARRIED 或 FEMALE"。  
  
```  
WITH  
MEMBER MEASURES.ORDEMO AS  
IIF(  
([Customer].[Gender].CURRENTMEMBER IS [Customer].[Gender].&[M])  
OR  
([Customer].[Marital Status].CURRENTMEMBER IS [Customer].[Marital Status].&[M]),  
"MARRIED OR MALE",  
"UNMARRIED OR FEMALE")  
SELECT [Customer].[Gender].[Gender].MEMBERS ON 0,  
[Customer].[Marital Status].[Marital Status].MEMBERS ON 1  
FROM [Adventure Works]  
WHERE(MEASURES.ORDEMO)  
```  
  
## <a name="see-also"></a>请参阅  
 [MDX 运算符参考&#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
