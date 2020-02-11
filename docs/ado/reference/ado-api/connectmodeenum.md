---
title: ConnectModeEnum |Microsoft Docs
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
ms.openlocfilehash: debf6f9dc4ac1326caf9fbf32b65f15f34a19094
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67933459"
---
# <a name="connectmodeenum"></a>ConnectModeEnum
指定可用于修改[连接](../../../ado/reference/ado-api/connection-object-ado.md)中的数据、打开[记录](../../../ado/reference/ado-api/record-object-ado.md)或为**Record**和[Stream](../../../ado/reference/ado-api/stream-object-ado.md)对象的[Mode](../../../ado/reference/ado-api/mode-property-ado.md)属性指定值的可用权限。  
  
|一直|值|说明|  
|--------------|-----------|-----------------|  
|**adModeRead**|1|指示只读权限。|  
|**adModeReadWrite**|3|指示读取/写入权限。|  
|**adModeRecursive**|0x400000|与其他* \*ShareDeny\* *值（**adModeShareDenyNone**、 **adModeShareDenyWrite**或**adModeShareDenyRead**）结合使用，以将共享限制传播到当前**记录**的所有子记录。 如果**记录**没有任何子级，则不会产生任何影响。 如果将运行时错误仅用于**adModeShareDenyNone** ，则会生成此错误。 但是，在与其他值结合使用时，可以将它与**adModeShareDenyNone**一起使用。 例如，可以使用 "**adModeRead** " 或 " **adModeShareDenyNone** " 或 " **adModeRecursive**"。|  
|**adModeShareDenyNone**|16|允许其他人打开具有任何权限的连接。 不能对其他人拒绝读取或写入访问权限。|  
|**adModeShareDenyRead**|4|阻止其他人打开具有读取权限的连接。|  
|**adModeShareDenyWrite**|8|阻止其他人打开具有写入权限的连接。|  
|**adModeShareExclusive**|12|阻止其他人打开连接。|  
|**adModeUnknown**|0|默认值。 指示权限尚未设置或无法确定。|  
|**adModeWrite**|2|指示只写权限。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 Package： **.com. 数据**  
  
|一直|  
|--------------|  
|AdoEnums. ConnectMode. READ|  
|AdoEnums. ConnectMode|  
|（没有 AdoEnums 的等效项。 ConnectMode）|  
|AdoEnums.ConnectMode.SHAREDENYNONE|  
|AdoEnums.ConnectMode.SHAREDENYREAD|  
|AdoEnums.ConnectMode.SHAREDENYWRITE|  
|AdoEnums.ConnectMode.SHAREEXCLUSIVE|  
|AdoEnums. ConnectMode. 未知|  
|AdoEnums. ConnectMode|  
  
## <a name="applies-to"></a>应用于  
  
|||  
|-|-|  
|[Mode 属性 (ADO)](../../../ado/reference/ado-api/mode-property-ado.md)|[Open 方法（ADO 记录）](../../../ado/reference/ado-api/open-method-ado-record.md)|  
|[Open 方法（ADO 流）](../../../ado/reference/ado-api/open-method-ado-stream.md)|[流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|
