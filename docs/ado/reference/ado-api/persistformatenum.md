---
title: PersistFormatEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- PersistFormatEnum
helpviewer_keywords:
- PersistFormatEnum enumeration [ADO]
ms.assetid: ebe1a2ab-e9f1-43a2-8f94-b190c9613d70
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2a26fd370e80cb288ee62b0fc53ed6670300172e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67917617"
---
# <a name="persistformatenum"></a>PersistFormatEnum
指定保存[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)的格式。  
  
|一直|值|说明|  
|--------------|-----------|-----------------|  
|**adPersistADTG**|0|指示 Microsoft Advanced Data TableGram （ADTG）格式。|  
|**adPersistADO**|1|指示将使用 ADO 自己的可扩展标记语言（XML）格式。 此值与 adPersistXML 相同，包含它是为了向后兼容。|  
|**adPersistXML**|1|指示可扩展标记语言（XML）格式。|  
|**adPersistProviderSpecific**|2|指示提供程序将使用其自己的格式保存**记录集**。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 Package： **.com. 数据**  
  
|一直|  
|--------------|  
|AdoEnums.PersistFormat.ADTG|  
|AdoEnums. PersistFormat|  
  
## <a name="applies-to"></a>应用于  
 [Save 方法](../../../ado/reference/ado-api/save-method.md)
