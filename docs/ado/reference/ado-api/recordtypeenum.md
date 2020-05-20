---
title: RecordTypeEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RecordTypeEnum
helpviewer_keywords:
- RecordTypeEnum enumeration [ADO]
ms.assetid: f557e537-015d-4ba7-8a41-a6f00b366a91
author: rothja
ms.author: jroth
ms.openlocfilehash: 8b47b68b8515ea80405d6083e37a767fb5a6d21e
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82756559"
---
# <a name="recordtypeenum"></a>RecordTypeEnum
指定[记录](../../../ado/reference/ado-api/record-object-ado.md)对象的类型。  
  
|返回的常量|值|说明|  
|--------------|-----------|-----------------|  
|**adSimpleRecord**|0|指示*简单*记录（不包含子节点）。|  
|**adCollectionRecord**|1|指示*集合*记录（包含子节点）。|  
|**adRecordUnknown**|-1|指示此**记录**的类型是未知的。|  
|**adStructDoc**|2|指示表示 COM 结构化文档的一种特殊类型的*集合*记录。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 这些常量没有 ADO/WFC 等效项。  
  
## <a name="applies-to"></a>应用于  
 [RecordType 属性 (ADO)](../../../ado/reference/ado-api/recordtype-property-ado.md)
