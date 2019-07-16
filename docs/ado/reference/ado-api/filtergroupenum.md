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
ms.openlocfilehash: 97add08a1d656e8c163600bb0ea8dda7fca264b5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67932644"
---
# <a name="filtergroupenum"></a>FilterGroupEnum
指定要从筛选的记录的组[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
|常量|ReplTest1|描述|  
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
