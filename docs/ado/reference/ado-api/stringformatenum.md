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
author: rothja
ms.author: jroth
ms.openlocfilehash: 67814e1236bc10e9b008d1684586796dd62950b4
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759553"
---
# <a name="stringformatenum"></a>StringFormatEnum
指定以字符串形式检索[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)时的格式。  
  
|返回的常量|值|说明|  
|--------------|-----------|-----------------|  
|**adClipString**|2|按*RowDelimiter*、 *ColumnDelimiter*和*NullExpr*分隔行。 [GetString](../../../ado/reference/ado-api/getstring-method-ado.md)方法的这三个参数仅对**adClipString**的*StringFormat*有效。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 Package： **.com. 数据**  
  
|返回的常量|  
|--------------|  
|AdoEnums.StringFormat.CLIPSTRING|  
  
## <a name="applies-to"></a>应用于  
 [GetString 方法 (ADO)](../../../ado/reference/ado-api/getstring-method-ado.md)
