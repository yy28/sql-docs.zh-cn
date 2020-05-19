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
author: rothja
ms.author: jroth
ms.openlocfilehash: a53d2c64e961c1b46b2d170de712493cc06f3910
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82756240"
---
# <a name="resyncenum"></a>ResyncEnum
指定是否通过调用[Resync](../../../ado/reference/ado-api/resync-method.md)覆盖基础值。  
  
|返回的常量|值|说明|  
|--------------|-----------|-----------------|  
|**adResyncAllValues**|2|默认。 覆盖数据，挂起的更新被取消。|  
|**adResyncUnderlyingValues**|1|不会覆盖数据，也不会取消挂起的更新。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 Package： **.com. 数据**  
  
|返回的常量|  
|--------------|  
|AdoEnums.Resync.ALLVALUES|  
|AdoEnums.Resync.UNDERLYINGVALUES|  
  
## <a name="applies-to"></a>应用于  
 [重新同步方法](../../../ado/reference/ado-api/resync-method.md)
