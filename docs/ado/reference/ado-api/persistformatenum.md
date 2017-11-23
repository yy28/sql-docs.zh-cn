---
title: "PersistFormatEnum |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: PersistFormatEnum
helpviewer_keywords: PersistFormatEnum enumeration [ADO]
ms.assetid: ebe1a2ab-e9f1-43a2-8f94-b190c9613d70
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2695db14fdbdf05aba5b0a1b14b063ff6672a928
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="persistformatenum"></a>PersistFormatEnum
指定要在其中保存格式[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
|常量|值|Description|  
|--------------|-----------|-----------------|  
|**adPersistADTG**|0|指示 Microsoft 高级数据表图 (ADTG) 格式。|  
|**adPersistADO**|1|表示将使用 ADO 自己可扩展标记语言 (XML) 格式。 此值是 xml 格式持久化记录相同，包括有关向后兼容性。|  
|**xml 格式持久化记录**|1|指示可扩展标记语言 (XML) 格式。|  
|**adPersistProviderSpecific**|2|指示提供程序将保持**记录集**使用其自己的格式。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 包： **com.ms.wfc.data**  
  
|常量|  
|--------------|  
|AdoEnums.PersistFormat.ADTG|  
|AdoEnums.PersistFormat.XML|  
  
## <a name="applies-to"></a>适用范围  
 [Save 方法](../../../ado/reference/ado-api/save-method.md)
