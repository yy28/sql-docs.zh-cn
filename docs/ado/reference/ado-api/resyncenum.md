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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67931248"
---
# <a name="resyncenum"></a>ResyncEnum
指定基础值将覆盖通过调用[重新同步](../../../ado/reference/ado-api/resync-method.md)。  
  
|常量|值|描述|  
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
