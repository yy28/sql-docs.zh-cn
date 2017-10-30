---
title: "或者 (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OR
dev_langs:
- kbMDX
helpviewer_keywords:
- OR operator
ms.assetid: 7634c08a-5b70-44cd-9422-6555fed6ae05
caps.latest.revision: 27
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 61639a3309b222565eeb94b19d0c4b1fba69389f
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="or-mdx"></a>OR (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 返回一个布尔值**true**如果其中一种或两个自变量的计算结果为**true**; 否则为**false**。  
  
## <a name="remarks"></a>注释  
 **或者**运算符将两个参数视为布尔值 (0，0，作为**false**; 否则为**true**) 运算符执行逻辑或运算之前。 下表说明了如何**或**运算符执行逻辑或运算。  
  
|*Expression1*|*Expression2*|返回值|  
|-------------------|-------------------|------------------|  
|**true**|**true**|**true**|  
|**true**|**false**|**true**|  
|**false**|**true**|**true**|  
|**false**|**false**|**false**|  
  
## <a name="example"></a>示例  
 下面的查询包含一个计算度量值，该度量值在 Customer 维度的 Gender 层次结构上的当前对象为 Male 时或者在 Customer 维度的 Marital Status 层次结构上的当前对象为 Married 时返回字符串“MARRIED OR MALE”，否则，它将返回字符串“UNMARRIED OR FEMALE”。  
  
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
 [MDX 运算符参考 &#40;MDX &#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  

