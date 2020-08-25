---
description: FilterGroupEnum
title: FilterGroupEnum |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 7552eb4b069b2cd2adc33e0bff25f23d918468c2
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/24/2020
ms.locfileid: "88775286"
---
# <a name="filtergroupenum"></a>FilterGroupEnum
指定要从 [记录集中](./recordset-object-ado.md)筛选的一组记录。  
  
|返回的常量|Value|说明|  
|--------------|-----------|-----------------|  
|**adFilterAffectedRecords**|2|用于仅查看受上次 [删除](./delete-method-ado-recordset.md)、重新 [同步](./resync-method.md)、 [UpdateBatch](./updatebatch-method.md)或 [CancelBatch](./cancelbatch-method-ado.md) 调用影响的记录的筛选器。|  
|**adFilterConflictingRecords**|5|用于查看上次批处理更新失败的记录的筛选器。|  
|**adFilterFetchedRecords**|3|用于查看当前缓存中的记录的筛选器，即，最后一次调用的结果是从数据库中检索记录。|  
|**adFilterNone**|0|删除当前筛选器并还原所有记录以供查看。|  
|**adFilterPendingRecords**|1|用于仅查看已更改但尚未发送到服务器的记录的筛选器。 仅适用于批处理更新模式。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 Package： **.com. 数据**  
  
|返回的常量|  
|--------------|  
|AdoEnums.FilterGroup.AFFECTEDRECORDS|  
|AdoEnums.FilterGroup.CONFLICTINGRECORDS|  
|AdoEnums.FilterGroup.FETCHEDRECORDS|  
|AdoEnums. FilterGroup|  
|AdoEnums.FilterGroup.PENDINGRECORDS|  
  
## <a name="applies-to"></a>适用于  
 [Filter 属性](./filter-property.md)