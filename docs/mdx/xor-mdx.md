---
title: XOR （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 1657d9e58a0ae729a67e179602cd9a886ae923b1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68125792"
---
# <a name="xor-mdx"></a>XOR (MDX)


  对两个数值表达式执行逻辑异运算。  
  
## <a name="syntax"></a>语法  
  
```  
  
Expression1 XOR Expression2  
  
```  
  
#### <a name="parameters"></a>参数  
 *Expression1*  
 返回数值的有效多维表达式 (MDX) 表达式。  
  
 Expression2**  
 返回数值的有效 MDX 表达式。  
  
## <a name="return-value"></a>返回值  
 一个布尔值，如果一个且仅有一个参数的计算结果为**true**，则返回**true** ;否则**为 false**。  
  
## <a name="remarks"></a>备注  
 **XOR**运算符将两个参数都视为布尔值（0，0，为**false**; 否则为**true**），然后运算符执行逻辑异运算。 下表说明了**XOR**运算符如何执行逻辑异运算。  
  
|*Expression1*|Expression2**|返回值|  
|-------------------|-------------------|------------------|  
|**true**|true |**false**|  
|true |**false**|true |  
|**false**|**true**|true |  
|**false**|**false**|**false**|  
  
## <a name="see-also"></a>另请参阅  
 [Mdx 运算符引用 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
