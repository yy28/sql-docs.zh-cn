---
title: StringFormatEnum |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- StringFormatEnum
helpviewer_keywords:
- StringFormatEnum enumeration [ADO]
ms.assetid: 28f7d1ec-092b-4323-a39d-d3f882c6c81a
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 13c4f80064a06299a6049330fcf85c8e0827e619
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="stringformatenum"></a>StringFormatEnum
指定检索时的格式[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)作为字符串。  
  
|常量|“值”|Description|  
|--------------|-----------|-----------------|  
|**adClipString**|2|分隔行乘以*RowDelimiter*，列 × *ColumnDelimiter*，和 null 值*NullExpr*。 以下三个参数[GetString](../../../ado/reference/ado-api/getstring-method-ado.md)方法是仅对有效*StringFormat*的**adClipString**。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 包： **com.ms.wfc.data**  
  
|常量|  
|--------------|  
|AdoEnums.StringFormat.CLIPSTRING|  
  
## <a name="applies-to"></a>适用范围  
 [GetString 方法 (ADO)](../../../ado/reference/ado-api/getstring-method-ado.md)
