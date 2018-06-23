---
title: '! （逻辑非）（SSIS 表达式）| Microsoft Docs'
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
- logical Not (!)
- '! (logical Not)'
ms.assetid: d5c4d1e1-7be4-4d25-bcd9-5b6ddb53b3b3
caps.latest.revision: 35
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 7de99bf9dc767c5f4f6e47abd88f66f874ebb1be
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015483"
---
# <a name="-logical-not-ssis-expression"></a>! （逻辑非）（SSIS 表达式）
  对布尔操作数求反。  
  
> [!NOTE]  
>  此 ! 运算符不能与其他运算符一起使用。 例如，不能将 ! 和 > 运算符组合为 !>. 运算符。  
  
## <a name="syntax"></a>语法  
  
```  
  
!boolean_expression  
  
```  
  
## <a name="arguments"></a>参数  
 *boolean_expression*  
 计算结果为布尔值的任何有效表达式。 有关详细信息，请参阅 [Integration Services 数据类型](../data-flow/integration-services-data-types.md)。  
  
## <a name="result-types"></a>结果类型  
 DT_BOOL  
  
## <a name="remarks"></a>Remarks  
 下表显示了 ! 操作。  
  
|原始布尔表达式|应用 ! 运算符后的表达式|  
|---------------------------------|------------------------------------|  
|TRUE|FALSE|  
|NULL|NULL|  
|FALSE|TRUE|  
  
## <a name="expression-examples"></a>表达式示例  
 以下示例中，如果 **Color** 列的值为“red”，则计算结果为 FALSE。  
  
```  
!(Color == "red")  
```  
  
 在以下示例中，如果 **MonthNumber** 变量的值和代表当前月份的整数相同，则计算结果为 TRUE。 有关详细信息，请参阅 [MONTH（SSIS 表达式）](month-ssis-expression.md)和 [GETDATE（SSIS 表达式）](getdate-ssis-expression.md)。  
  
```  
!(@MonthNumber != MONTH(GETDATE())  
```  
  
## <a name="see-also"></a>请参阅  
 [运算符优先级和结合性](operator-precedence-and-associativity.md)   
 [运算符&#40;SSIS 表达式&#41;](operators-ssis-expression.md)  
  
  