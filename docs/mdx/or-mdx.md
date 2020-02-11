---
title: 或（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 45063e9f2aca6a924289d4d52434535d16c9a08e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68055707"
---
# <a name="or-mdx"></a>OR (MDX)


  对数值表达式执行逻辑或运算。  
  
## <a name="syntax"></a>语法  
  
```  
  
Expression1 OR Expression2   
```  
  
#### <a name="parameters"></a>parameters  
 Expression1  
 返回数值的有效多维表达式 (MDX) 表达式。  
  
 Expression2  
 返回数值的有效 MDX 表达式。  
  
## <a name="return-value"></a>返回值  
 一个布尔值，如果其中一个或两个参数的计算结果都为**true**，则返回**true** ;否则**为 false**。  
  
## <a name="remarks"></a>备注  
 在运算符执行逻辑析取之前，**或**运算符将两个参数都视为布尔值（零，0，为**false**; 否则为**true**）。 下表说明了**OR**运算符如何执行逻辑析取。  
  
|Expression1 |Expression2 |返回值|  
|-------------------|-------------------|------------------|  
|**true**|**true**|**true**|  
|**true**|**false**|**true**|  
|**false**|**true**|**true**|  
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
  
  
