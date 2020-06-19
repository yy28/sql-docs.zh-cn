---
title: NULL（SSIS 表达式）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- NULL function
- null values [Integration Services]
ms.assetid: df144237-3fbb-41ac-8624-efd92b6522b9
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 636a51af831476b691fa6e95adbba24c6ff80585
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84969177"
---
# <a name="null-ssis-expression"></a>NULL（SSIS 表达式）
  返回请求的数据类型的 Null 值。  
  
## <a name="syntax"></a>语法  
  
```  
  
NULL(typespec)  
```  
  
## <a name="arguments"></a>参数  
 *typespec*  
 有效的数据类型。 有关详细信息，请参阅 [Integration Services 数据类型](../data-flow/integration-services-data-types.md)。  
  
## <a name="result-types"></a>结果类型  
 任何包含 Null 值的有效数据类型。  
  
## <a name="remarks"></a>备注  
 如果参数为 Null，则 NULL 返回的结果为 Null。  
  
 请求某些数据类型的 Null 值时需要提供参数。 下表列出了这些数据类型及其参数。  
  
|数据类型|参数|示例|  
|---------------|---------------|-------------|  
|DT_STR|*charcount*<br /><br /> *codepage*|(DT_STR,30,1252) 将 30 个字符转换为使用 1252 代码页的 DT_STR 数据类型。|  
|DT_WSTR|*charcount*|(DT_WSTR,20) 将 20 个字符转换为 DT_WSTR 数据类型。|  
|DT_BYTES|*bytecount*|(DT_BYTES,50) 将 50 个字节的数据转换为 DT_BYTES 数据类型。|  
|DT_DECIMAL|*scale*|(DT_DECIMAL,2) 将数值转换为带 2 位小数的 DT_DECIMAL 数据类型。|  
|DT_NUMERIC|*精度*<br /><br /> *scale*|(DT_NUMERIC,10,3) 将数值转换为带 3 位小数且精度为 10 的 DT_NUMERIC 数据类型。|  
|DT_TEXT|*codepage*|(DT_TEXT,1252) 将值转换为使用 1252 代码页的 DT_TEXT 数据类型。|  
  
## <a name="expression-examples"></a>表达式示例  
 以下示例将返回下列数据类型的 Null 值：DT_STR、DT_DATE 和 DT_BOOL。  
  
```  
NULL(DT_STR,10,1252)  
NULL(DT_DATE)  
NULL(DT_BOOL)  
```  
  
## <a name="see-also"></a>另请参阅  
 [ISNULL（SSIS 表达式）](null-ssis-expression.md)   
 [函数（SSIS 表达式）](functions-ssis-expression.md)  
  
  
