---
title: GETUTCDATE（SSIS 表达式）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- dates [Integration Services], GETUTCDATE
- current date
- UTC time
- GETUTCDATE function
ms.assetid: 2282339c-c24f-493e-8e66-181ea8af5ad0
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 5e8c8dbdee729b01ed4b49e5a38ff989c80fbc20
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85428624"
---
# <a name="getutcdate-ssis-expression"></a>GETUTCDATE（SSIS 表达式）
  使用 DT_DBTIMESTAMP 格式返回以 UTC 时间（协调世界时或格林尼治标准时间）表示的系统当前日期。 GETUTCDATE 函数不带参数。  
  
## <a name="syntax"></a>语法  
  
```  
  
GETUTCDATE()  
```  
  
## <a name="arguments"></a>参数  
 无  
  
## <a name="result-types"></a>结果类型  
 DT_DBTIMESTAMP  
  
## <a name="expression-examples"></a>表达式示例  
 此示例返回以 UTC 时间表示的当前日期的年份。  
  
```  
DATEPART("year",GETUTCDATE())  
```  
  
 此示例返回 **ModifiedDate** 列中的日期和当前 UTC 日期之间的天数。  
  
```  
DATEDIFF("dd",ModifiedDate,GETUTCDATE())  
```  
  
 此示例将三个月加到当前 UTC 日期。  
  
```  
DATEADD("Month",3,GETUTCDATE())  
```  
  
## <a name="see-also"></a>另请参阅  
 [GETDATE（SSIS 表达式）](getdate-ssis-expression.md)   
 [函数（SSIS 表达式）](functions-ssis-expression.md)  
  
  
