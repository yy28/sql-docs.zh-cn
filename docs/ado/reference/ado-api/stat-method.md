---
title: Stat 方法 |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::Stat
helpviewer_keywords:
- Stat method [ADO]
ms.assetid: 99a2b2d4-e6b1-4205-b011-72d024ea7240
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1b900386c1890d54ec61d3bfd2328f3d173c9300
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35282016"
---
# <a name="stat-method"></a>Stat 方法
有关检索信息[流](../../../ado/reference/ado-api/stream-object-ado.md)对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
Long stream.Stat(StatStg, StatFlag)  
```  
  
## <a name="return-value"></a>返回值  
 A**长**值，该值指示操作的状态。  
  
#### <a name="parameters"></a>Parameters  
 *StatStg*  
 将使用有关流的信息填充 STATSTG 结构。 实现**Stat** ADO 流对象使用的方法不填写所有字段的结构。  
  
 *StatFlag*  
 指定此方法不返回的某些成员在 STATSTG 结构中，从而节省了内存分配操作。 值，将从 STATFLAG 枚举。 STATFLAG 枚举具有两个值  
  
|常量|ReplTest1|  
|--------------|-----------|  
|STATFLAG_DEFAULT|0|  
|STATFLAG_NONAME|@shouldalert|  
  
## <a name="remarks"></a>Remarks  
 Stat 为 ADO 流对象实现的方法的版本填写 STATSTG 结构的以下字段：  
  
 *pwcsName*  
 未指定包含的流，如果有可用和 StatFlag 值 STATFLAG_NONAME 名称的字符串。  
  
 *cbSize*  
 以字节为单位的流或字节数组中指定的大小。  
  
 *mtime*  
 指示此存储、 流或字节数组的上次修改时间。  
  
 *ctime*  
 指示为此存储、 流或字节数组的创建时间。  
  
 *atime*  
 指示为此存储、 流或字节数组的上次访问时间。  
  
 如果 STATFLAG_NONAME StatFlag 参数中指定，则不会返回的流的名称。  
  
 如果 STATFLAG_NONAME 中 StatFlag 参数中，未指定，并且不没有可用于当前流的任何名称，此值将为 E_NOTIMPL。  
  
## <a name="applies-to"></a>适用范围  
 [流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
