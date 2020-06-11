---
title: 拆分（DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 2d75bd4a1d4b75d9acb153c3a3aec9efcf58d876
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2020
ms.locfileid: "83669741"
---
# <a name="divide-dmx"></a>（除）(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  执行算术运算，将一个数除以另一个数。  
  
## <a name="syntax"></a>语法  
  
```  
  
Dividend / Divisor  
```  
  
#### <a name="parameters"></a>参数  
 *被除数*  
 一个返回数值的有效数据挖掘扩展 (DMX) 表达式。  
  
 *除数*  
 一个返回数值的有效 DMX 表达式。  
  
## <a name="return-value"></a>返回值  
 与优先级较高的参数具有相同数据类型的值。  
  
## <a name="remarks"></a>注解  
 此运算符返回的值即为用第一个表达式除以第二个表达式所得的商。  
  
 两个表达式必须具有相同的数据类型，或者其中一个表达式必须能够隐式转换为另一个表达式的数据类型。 如果除数的计算结果为 Null 值，则该运算符将产生错误。 如果除数和被除数的计算结果均为 Null 值，则该运算符将返回 Null 值。  
  
## <a name="see-also"></a>另请参阅  
 [算术运算符 &#40;DMX&#41;](../dmx/operators-arithmetic.md)   
 [数据挖掘扩展插件 &#40;DMX&#41; 运算符引用](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [运算符 &#40;DMX&#41;](../dmx/operators-dmx.md)   
 [将 &#40;SSIS 表达式相除&#41;](../integration-services/expressions/divide-ssis-expression.md)   
 [&#40;相除&#41; &#40;Transact-sql&#41;](../t-sql/language-elements/divide-transact-sql.md)  
  
  
