---
title: ISNULL（SSIS 表达式）| Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- null values [Integration Services]
- ISNULL function
ms.assetid: 88dbf49e-1307-4dda-b9db-ff1632053550
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f57f66c531619ab81b9e7cd6f7b49324efd7f09f
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/16/2019
ms.locfileid: "65725289"
---
# <a name="isnull-ssis-expression"></a>ISNULL（SSIS 表达式）

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  根据表达式是否为空，返回一个布尔值结果。  
  
## <a name="syntax"></a>语法  
  
```  
  
ISNULL(expression)  
```  
  
## <a name="arguments"></a>参数  
 *expression*  
 是任何数据类型的有效表达式。  
  
## <a name="result-types"></a>结果类型  
 DT_BOOL  
  
## <a name="expression-examples"></a>表达式示例  
 如果 **DiscontinuedDate** 列包含 Null 值，此示例将返回 TRUE。  
  
```  
ISNULL(DiscontinuedDate)  
```  
  
 如果 **LastName** 列中的值为空，则此示例返回“Unknown last name”，否则返回 **LastName**中的值。  
  
```  
ISNULL(LastName)? "Unknown last name":LastName  
```  
  
 如果 **DaysToManufacture** 列为空，则不管变量 **AddDays**的值如何，此示例都始终返回 TRUE。  
  
```  
ISNULL(DaysToManufacture + @AddDays)  
```  
  
## <a name="see-also"></a>另请参阅  
 [函数（SSIS 表达式）](../../integration-services/expressions/functions-ssis-expression.md)   
 [COALESCE (Transact-SQL)](../../t-sql/language-elements/coalesce-transact-sql.md)  
  
  
