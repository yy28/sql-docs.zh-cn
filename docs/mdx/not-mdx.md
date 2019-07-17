---
title: 不 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4031b887eb0a42580d6ae8debf6c9177ff67efc3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088227"
---
# <a name="not-mdx"></a>NOT (MDX)


  对数值表达式执行逻辑非运算。  
  
## <a name="syntax"></a>语法  
  
```  
  
NOT Expression1  
```  
  
#### <a name="parameters"></a>Parameters  
 *Expression1*  
 返回数值的有效多维表达式 (MDX) 表达式。  
  
## <a name="return-value"></a>返回值  
 一个布尔值，返回**false**如果参数的值为**true**; 否则为**true**。  
  
## <a name="remarks"></a>备注  
 **不**运算符将表达式视为一个布尔值 (0 被作为**false**; 否则为**true**) 运算符执行逻辑非运算之前。 下表说明了如何**不**运算符执行逻辑求反。  
  
|*Expression1*|返回值|  
|-------------------|------------------|  
|**true**|**false**|  
|**false**|**true**|  
  
## <a name="see-also"></a>请参阅  
 [MDX 运算符参考&#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
