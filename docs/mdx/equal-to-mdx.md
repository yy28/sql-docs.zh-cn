---
title: = （等于） (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 189facb54de244ff220b41ec08c8b02faf5a2c27
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68139315"
---
# <a name="-equal-to-mdx"></a>=（等于）(MDX)


  执行比较运算，以确定一个多维表达式 (MDX) 的值是否等于另一个 MDX 表达式的值。  
  
> [!NOTE]  
>  若要比较的对象，请使用[IS &#40;MDX&#41; ](../mdx/is-mdx.md)运算符。 例如，检查查询轴上的当前成员是否为特定成员时，使用 IS 运算符。  
  
## <a name="syntax"></a>语法  
  
```  
  
MDX_Expression = MDX_Expression   
```  
  
#### <a name="parameters"></a>Parameters  
 *MDX_Expression*  
 有效的 MDX 表达式。  
  
## <a name="return-value"></a>返回值  
 布尔值，具体情形如下：  
  
-   **true**的第一个参数的值是否等于第二个参数的值。  
  
-   **false**的第一个参数的值是否不等于第二个参数的值。  
  
-   **true**如果两个参数都为 null，或一个参数为 null，则另一个参数为 0。  
  
## <a name="examples"></a>示例  
 以下查询说明上述情况的示例：  
  
 `With`  
  
 `--Returns true`  
  
 `Member [Measures].bool1 as 1=1`  
  
 `--Returns false`  
  
 `Member [Measures].bool2 as 1=0`  
  
 `--Returns true`  
  
 `Member [Measures].bool3 as null=null`  
  
 `--Returns true`  
  
 `Member [Measures].bool4 as 0=null`  
  
 `--Returns false`  
  
 `Member [Measures].bool5 as 1=null`  
  
 `Select {[Measures].bool1,[Measures].bool2,[Measures].bool3,[Measures].bool4,[Measures].bool5}`  
  
 `On 0`  
  
 `From [Adventure Works]`  
  
## <a name="see-also"></a>请参阅  
 [MDX 运算符参考&#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
