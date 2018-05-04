---
title: StayInSync 属性 |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::StayInSync
- Recordset20::put_StayInSync
- Recordset20::PutStayInSync
- Recordset20::get_StayInSync
- Recordset20::GetStayInSync
helpviewer_keywords:
- StayInSync property
ms.assetid: 502d69b5-dc9a-455d-b115-a03bd39a552b
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d4e5067036aaaf36c60a134f825012fdc5facf75
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="stayinsync-property"></a>StayInSync 属性
指示在分层结构[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象、 是否对基础的子记录的引用 (即，*章*) 对父行的位置更改时，发生变化。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回**布尔**值。 默认值是 **True**秒。 如果**True**，将更新章，如果父**记录集**对象更改行位置; 如果**False**，章将继续引用上一章中的数据即使父**记录集**对象已更改行位置。  
  
## <a name="remarks"></a>注释  
 此属性应用于层次结构的记录集，如支持的那些[用于 OLE DB 的 Microsoft 数据调整服务](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)，并且必须在父类上设置**记录集**子级之前**记录集**检索。 此属性可以简化导航分层记录集。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [StayInSync 属性示例 (VB)](../../../ado/reference/ado-api/stayinsync-property-example-vb.md)   
 [调整用于 OLE DB （ADO 服务提供程序） 的服务的 Microsoft 数据](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)
