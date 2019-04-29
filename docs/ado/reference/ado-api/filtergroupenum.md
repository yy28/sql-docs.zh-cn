---
title: FilterGroupEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- FilterGroupEnum
helpviewer_keywords:
- FilterGroupEnum enumeration [ADO]
ms.assetid: b22e725e-84bd-4286-a070-290c278c3783
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 89cab313736a8d5acf2f7796ea79fb5649f85ab2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63028125"
---
# <a name="filtergroupenum"></a>FilterGroupEnum
指定要从筛选的记录的组[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
|常量|ReplTest1|Description|  
|--------------|-----------|-----------------|  
|**adFilterAffectedRecords**|2|用于查看仅受影响的最后一个的记录的筛选器[删除](../../../ado/reference/ado-api/delete-method-ado-recordset.md)，[重新同步](../../../ado/reference/ado-api/resync-method.md)， [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)，或者[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)调用。|  
|**adFilterConflictingRecords**|5|用于查看失败的最后的批处理更新的记录的筛选器。|  
|**adFilterFetchedRecords**|3|用于查看当前缓存中的记录的筛选器-即，要从数据库中检索记录的最后一个调用的结果。|  
|**adFilterNone**|0|删除当前筛选器并还原所有记录以进行查看。|  
|**adFilterPendingRecords**|1|查看仅记录的筛选器的已更改但尚未发送到服务器。 仅适用于批更新模式。|  
  
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
