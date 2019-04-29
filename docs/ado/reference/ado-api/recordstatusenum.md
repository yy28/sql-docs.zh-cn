---
title: RecordStatusEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RecordStatusEnum
helpviewer_keywords:
- RecordStatusEnum enumeration [ADO]
ms.assetid: 506fdd70-4452-4e83-95d5-c94311988dfa
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e91f82595c8e4f6fe07969960959a12464bf53a9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63033399"
---
# <a name="recordstatusenum"></a>RecordStatusEnum
指定[状态](../../../ado/reference/ado-api/status-property-ado-recordset.md)的批更新和其他大容量操作的记录。  
  
|常量|ReplTest1|Description|  
|--------------|-----------|-----------------|  
|**adRecCanceled**|0x100|指示由于操作被取消而不保存记录。|  
|**adRecCantRelease**|0x400|指示由于现有记录已被锁定，而不保存新记录。|  
|**adRecConcurrencyViolation**|0x800|指示由于正在使用乐观并发，而不保存记录。|  
|**adRecDBDeleted**|0x40000|指示从数据源已删除记录。|  
|**adRecDeleted**|0x4|指示记录已被删除。|  
|**adRecIntegrityViolation**|0x1000|指示由于用户违反了完整性约束，而不保存记录。|  
|**adRecInvalid**|0x10|指示由于其书签无效，而不保存记录。|  
|**adRecMaxChangesExceeded**|0x2000|指示由于过多挂起的更改，而不保存记录。|  
|**adRecModified**|0x2|指示记录已修改。|  
|**adRecMultipleChanges**|0x40|指示该记录不保存，因为它会影响多个记录。|  
|**adRecNew**|0x1|指示新记录。|  
|**adRecObjectOpen**|0x4000|指示由于与打开的存储对象发生冲突而未保存记录。|  
|**adRecOK**|0|指示已成功更新记录。|  
|**adRecOutOfMemory**|0x8000|指示由于在计算机内存不足而不保存记录。|  
|**adRecPendingChanges**|0x80|指示由于它是指挂起的插入，而不保存记录。|  
|**adRecPermissionDenied**|0x10000|指示由于用户没有足够的权限，而不保存记录。|  
|**adRecSchemaViolation**|0x20000|指示由于违反了基础数据库的结构而不保存记录。|  
|**adRecUnmodified**|0x8|指示不修改记录。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 AdoEnums.RecordStatus。  
  
 包： **com.ms.wfc.data**  
  
|常量|  
|--------------|  
|AdoEnums.RecordStatus.CANCELED|  
|AdoEnums.RecordStatus.CANTRELEASE|  
|AdoEnums.RecordStatus.CONCURRENCYVIOLATION|  
|AdoEnums.RecordStatus.DBDELETED|  
|AdoEnums.RecordStatus.DELETED|  
|AdoEnums.RecordStatus.INTEGRITYVIOLATION|  
|AdoEnums.RecordStatus.INVALID|  
|AdoEnums.RecordStatus.MAXCHANGESEXCEEDED|  
|AdoEnums.RecordStatus.MODIFIED|  
|AdoEnums.RecordStatus.MULTIPLECHANGES|  
|AdoEnums.RecordStatus.NEW|  
|AdoEnums.RecordStatus.OBJECTOPEN|  
|AdoEnums.RecordStatus.OK|  
|AdoEnums.RecordStatus.OUTOFMEMORY|  
|AdoEnums.RecordStatus.PENDINGCHANGES|  
|AdoEnums.RecordStatus.PERMISSIONDENIED|  
|AdoEnums.RecordStatus.SCHEMAVIOLATION|  
|AdoEnums.RecordStatus.UNMODIFIED|  
  
## <a name="applies-to"></a>适用范围  
 [Status 属性 （ADO 记录集）](../../../ado/reference/ado-api/status-property-ado-recordset.md)
