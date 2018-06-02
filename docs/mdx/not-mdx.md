---
title: 不 (MDX) |Microsoft 文档
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5020f461d2576bbac7d0292ca0bf75bd8033e173
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/02/2018
ms.locfileid: "34580499"
---
# <a name="not-mdx"></a>NOT (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  对数值表达式执行逻辑非运算。  
  
## <a name="syntax"></a>语法  
  
```  
  
NOT Expression1  
```  
  
#### <a name="parameters"></a>Parameters  
 *Expression1*  
 返回数值的有效多维表达式 (MDX) 表达式。  
  
## <a name="return-value"></a>返回值  
 返回一个布尔值**false**如果自变量的计算结果为**true**; 否则为**true**。  
  
## <a name="remarks"></a>Remarks  
 **不**运算符将表达式视为一个布尔值 (0，0，作为**false**; 否则为**true**) 运算符执行逻辑求反运算之前。 下表说明了如何**不**运算符执行逻辑求反运算。  
  
|*Expression1*|返回值|  
|-------------------|------------------|  
|**true**|**false**|  
|**false**|**true**|  
  
## <a name="see-also"></a>请参阅  
 [MDX 运算符参考&#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
