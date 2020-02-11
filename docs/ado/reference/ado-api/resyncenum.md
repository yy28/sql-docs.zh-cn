---
title: ResyncEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ResyncEnum
helpviewer_keywords:
- ResyncEnum enumeration [ADO]
ms.assetid: d3df2c90-e570-4c40-a79a-25b3448a009c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4a872ee5f4af49d9fbe97621a5d2549fd9472202
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67931248"
---
# <a name="resyncenum"></a>ResyncEnum
指定是否通过调用[Resync](../../../ado/reference/ado-api/resync-method.md)覆盖基础值。  
  
|一直|值|说明|  
|--------------|-----------|-----------------|  
|**adResyncAllValues**|2|默认值。 覆盖数据，挂起的更新被取消。|  
|**adResyncUnderlyingValues**|1|不会覆盖数据，也不会取消挂起的更新。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 Package： **.com. 数据**  
  
|一直|  
|--------------|  
|AdoEnums.Resync.ALLVALUES|  
|AdoEnums.Resync.UNDERLYINGVALUES|  
  
## <a name="applies-to"></a>应用于  
 [重新同步方法](../../../ado/reference/ado-api/resync-method.md)
