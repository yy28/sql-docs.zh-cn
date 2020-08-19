---
description: CursorLocation 属性 (ADO)
title: " (ADO) 的 CursorLocation 属性 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::CursorLocation
- Recordset15::CursorLocation
helpviewer_keywords:
- CursorLocation property [ADO]
ms.assetid: 39c8d86e-7ee9-4182-be5e-aad5ce952f84
author: rothja
ms.author: jroth
ms.openlocfilehash: 92567057acad1edb0a0571a0057a11a47a3c65d6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88444299"
---
# <a name="cursorlocation-property-ado"></a>CursorLocation 属性 (ADO)
指示游标服务的位置。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回一个可以设置为[CursorLocationEnum](../../../ado/reference/ado-api/cursorlocationenum.md)值之一的**Long**值。  
  
## <a name="remarks"></a>备注  
 此属性允许您在提供程序可访问的各种游标库之间进行选择。 通常，你可以选择使用客户端游标库还是位于服务器上的一个。  
  
 此属性设置只影响在设置了属性后建立的连接。 更改 **CursorLocation** 属性不会影响现有连接。  
  
 [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md)方法返回的游标继承了此设置。 **记录集** 对象将自动从其关联的连接继承此设置。  
  
 此属性在 [连接](../../../ado/reference/ado-api/connection-object-ado.md) 或关闭的 [记录集](../../../ado/reference/ado-api/recordset-object-ado.md)上是可读/写的，在打开的 **记录集中**为只读。  
  
> [!NOTE]
>  **远程数据服务使用情况** 使用客户端 **记录集** 或 **连接** 对象时，只能将 **CursorLocation** 属性设置为 **adUseClient**。  
  
## <a name="applies-to"></a>适用于  

:::row:::
    :::column:::
        [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
    :::column-end:::
    :::column:::
        [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>另请参阅  
 [附录 A：提供程序](../../../ado/guide/appendixes/appendix-a-providers.md)
