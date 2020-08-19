---
description: StayInSync 属性
title: StayInSync 属性 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 7bd35cbd24dadef9d6a9468f65bc85f95169d0cb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88441879"
---
# <a name="stayinsync-property"></a>StayInSync 属性
指示在分层 [记录集](../../../ado/reference/ado-api/recordset-object-ado.md) 对象中，对基础子记录的引用 (即，该 *章节*) 父行位置发生更改时所做的更改。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回一个 **布尔** 值。 默认值为 **True**。 如果 **为 True**，则当父 **记录集** 对象更改行位置时，将更新该章节;如果 **为 False**，则即使父 **记录集** 对象已更改行位置，本章仍将继续引用前一章节中的数据。  
  
## <a name="remarks"></a>备注  
 此属性适用于分层记录集（例如[OLE DB 的 Microsoft 数据定形服务](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)支持的层次记录集），并且必须在检索子**记录集**之前对父**记录**集进行设置。 此属性可简化层次记录集导航。  
  
## <a name="applies-to"></a>适用于  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [StayInSync 属性示例 (VB) ](../../../ado/reference/ado-api/stayinsync-property-example-vb.md)   
 [适用于 OLE DB (ADO 服务提供商的 Microsoft 数据定形服务) ](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)
