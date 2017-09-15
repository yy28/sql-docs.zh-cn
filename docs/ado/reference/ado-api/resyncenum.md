---
title: "ResyncEnum |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- ResyncEnum
helpviewer_keywords:
- ResyncEnum enumeration [ADO]
ms.assetid: d3df2c90-e570-4c40-a79a-25b3448a009c
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5d7757a6db51b6d5d1d5f10f303cd0f614b0132a
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

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
