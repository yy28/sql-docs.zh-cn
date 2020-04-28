---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 85bef64902f014e7b5269d6df328128bc8fe8d6e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "67937885"
---
# <a name="stringformatenum"></a>StringFormatEnum
指定以字符串形式检索[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)时的格式。  
  
|Constant|值|说明|  
|--------------|-----------|-----------------|  
|**adClipString**|2|按*RowDelimiter*、 *ColumnDelimiter*和*NullExpr*分隔行。 [GetString](../../../ado/reference/ado-api/getstring-method-ado.md)方法的这三个参数仅对**adClipString**的*StringFormat*有效。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 Package： **.com. 数据**  
  
|Constant|  
|--------------|  
|AdoEnums.StringFormat.CLIPSTRING|  
  
## <a name="applies-to"></a>应用于  
 [GetString 方法 (ADO)](../../../ado/reference/ado-api/getstring-method-ado.md)
