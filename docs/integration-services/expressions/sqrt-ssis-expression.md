---
title: "SQRT （SSIS 表达式） |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: expressions
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQRT function
- square root of given expression
ms.assetid: 54a75389-c501-4e22-87b8-905f66d6a3a5
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f5ae5e55d52ba0e4232d8e7a83d3aab2f70a6b56
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="sqrt-ssis-expression"></a>SQRT（SSIS 表达式）
  返回数值表达式的平方根。  
  
## <a name="syntax"></a>语法  
  
```  
  
SQRT(numeric_expression)  
```  
  
## <a name="arguments"></a>参数  
 *numeric_expression*  
 是任意数值数据类型的数值表达式。 有关详细信息，请参阅 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)。  
  
## <a name="result-types"></a>结果类型  
 DT_R8  
  
## <a name="remarks"></a>注释  
 如果参数为空，则 SQRT 返回的结果为空。  
  
 如果参数是负值，则 SQRT 失败。  
  
 进行平方根操作前，该参数被转换为 DT_R8 数据类型。  
  
## <a name="expression-examples"></a>表达式示例  
 此示例返回数值的平方根。 返回结果为 12。  
  
```  
SQRT(144)  
```  
  
 此示例返回表达式（ **Value1** 列和 **Value2** 列的值相减的结果）的平方根。  
  
```  
SQRT(Value1 - Value2)  
```  
  
 此示例通过对两个变量应用 SQUARE 函数然后计算其和的平方根，返回直角三角形第三边的长度。 如果 **Side1** 包含3， **Side2** 包含4，则 SQRT 函数返回 5。  
  
```  
SQRT(SQUARE(@Side1) + SQUARE(@Side2))  
```  
  
> [!NOTE]  
>  在表达式中，变量名必须包含前缀 @。  
  
## <a name="see-also"></a>另请参阅  
 [函数 &#40;SSIS 表达式 &#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  

