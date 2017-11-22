---
title: "FilterGroupEnum |Microsoft 文档"
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
f1_keywords: FilterGroupEnum
helpviewer_keywords: FilterGroupEnum enumeration [ADO]
ms.assetid: b22e725e-84bd-4286-a070-290c278c3783
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 080b0149fcfe0df39e1efbe44a87fe6243424468
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="filtergroupenum"></a>FilterGroupEnum
指定要从筛选的记录组[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
|常量|值|Description|  
|--------------|-----------|-----------------|  
|**adFilterAffectedRecords**|2|用于查看仅由最后一个受影响的记录的筛选器[删除](../../../ado/reference/ado-api/delete-method-ado-recordset.md)，[重新同步](../../../ado/reference/ado-api/resync-method.md)， [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)，或[执行](../../../ado/reference/ado-api/cancelbatch-method-ado.md)调用。|  
|**adFilterConflictingRecords**|5|用于查看失败的最后一个批处理更新的记录的筛选器。|  
|**adFilterFetchedRecords**|3|用于查看当前的缓存中的记录的筛选器 — 也就是说，若要从数据库检索记录的最后一个调用的结果。|  
|**adFilterNone**|0|移除当前筛选器并还原所有记录以进行查看。|  
|**adFilterPendingRecords**|1|用于查看仅记录的筛选器的已更改但尚未发送到服务器。 仅适用于批处理更新模式。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 包： **com.ms.wfc.data**  
  
|常量|  
|--------------|  
|AdoEnums.FilterGroup.AFFECTEDRECORDS|  
|AdoEnums.FilterGroup.CONFLICTINGRECORDS|  
|AdoEnums.FilterGroup.FETCHEDRECORDS|  
|AdoEnums.FilterGroup.NONE|  
|AdoEnums.FilterGroup.PENDINGRECORDS|  
  
## <a name="applies-to"></a>适用范围  
 [Filter 属性](../../../ado/reference/ado-api/filter-property.md)
