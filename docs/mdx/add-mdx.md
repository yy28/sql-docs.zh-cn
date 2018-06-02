---
title: + （添加）(MDX) |Microsoft 文档
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b13784b757241cc99ee58bec949348017b048e64
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/02/2018
ms.locfileid: "34576969"
---
# <a name="-add-mdx"></a>+（加）(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  执行两个数相加的算术运算。  
  
## <a name="syntax"></a>语法  
  
```  
  
Numeric_Expression + Numeric_Expression  
```  
  
#### <a name="parameters"></a>Parameters  
 *数值表达式*  
 返回数值的有效多维表达式 (MDX) 表达式。  
  
## <a name="return-value"></a>返回值  
 具有与优先级较高的参数相同的数据类型的值。  
  
## <a name="remarks"></a>Remarks  
 两个表达式必须具有相同的数据类型，或者其中一个表达式必须能够隐式转换为另一个表达式的数据类型。 如果一个表达式求出的值为空值，该运算符将返回另一个表达式的结果。  
  
## <a name="see-also"></a>请参阅  
 [MDX 运算符参考&#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
