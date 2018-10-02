---
title: GETUTCDATE（SSIS 表达式）| Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- dates [Integration Services], GETUTCDATE
- current date
- UTC time
- GETUTCDATE function
ms.assetid: 2282339c-c24f-493e-8e66-181ea8af5ad0
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4afe3909387669e1bfcc230744ff7cf5dbd7ae20
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47648175"
---
# <a name="getutcdate-ssis-expression"></a>GETUTCDATE（SSIS 表达式）
  使用 DT_DBTIMESTAMP 格式返回以 UTC 时间（协调世界时或格林尼治标准时间）表示的系统当前日期。 GETUTCDATE 函数不带参数。  
  
## <a name="syntax"></a>语法  
  
```  
  
GETUTCDATE()  
```  
  
## <a name="arguments"></a>参数  
 None  
  
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
 [GETDATE（SSIS 表达式）](../../integration-services/expressions/getdate-ssis-expression.md)   
 [函数（SSIS 表达式）](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
