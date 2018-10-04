---
title: '&amp;&amp;（逻辑与）（SSIS 表达式）| Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- '&& (logical AND)'
- AND, logical AND
- logical AND (&&)
ms.assetid: a8cb3517-d5d1-4861-9f04-905c719185ff
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a59545c26427afa1677eca78e4c00263e663dded
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48065527"
---
# <a name="ampamp-logical-and-ssis-expression"></a>&amp;&amp;（逻辑与）（SSIS 表达式）
  执行“逻辑与”运算。 如果所有条件都为 TRUE，则表达式计算结果为 TRUE。  
  
## <a name="syntax"></a>语法  
  
```  
  
boolean_expression1 && boolean_expression2  
```  
  
## <a name="arguments"></a>参数  
 *boolean _expression1、boolean_expression2*  
 计算结果为 TRUE、FALSE 或 NULL 的任意有效表达式。  
  
## <a name="result-types"></a>结果类型  
 DT_BOOL  
  
## <a name="remarks"></a>备注  
 下表显示 && 运算符的结果。  
  
|结果|表达式|表达式|  
|------------|----------------|----------------|  
|TRUE|TRUE|TRUE|  
|FALSE|TRUE|FALSE|  
|FALSE|FALSE|FALSE|  
|NULL|NULL|NULL|  
|NULL|NULL|TRUE|  
|FALSE|NULL|FALSE|  
  
## <a name="expression-examples"></a>表达式示例  
 该示例使用 **StandardCost** 和 **ListPrice** 列。 如果 **StandardCost** 列的值小于 300，并且 **ListPrice** 列的值大于 500，则该示例计算结果为 TRUE。  
  
```  
StandardCost < 300 && ListPrice > 500  
```  
  
 此示例使用变量 **SPrice** 和 **LPrice** ，而不是文字。  
  
```  
StandardCost < @SPrice && ListPrice > @LPrice  
```  
  
## <a name="see-also"></a>请参阅  
 [（& a)&#40;按位 AND&#41; &#40;SSIS 表达式&#41;](bitwise-and-ssis-expression.md)   
 [运算符优先级和结合性](operator-precedence-and-associativity.md)   
 [运算符&#40;SSIS 表达式&#41;](operators-ssis-expression.md)  
  
  
