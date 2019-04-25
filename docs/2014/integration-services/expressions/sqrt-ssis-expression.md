---
title: SQRT（SSIS 表达式）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQRT function
- square root of given expression
ms.assetid: 54a75389-c501-4e22-87b8-905f66d6a3a5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 308a74501b0b4bf7b071feae2088c1ab1b7f030c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62768763"
---
# <a name="sqrt-ssis-expression"></a>SQRT（SSIS 表达式）
  返回数值表达式的平方根。  
  
## <a name="syntax"></a>语法  
  
```  
  
SQRT(numeric_expression)  
```  
  
## <a name="arguments"></a>参数  
 *numeric_expression*  
 是任意数值数据类型的数值表达式。 有关详细信息，请参阅 [Integration Services 数据类型](../data-flow/integration-services-data-types.md)。  
  
## <a name="result-types"></a>结果类型  
 DT_R8  
  
## <a name="remarks"></a>备注  
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
>  在表达式中，变量名始终包含前缀 \@。  
  
## <a name="see-also"></a>请参阅  
 [函数（SSIS 表达式）](functions-ssis-expression.md)  
  
  
