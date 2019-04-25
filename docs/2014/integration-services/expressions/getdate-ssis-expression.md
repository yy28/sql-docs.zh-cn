---
title: GETDATE（SSIS 表达式）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- current date
- GETDATE function
- dates [Integration Services], GETDATE
ms.assetid: 6d20ec93-3244-4d63-baf6-70eff7bd598c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 83d8d4126ff7dbcd6e0d5b114626cd8acb1b8d20
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62769024"
---
# <a name="getdate-ssis-expression"></a>GETDATE（SSIS 表达式）
  以 DT_DBTIMESTAMP 格式返回系统的当前日期。 GETDATE 函数不使用参数。  
  
> [!NOTE]  
>  GETDATE 函数的返回结果的长度为 29 个字符。  
  
## <a name="syntax"></a>语法  
  
```  
  
GETDATE()  
```  
  
## <a name="arguments"></a>参数  
 None  
  
## <a name="result-types"></a>结果类型  
 DT_DBTIMESTAMP  
  
## <a name="expression-examples"></a>表达式示例  
 此示例返回当前日期的年份。  
  
```  
DATEPART("year",GETDATE())  
```  
  
 此示例返回 **ModifiedDate** 列中的日期和当前日期之间的天数。  
  
```  
DATEDIFF("dd",ModifiedDate,GETDATE())  
```  
  
 此示例将三个月加到当前日期。  
  
```  
DATEADD("Month",3,GETDATE())  
```  
  
## <a name="see-also"></a>请参阅  
 [GETUTCDATE（SSIS 表达式）](getutcdate-ssis-expression.md)   
 [函数（SSIS 表达式）](functions-ssis-expression.md)  
  
  
