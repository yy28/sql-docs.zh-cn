---
title: Stat 方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::Stat
helpviewer_keywords:
- Stat method [ADO]
ms.assetid: 99a2b2d4-e6b1-4205-b011-72d024ea7240
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 5f19d1b9ef0dc3b200a895d05728f6985544203b
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66719076"
---
# <a name="stat-method"></a>Stat 方法
检索有关的信息[Stream](../../../ado/reference/ado-api/stream-object-ado.md)对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
Long stream.Stat(StatStg, StatFlag)  
```  
  
## <a name="return-value"></a>返回值  
 一个**长**值，该值指示操作的状态。  
  
#### <a name="parameters"></a>Parameters  
 *StatStg*  
 STATSTG 结构，它将填充有关流的信息。 实现**Stat** ADO Stream 对象使用的方法不填写所有的结构字段。  
  
 *StatFlag*  
 指定此方法不返回的某些成员在 STATSTG 结构中，从而节省内存分配操作。 值取自 STATFLAG 枚举。 STATFLAG 枚举具有两个值  
  
|常量|ReplTest1|  
|--------------|-----------|  
|STATFLAG_DEFAULT|0|  
|STATFLAG_NONAME|1|  
  
## <a name="remarks"></a>备注  
 Stat 方法 ADO Stream 对象实现的版本将填充 STATSTG 结构的以下字段：  
  
 *pwcsName*  
 未指定包含的流，如果有可用和 StatFlag 值 STATFLAG_NONAME 名称的字符串。  
  
 *cbSize*  
 以字节为单位的流或字节数组中指定的大小。  
  
 *mtime*  
 指示此存储、 流或字节数组的上次修改时间。  
  
 *ctime*  
 指示此存储、 流或字节数组的创建时间。  
  
 *atime*  
 指示此存储、 流或字节数组的上次访问时间。  
  
 如果 STATFLAG_NONAME StatFlag 参数中指定，则不返回的流的名称。  
  
 如果 STATFLAG_NONAME StatFlag 参数中未指定，并且不没有可用于当前流的任何名称，此值将为 E_NOTIMPL。  
  
## <a name="applies-to"></a>适用范围  
 [流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
