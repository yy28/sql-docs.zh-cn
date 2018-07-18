---
title: ISNULL（SSIS 表达式）| Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- null values [Integration Services]
- ISNULL function
ms.assetid: 88dbf49e-1307-4dda-b9db-ff1632053550
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8e8cf6188ea94f8afb1ff7208d4fc593190b0819
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/12/2018
ms.locfileid: "35404629"
---
# <a name="isnull-ssis-expression"></a>ISNULL（SSIS 表达式）
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
  
  
