---
title: CursorLocation 属性 (ADO) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 344956b349e51a448a768988ff5062bfbc532562
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66698427"
---
# <a name="cursorlocation-property-ado"></a>CursorLocation 属性 (ADO)
指示游标服务的位置。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回**长**值，可以设置为之一[CursorLocationEnum](../../../ado/reference/ado-api/cursorlocationenum.md)值。  
  
## <a name="remarks"></a>备注  
 此属性可以访问该提供程序的各种游标库之间进行选择。 通常情况下，可以选择使用客户端游标库或其中一个位于服务器上。  
  
 此属性设置会影响仅后设置该属性建立的连接。 更改**CursorLocation**属性不起作用的现有连接。  
  
 通过返回的游标[Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md)方法将继承此设置。 **记录集**对象将自动继承此设置其关联的连接。  
  
 此属性为读/写上[连接](../../../ado/reference/ado-api/connection-object-ado.md)或已关闭[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)，和上一个打开只读**记录集**。  
  
> [!NOTE]
>  **远程数据服务使用情况**客户端上使用时**记录集**或**连接**对象**CursorLocation**属性只能设置为**adUseClient**。  
  
## <a name="applies-to"></a>适用范围  
  
|||  
|-|-|  
|[连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>请参阅  
 [附录 A：提供程序](../../../ado/guide/appendixes/appendix-a-providers.md)
