---
title: '||（逻辑或）（SSIS 表达式） | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- OR operator
- logical OR (||)
- '|| (logical OR)'
ms.assetid: a3c07c09-f121-4187-9617-b01adcf843c4
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e63c829e1865213b29aca6e75d1de52021b4d5ac
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48052317"
---
# <a name="-logical-or-ssis-expression"></a>||（逻辑或）（SSIS 表达式）
  执行“逻辑或”运算。 如果条件之一或两个条件都为 TRUE，则表达式计算结果为 TRUE。  
  
## <a name="syntax"></a>语法  
  
```  
  
boolean_expression1 || boolean_expression2  
```  
  
## <a name="arguments"></a>参数  
 *boolean_expression1、boolean_expression2*  
 计算结果为 TRUE、FALSE 或 NULL 的任意有效表达式。  
  
## <a name="result-types"></a>结果类型  
 DT_BOOL  
  
## <a name="remarks"></a>备注  
 下表显示了 || 运算符的结果。  
  
|结果|表达式|表达式|  
|------------|----------------|----------------|  
|TRUE|TRUE|TRUE|  
|TRUE|TRUE|FALSE|  
|FALSE|FALSE|FALSE|  
|NULL|NULL|NULL|  
|TRUE|NULL|TRUE|  
|NULL|NULL|FALSE|  
  
## <a name="ssis-expression-examples"></a>SSIS 表达式示例  
 该示例使用 **StandardCost** 和 **ListPrice** 列。 如果 **StandardCost** 列的值小于 300 或者 **ListPrice** 列的值大于 500，则该示例计算结果为 TRUE。  
  
```  
StandardCost < 300 || ListPrice > 500  
```  
  
 该示例使用变量 **SPrice** 和 **LPrice** ，而不是数值。  
  
```  
StandardCost < @SPrice || ListPrice > @LPrice  
```  
  
## <a name="see-also"></a>请参阅  
 [&#124;&#40;按位异或&#41; &#40;SSIS 表达式&#41;](bitwise-inclusive-or-ssis-expression.md)   
 [^（位异或）（SSIS 表达式）](bitwise-exclusive-or-ssis-expression.md)   
 [运算符优先级和结合性](operator-precedence-and-associativity.md)   
 [运算符&#40;SSIS 表达式&#41;](operators-ssis-expression.md)  
  
  
