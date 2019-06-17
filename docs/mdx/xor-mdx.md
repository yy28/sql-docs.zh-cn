---
title: XOR (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f9115fc1e226e05c788206706d59a5435bfd1c5d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63251486"
---
# <a name="xor-mdx"></a>XOR (MDX)


  对两个数值表达式执行逻辑异运算。  
  
## <a name="syntax"></a>语法  
  
```  
  
Expression1 XOR Expression2  
  
```  
  
#### <a name="parameters"></a>Parameters  
 *Expression1*  
 返回数值的有效多维表达式 (MDX) 表达式。  
  
 *Expression2*  
 返回数值的有效 MDX 表达式。  
  
## <a name="return-value"></a>返回值  
 一个布尔值，返回 **，则返回 true**如果有且只有一个参数的值为**true**; 否则为**false**。  
  
## <a name="remarks"></a>备注  
 **XOR**运算符将两个参数都视为布尔值 (0 被作为**false**; 否则为**true**) 运算符执行逻辑异运算之前。 下表说明了如何**XOR**运算符执行逻辑异运算。  
  
|*Expression1*|*Expression2*|返回值|  
|-------------------|-------------------|------------------|  
|**true**|**true**|**false**|  
|**true**|**false**|**true**|  
|**false**|**true**|**true**|  
|**false**|**false**|**false**|  
  
## <a name="see-also"></a>请参阅  
 [MDX 运算符参考&#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
