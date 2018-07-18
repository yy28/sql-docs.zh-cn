---
title: REVERSE（SSIS 表达式）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- REVERSE function
- reverse character expressions
ms.assetid: bcebcc55-7247-4896-8f53-4d582d58cfb4
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: eb219d26d5aa4ce4d1bb2d241475b39d65673f80
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37180364"
---
# <a name="reverse-ssis-expression"></a>REVERSE（SSIS 表达式）
  按相反顺序返回字符表达式。  
  
## <a name="syntax"></a>语法  
  
```  
  
REVERSE(character_expression)  
```  
  
## <a name="arguments"></a>参数  
 *character_expression*  
 是要反转的字符表达式。  
  
## <a name="result-types"></a>结果类型  
 DT_WSTR  
  
## <a name="remarks"></a>Remarks  
 character_expression 参数必须具有 DT_WSTR 数据类型。  
  
 如果 character_expression 为 Null，则 REVERSE 将返回 Null 结果。  
  
## <a name="expression-examples"></a>表达式示例  
 此示例使用一个字符串文字。 返回结果为“ekiB niatnuoM”。  
  
```  
REVERSE("Mountain Bike")  
```  
  
 此示例使用一个变量。 如果 **Name** 包含 Touring Bike，则返回的结果为“ekiB gniruoT”。  
  
```  
REVERSE(@Name)  
```  
  
## <a name="see-also"></a>请参阅  
 [函数&#40;SSIS 表达式&#41;](functions-ssis-expression.md)  
  
  
