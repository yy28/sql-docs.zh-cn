---
title: ConnectModeEnum |Microsoft 文档
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ConnectModeEnum
helpviewer_keywords:
- ConnectModeEnum enumeration [ADO]
ms.assetid: 3792c294-5161-4538-a908-22a5fc50b85f
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 094878a0b8289ad6347207530ca672cd0f2bd58c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="connectmodeenum"></a>ConnectModeEnum
指定在中修改数据的可用权限[连接](../../../ado/reference/ado-api/connection-object-ado.md)，打开[记录](../../../ado/reference/ado-api/record-object-ado.md)，或为指定值[模式](../../../ado/reference/ado-api/mode-property-ado.md)属性**记录**和[流](../../../ado/reference/ado-api/stream-object-ado.md)对象。  
  
|常量|“值”|Description|  
|--------------|-----------|-----------------|  
|**adModeRead**|1|指示只读权限。|  
|**adModeReadWrite**|3|指示读/写权限。|  
|**adModeRecursive**|0x400000|与其他结合使用*\*ShareDeny\** 值 (**adModeShareDenyNone**， **adModeShareDenyWrite**，或**adModeShareDenyRead**) 传播到所有子记录的当前的共享限制**记录**。 它没有任何影响，如果**记录**没有任何子级。 如果与一起使用，则会生成运行时错误**adModeShareDenyNone**仅。 但是，它可以用于**adModeShareDenyNone**时与其他值组合。 例如，你可以使用"**adModeRead**或者**adModeShareDenyNone**或者**adModeRecursive**"。|  
|**adModeShareDenyNone**|16|允许其他人具有任何权限打开的连接。 读取和写入访问权限都不可能向其他用户被拒绝。|  
|**adModeShareDenyRead**|4|防止其他人打开具有读取权限的连接。|  
|**adModeShareDenyWrite**|8|防止其他人打开具有写权限的连接。|  
|**adModeShareExclusive**|12|防止其他人打开连接。|  
|**adModeUnknown**|0|默认值。 指示权限尚未设置，或无法确定。|  
|**adModeWrite**|2|指示只写权限。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 包： **com.ms.wfc.data**  
  
|常量|  
|--------------|  
|AdoEnums.ConnectMode.READ|  
|AdoEnums.ConnectMode.READWRITE|  
|（没有 AdoEnums.ConnectMode.RECURSIVE 无等效项）|  
|AdoEnums.ConnectMode.SHAREDENYNONE|  
|AdoEnums.ConnectMode.SHAREDENYREAD|  
|AdoEnums.ConnectMode.SHAREDENYWRITE|  
|AdoEnums.ConnectMode.SHAREEXCLUSIVE|  
|AdoEnums.ConnectMode.UNKNOWN|  
|AdoEnums.ConnectMode.WRITE|  
  
## <a name="applies-to"></a>适用范围  
  
|||  
|-|-|  
|[Mode 属性 (ADO)](../../../ado/reference/ado-api/mode-property-ado.md)|[Open 方法（ADO 记录）](../../../ado/reference/ado-api/open-method-ado-record.md)|  
|[Open 方法（ADO 流）](../../../ado/reference/ado-api/open-method-ado-stream.md)|[流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|
