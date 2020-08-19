---
description: ResyncEnum
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
ms.openlocfilehash: c379ca2a3f68b195c0020d0e89009d2715da5850
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442249"
---
# <a name="resyncenum"></a>ResyncEnum
指定是否通过调用 [Resync](../../../ado/reference/ado-api/resync-method.md)覆盖基础值。  
  
|返回的常量|值|描述|  
|--------------|-----------|-----------------|  
|**adResyncAllValues**|2|默认。 覆盖数据，挂起的更新被取消。|  
|**adResyncUnderlyingValues**|1|不会覆盖数据，也不会取消挂起的更新。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 Package： **.com. 数据**  
  
|返回的常量|  
|--------------|  
|AdoEnums.Resync.ALLVALUES|  
|AdoEnums.Resync.UNDERLYINGVALUES|  
  
## <a name="applies-to"></a>适用于  
 [重新同步方法](../../../ado/reference/ado-api/resync-method.md)
