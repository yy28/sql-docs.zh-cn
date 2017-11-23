---
title: "ResyncEnum |Microsoft 文档"
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
f1_keywords: ResyncEnum
helpviewer_keywords: ResyncEnum enumeration [ADO]
ms.assetid: d3df2c90-e570-4c40-a79a-25b3448a009c
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8f7ad5525f2f9e7ce7e915b97d397d3d7d372a27
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="resyncenum"></a>ResyncEnum
指定基础值将被调用的覆盖[重新同步](../../../ado/reference/ado-api/resync-method.md)。  
  
|常量|值|Description|  
|--------------|-----------|-----------------|  
|**adResyncAllValues**|2|默认值。 将覆盖数据，并且取消挂起的更新。|  
|**adResyncUnderlyingValues**|1|不会覆盖数据，并且未取消挂起的更新。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 包： **com.ms.wfc.data**  
  
|常量|  
|--------------|  
|AdoEnums.Resync.ALLVALUES|  
|AdoEnums.Resync.UNDERLYINGVALUES|  
  
## <a name="applies-to"></a>适用范围  
 [重新同步方法](../../../ado/reference/ado-api/resync-method.md)
