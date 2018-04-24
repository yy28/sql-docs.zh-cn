---
title: CursorLocation 属性 (ADO) |Microsoft 文档
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
- Connection15::CursorLocation
- Recordset15::CursorLocation
helpviewer_keywords:
- CursorLocation property [ADO]
ms.assetid: 39c8d86e-7ee9-4182-be5e-aad5ce952f84
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4ef22aa0aa82071367e9912c31f747cacf7e5075
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="cursorlocation-property-ado"></a>CursorLocation 属性 (ADO)
指示光标服务的位置。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回**长**值，可以将设置为其中一个[CursorLocationEnum](../../../ado/reference/ado-api/cursorlocationenum.md)值。  
  
## <a name="remarks"></a>注释  
 此属性，可在各种提供程序访问的光标库中进行选择。 通常情况下，你可以使用在服务器上的客户端游标库或一个位于之间进行选择。  
  
 此属性设置会影响仅后未设置该属性建立的连接。 更改**CursorLocation**属性具有现有连接没有影响。  
  
 返回的游标[执行](../../../ado/reference/ado-api/execute-method-ado-connection.md)方法继承此设置。 **记录集**对象将自动继承此设置从其相关联的连接。  
  
 此属性为读/写上[连接](../../../ado/reference/ado-api/connection-object-ado.md)或关闭[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)，并处于打开状态以只读方式**记录集**。  
  
> [!NOTE]
>  **远程数据服务使用情况**时在客户端上使用**记录集**或**连接**对象， **CursorLocation**属性只能设置到**adUseClient**。  
  
## <a name="applies-to"></a>适用范围  
  
|||  
|-|-|  
|[连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>另请参阅  
 [附录 A：提供程序](../../../ado/guide/appendixes/appendix-a-providers.md)
