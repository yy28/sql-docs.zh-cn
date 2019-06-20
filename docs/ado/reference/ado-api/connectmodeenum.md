---
title: ConnectModeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ConnectModeEnum
helpviewer_keywords:
- ConnectModeEnum enumeration [ADO]
ms.assetid: 3792c294-5161-4538-a908-22a5fc50b85f
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 3528034b4a87115d704e7cbbc1f9d98a36e11794
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66695676"
---
# <a name="connectmodeenum"></a>ConnectModeEnum
指定用于修改数据中的可用权限[连接](../../../ado/reference/ado-api/connection-object-ado.md)，打开[记录](../../../ado/reference/ado-api/record-object-ado.md)，或为指定值[模式](../../../ado/reference/ado-api/mode-property-ado.md)属性**记录**并[Stream](../../../ado/reference/ado-api/stream-object-ado.md)对象。  
  
|常量|ReplTest1|Description|  
|--------------|-----------|-----------------|  
|**adModeRead**|1|指示只读权限。|  
|**adModeReadWrite**|3|指示读/写权限。|  
|**adModeRecursive**|0x400000|结合使用与其他 *\*ShareDeny\** 值 (**adModeShareDenyNone**， **adModeShareDenyWrite**，或**adModeShareDenyRead**) 将传播到所有子记录的当前的共享限制**记录**。 如果它没有任何影响**记录**不具有任何子级。 如果它用于生成运行时错误**adModeShareDenyNone**仅。 但是，可以使用它与**adModeShareDenyNone**与其他值结合使用时。 例如，可以使用"**adModeRead**或者**adModeShareDenyNone**或者**adModeRecursive**"。|  
|**adModeShareDenyNone**|16|允许其他人具有任何权限打开的连接。 读取和写入访问权限都不可以向其他人拒绝。|  
|**adModeShareDenyRead**|4|防止其他人具有读取权限打开的连接。|  
|**adModeShareDenyWrite**|8|防止其他人具有写权限打开的连接。|  
|**adModeShareExclusive**|12|防止其他人打开连接。|  
|**adModeUnknown**|0|默认值。 指示尚未设置权限，或无法确定。|  
|**adModeWrite**|2|指示只写权限。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 包： **com.ms.wfc.data**  
  
|常量|  
|--------------|  
|AdoEnums.ConnectMode.READ|  
|AdoEnums.ConnectMode.READWRITE|  
|（AdoEnums.ConnectMode.RECURSIVE 没有等效项)|  
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
