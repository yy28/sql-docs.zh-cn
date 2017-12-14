---
title: "NULL（SSIS 表达式）| Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: expressions
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- NULL function
- null values [Integration Services]
ms.assetid: df144237-3fbb-41ac-8624-efd92b6522b9
caps.latest.revision: "30"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 29f3820518e10bf0b4066d7cf3e8e11d9e50ce3c
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="null-ssis-expression"></a>NULL（SSIS 表达式）
  返回请求的数据类型的 Null 值。  
  
## <a name="syntax"></a>语法  
  
```  
  
NULL(typespec)  
```  
  
## <a name="arguments"></a>参数  
 *typespec*  
 有效的数据类型。 有关详细信息，请参阅 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)。  
  
## <a name="result-types"></a>结果类型  
 任何包含 Null 值的有效数据类型。  
  
## <a name="remarks"></a>注释  
 如果参数为 Null，则 NULL 返回的结果为 Null。  
  
 请求某些数据类型的 Null 值时需要提供参数。 下表列出了这些数据类型及其参数。  
  
|数据类型|参数|示例|  
|---------------|---------------|-------------|  
|DT_STR|*charcount*<br /><br /> *codepage*|(DT_STR,30,1252) 将 30 个字符转换为使用 1252 代码页的 DT_STR 数据类型。|  
|DT_WSTR|*charcount*|(DT_WSTR,20) 将 20 个字符转换为 DT_WSTR 数据类型。|  
|DT_BYTES|*bytecount*|(DT_BYTES,50) 将 50 个字节的数据转换为 DT_BYTES 数据类型。|  
|DT_DECIMAL|*小数位数*|(DT_DECIMAL,2) 将数值转换为带 2 位小数的 DT_DECIMAL 数据类型。|  
|DT_NUMERIC|*精度*<br /><br /> *小数位数*|(DT_NUMERIC,10,3) 将数值转换为带 3 位小数且精度为 10 的 DT_NUMERIC 数据类型。|  
|DT_TEXT|*codepage*|(DT_TEXT,1252) 将值转换为使用 1252 代码页的 DT_TEXT 数据类型。|  
  
## <a name="expression-examples"></a>表达式示例  
 以下示例将返回下列数据类型的 Null 值：DT_STR、DT_DATE 和 DT_BOOL。  
  
```  
NULL(DT_STR,10,1252)  
NULL(DT_DATE)  
NULL(DT_BOOL)  
```  
  
## <a name="see-also"></a>另请参阅  
 [ISNULL（SSIS 表达式）](../../integration-services/expressions/isnull-ssis-expression.md)   
 [函数（SSIS 表达式）](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
