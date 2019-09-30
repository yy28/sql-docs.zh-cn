---
title: CODEPOINT（SSIS 表达式）| Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- CODEPOINT function
- leftmost character of expression
ms.assetid: 0783d05e-7f35-42fb-a2c4-9621c46effd6
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 06c015c2f96bf2f7206a3e802d44a65871828d2c
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2019
ms.locfileid: "71290265"
---
# <a name="codepoint-ssis-expression"></a>CODEPOINT（SSIS 表达式）

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  返回字符表达式中最左侧字符的 Unicode 码位。  
  
## <a name="syntax"></a>语法  
  
```  
  
CODEPOINT(character_expression)  
```  
  
## <a name="arguments"></a>参数  
 *character_expression*  
 要对其最左侧字符进行计算的字符表达式。  
  
## <a name="result-types"></a>结果类型  
 DT_UI2  
  
## <a name="remarks"></a>Remarks  
 *character_expression* 必须具有 DT_WSTR 数据类型。  
  
 如果 *character_expression* 为 NULL 或为空字符串，则 CODEPOINT 返回的结果为 NULL。  
  
## <a name="expression-examples"></a>表达式示例  
 此示例使用一个字符串文字。 返回结果为 M 的 Unicode 码位 77。  
  
```  
CODEPOINT("Mountain Bike")  
```  
  
 此示例使用一个变量。 如果 **Name** 为 Touring Front Wheel，则返回结果为 T 的 Unicode 码位 84。  
  
```  
CODEPOINT(@Name)  
```  
  
## <a name="see-also"></a>另请参阅  
 [函数（SSIS 表达式）](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
