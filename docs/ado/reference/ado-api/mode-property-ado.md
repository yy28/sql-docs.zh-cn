---
title: Mode 属性（ADO） |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 3487463bf4a13cc97cbc7cd031e18cef5dccb2a7
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/28/2020
ms.locfileid: "87242637"
---
# <a name="mode-property-ado"></a>Mode 属性 (ADO)
指示用于修改[连接](../../../ado/reference/ado-api/connection-object-ado.md)、[记录](../../../ado/reference/ado-api/record-object-ado.md)或[流](../../../ado/reference/ado-api/stream-object-ado.md)对象中的数据的可用权限。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回一个[ConnectModeEnum](../../../ado/reference/ado-api/connectmodeenum.md)值。 **连接**的默认值为**adModeUnknown**。 **记录**对象的默认值为**adModeRead**。 与基础源关联的**流**的默认值（使用 URL 作为源，或者作为**记录**的默认**流**打开）是**adModeRead**。 不与基础源（在内存中实例化）关联的**流**的默认值为**adModeUnknown**。  
  
## <a name="remarks"></a>备注  
 使用**Mode**属性可以设置或返回当前连接上的提供程序所使用的访问权限。 仅当关闭**连接**对象时，才可以设置**Mode**属性。  
  
 对于**流**对象，如果未指定访问模式，则从用于打开**流**对象的源继承。 例如，如果从**记录**对象打开流，则默认情况下，将以与**记录**相同的模式打开**流**。  
  
 当对象处于关闭状态时，此属性是可读/写的，当对象处于打开状态时，此属性为只读。  
  
> [!NOTE]
>  **远程数据服务使用情况**当在客户端**连接**对象上使用时，**模式**属性只能设置为**adModeUnknown**。  
  
## <a name="applies-to"></a>应用到  

:::row:::
    :::column:::
        [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
    :::column-end:::
    :::column:::
        [记录对象 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
    :::column-end:::
    :::column:::
        [流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>另请参阅  
 [IsolationLevel 和 Mode 属性示例（VB）](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vb.md)   
 [IsolationLevel 和 Mode 属性示例（VC + +）](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vc.md)   
