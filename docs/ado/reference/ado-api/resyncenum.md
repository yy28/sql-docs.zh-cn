---
title: ResyncEnum | Microsoft Docs
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
manager: jroth
ms.openlocfilehash: 2bc43e772ab8f1e330d393461944cb2ecd585149
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66711562"
---
# <a name="resyncenum"></a>ResyncEnum
指定基础值将覆盖通过调用[重新同步](../../../ado/reference/ado-api/resync-method.md)。  
  
|常量|ReplTest1|Description|  
|--------------|-----------|-----------------|  
|**adResyncAllValues**|2|默认值。 将覆盖数据，并且将取消挂起的更新。|  
|**adResyncUnderlyingValues**|1|不会覆盖数据，并且未取消挂起的更新。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 包： **com.ms.wfc.data**  
  
|常量|  
|--------------|  
|AdoEnums.Resync.ALLVALUES|  
|AdoEnums.Resync.UNDERLYINGVALUES|  
  
## <a name="applies-to"></a>适用范围  
 [重新同步方法](../../../ado/reference/ado-api/resync-method.md)
