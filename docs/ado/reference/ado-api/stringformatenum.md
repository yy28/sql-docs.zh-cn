---
description: StringFormatEnum
title: StringFormatEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- StringFormatEnum
helpviewer_keywords:
- StringFormatEnum enumeration [ADO]
ms.assetid: 28f7d1ec-092b-4323-a39d-d3f882c6c81a
author: rothja
ms.author: jroth
ms.openlocfilehash: 90c6214caa0adc1c11cdc0660b65795624919e51
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777136"
---
# <a name="stringformatenum"></a>StringFormatEnum
指定以字符串形式检索 [记录集](./recordset-object-ado.md) 时的格式。  
  
|返回的常量|Value|说明|  
|--------------|-----------|-----------------|  
|**adClipString**|2|按 *RowDelimiter*、 *ColumnDelimiter*和 *NullExpr*分隔行。 [GetString](./getstring-method-ado.md)方法的这三个参数仅对**adClipString**的*StringFormat*有效。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 Package： **.com. 数据**  
  
|返回的常量|  
|--------------|  
|AdoEnums.StringFormat.CLIPSTRING|  
  
## <a name="applies-to"></a>适用于  
 [GetString 方法 (ADO)](./getstring-method-ado.md)