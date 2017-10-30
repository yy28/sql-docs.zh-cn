---
title: "SQUARE （SSIS 表达式） |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQUARE
- square values
ms.assetid: cecf1bb2-3d55-40a6-9688-ed67bcc150b4
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 18be83801a35d9b3512d85f69c91256147fb81a9
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="square-ssis-expression"></a>SQUARE（SSIS 表达式）
  返回数值表达式的平方。  
  
## <a name="syntax"></a>语法  
  
```  
  
SQUARE(numeric_expression)  
```  
  
## <a name="arguments"></a>参数  
 *numeric_expression*  
 是任意数值数据类型的数值表达式。 有关详细信息，请参阅 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)。  
  
## <a name="result-types"></a>结果类型  
 DT_R8  
  
## <a name="remarks"></a>注释  
 如果参数为空，SQUARE 将返回空结果。  
  
 执行 SQUARE 操作前，参数会转换为 DT_R8 数据类型。  
  
## <a name="expression-examples"></a>表达式示例  
 此示例返回 12 的平方。 返回结果为 144。  
  
```  
SQUARE(12)  
```  
  
 以下示例返回两列值相减所得结果的平方。 如果 **Value1** 包含 12， **Value2** 包含 4，则 SQUARE 函数返回 64。  
  
```  
SQUARE(Value1 - Value2)  
```  
  
 以下示例通过对两个变量应用 SQUARE 函数，然后计算其结果相加值的平方根，返回直角三角形斜边的长度。 如果 **Side1** 包含3， **Side2** 包含4，则 SQRT 函数返回 5。  
  
```  
SQRT(SQUARE(@Side1) + SQUARE(@Side2))  
```  
  
> [!NOTE]  
>  在表达式中，变量名必须包含前缀 @。  
  
## <a name="see-also"></a>另请参阅  
 [函数 &#40;SSIS 表达式 &#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  

