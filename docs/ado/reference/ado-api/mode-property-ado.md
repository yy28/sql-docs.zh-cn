---
title: 模式属性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::Mode
- _Stream::Mode
- _Record::Mode
helpviewer_keywords:
- Mode property [ADO]
ms.assetid: 808661eb-0d7c-4e6d-8e40-9dc3bef3d77a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bc5b2e2bce410309656bad5591a3df90781cc8bc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67932226"
---
# <a name="mode-property-ado"></a>Mode 属性 (ADO)
指示在中修改数据的可用权限[连接](../../../ado/reference/ado-api/connection-object-ado.md)，[记录](../../../ado/reference/ado-api/record-object-ado.md)，或[Stream](../../../ado/reference/ado-api/stream-object-ado.md)对象。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回[ConnectModeEnum](../../../ado/reference/ado-api/connectmodeenum.md)值。 默认值为**连接**是**adModeUnknown**。 默认值为**记录**对象是**adModeRead**。 默认值为**Stream**与基础源相关联 (使用 URL 作为源，或为默认打开**Stream**的**记录**) 是**adModeRead**。 默认值为**Stream**未关联与基础源 （在内存中实例化） 是**adModeUnknown**。  
  
## <a name="remarks"></a>备注  
 使用**模式下**属性来设置或返回提供程序在当前连接上使用的访问权限。 可以设置**模式下**属性时，才**连接**对象已关闭。  
  
 有关**Stream**对象，如果未指定访问模式，它从用于打开的源继承**Stream**对象。 例如，如果**Stream**从打开**记录**对象，默认情况下与相同的模式中打开**记录**。  
  
 此属性是读/写，而该对象已关闭，只读的该对象处于打开状态时。  
  
> [!NOTE]
>  **远程数据服务使用情况**客户端上使用时**连接**对象，**模式**属性只能设置为**adModeUnknown**。  
  
## <a name="applies-to"></a>适用范围  
  
||||  
|-|-|-|  
|[连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[记录对象 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|[流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|  
  
## <a name="see-also"></a>请参阅  
 [IsolationLevel 和 Mode 属性示例 (VB)](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vb.md)   
 [IsolationLevel 和 Mode 属性示例 （VC + +）](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vc.md)   
