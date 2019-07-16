---
title: StringFormatEnum | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67937885"
---
# <a name="stringformatenum"></a>StringFormatEnum
检索时指定的格式[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)作为字符串。  
  
|常量|ReplTest1|描述|  
|--------------|-----------|-----------------|  
|**adClipString**|2|分隔行乘以*RowDelimiter*，按列*ColumnDelimiter*，和 null 值*NullExpr*。 这三个参数的[GetString](../../../ado/reference/ado-api/getstring-method-ado.md)方法是仅对于有效*StringFormat*的**adClipString**。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 包： **com.ms.wfc.data**  
  
|常量|  
|--------------|  
|AdoEnums.StringFormat.CLIPSTRING|  
  
## <a name="applies-to"></a>适用范围  
 [GetString 方法 (ADO)](../../../ado/reference/ado-api/getstring-method-ado.md)
