---
title: ROUND（SSIS 表达式）| Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- rounding expressions
- ROUND function [SSIS]
ms.assetid: 376f1947-4fc5-4611-ad86-823e4db1b468
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 74b18ed725b70e1086b22515a0a051d2521383b7
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "71288325"
---
# <a name="round-ssis-expression"></a>ROUND（SSIS 表达式）

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  返回舍入到指定长度或精度的数值表达式。 length 参数的取值必须为整数。  
  
## <a name="syntax"></a>语法  
  
```  
  
ROUND(numeric_expression,length)  
```  
  
## <a name="arguments"></a>参数  
 *numeric_expression*  
 是有效的数值类型的表达式。 有关详细信息，请参阅 [Integration Services 数据类型](../../integration-services/data-flow/integration-services-data-types.md)。  
  
 *length*  
 是整数表达式。 它是 *numeric_expression* 的舍入精度。  
  
## <a name="result-types"></a>结果类型  
 与 *numeric*_*expression.* 相同的类型。  
  
## <a name="remarks"></a>备注  
 *length* 参数的取值必须为正整数或零。  
  
 如果该参数为空，则 ROUND 返回的结果为空。  
  
## <a name="expression-examples"></a>表达式示例  
 下面的示例对数值进行舍入操作，使其精确到小数点后 3 位。 第一个返回结果为 137.1570，第二个为 137.1580。  
  
```  
ROUND(137.1574,3)  
ROUND(137.1575,3)  
```  
  
## <a name="see-also"></a>另请参阅  
 [函数（SSIS 表达式）](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
