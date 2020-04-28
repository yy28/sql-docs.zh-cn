---
title: 不是（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4031b887eb0a42580d6ae8debf6c9177ff67efc3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68088227"
---
# <a name="not-mdx"></a>NOT (MDX)


  对数值表达式执行逻辑非运算。  
  
## <a name="syntax"></a>语法  
  
```  
  
NOT Expression1  
```  
  
#### <a name="parameters"></a>参数  
 *Expression1*  
 返回数值的有效多维表达式 (MDX) 表达式。  
  
## <a name="return-value"></a>返回值  
 一个布尔值，如果参数的计算结果为**true**，则返回**false** ;否则**为 true**。  
  
## <a name="remarks"></a>备注  
 **NOT**运算符将表达式视为布尔值（零，0，为**false**; 否则为**true**），然后运算符执行逻辑非运算。 下表说明了 NOT 运算符如何执行逻辑**非**运算。  
  
|*Expression1*|返回值|  
|-------------------|------------------|  
|true |**false**|  
|**false**|**true**|  
  
## <a name="see-also"></a>另请参阅  
 [Mdx 运算符引用 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
