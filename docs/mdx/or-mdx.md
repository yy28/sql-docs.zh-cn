---
title: 或者 (MDX) |Microsoft 文档
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 215ed38ef7887d9815c6cf4ac79321b95a367707
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/02/2018
ms.locfileid: "34580619"
---
# <a name="or-mdx"></a>OR (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
## <a name="remarks"></a>Remarks  
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
  
## <a name="see-also"></a>请参阅  
 [MDX 运算符参考&#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
