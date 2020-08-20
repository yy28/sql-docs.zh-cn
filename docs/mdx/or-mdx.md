---
description: OR (MDX)
title: 或 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d5ea3e65dd9bad768ef829858d42d6e4adea7a72
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471749"
---
# <a name="or-mdx"></a>OR (MDX)


  对数值表达式执行逻辑或运算。  
  
## <a name="syntax"></a>语法  
  
```  
  
Expression1 OR Expression2   
```  
  
#### <a name="parameters"></a>参数  
 Expression1  
 返回数值的有效多维表达式 (MDX) 表达式。  
  
 Expression2  
 返回数值的有效 MDX 表达式。  
  
## <a name="return-value"></a>返回值  
 一个布尔值，如果其中一个或两个参数的计算结果都为**true**，则返回**true** ;否则**为 false**。  
  
## <a name="remarks"></a>备注  
 **OR**运算符将两个参数都视为布尔值 (零，0，为**false**;否则，在运算符执行逻辑析取**之前) 。** 下表说明了 **OR** 运算符如何执行逻辑析取。  
  
|Expression1|Expression2|返回值|  
|-------------------|-------------------|------------------|  
|true|true|true|  
|true|**false**|true|  
|**false**|true|true|  
|**false**|**false**|**false**|  
  
## <a name="example"></a>示例  
 如果客户维度的性别层次结构上的当前成员为 "男" 或 "客户" 维度的 "婚姻状态" 层次结构上的当前成员已结婚，则以下查询包含一个返回字符串 "结婚或男" 的计算度量值;否则，它将返回字符串 "UNMARRIED OR 女性"。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [Mdx 运算符引用 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
