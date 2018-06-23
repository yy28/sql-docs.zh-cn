---
title: '&amp;&amp;（逻辑与）（SSIS 表达式）| Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- '&& (logical AND)'
- AND, logical AND
- logical AND (&&)
ms.assetid: a8cb3517-d5d1-4861-9f04-905c719185ff
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 9f6cdb28a48a69ee1702b19918b9326ac861eb29
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36016149"
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
  
## <a name="remarks"></a>Remarks  
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
 [&&#40;按位 AND&#41; &#40;SSIS 表达式&#41;](bitwise-and-ssis-expression.md)   
 [运算符优先级和结合性](operator-precedence-and-associativity.md)   
 [运算符&#40;SSIS 表达式&#41;](operators-ssis-expression.md)  
  
  