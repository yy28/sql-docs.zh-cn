---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 18d17e0a761fe03053ba90b8ff1ef87f3067df76
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67930749"
---
# <a name="stayinsync-property"></a>StayInSync 属性
指示以分层[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象，是否对基础的子记录的引用 (即*章*) 当父行位置更改时进行更改。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回**布尔**值。 默认值是 **True**秒。 如果 **，则返回 True**，将更新了章节，如果父**记录集**对象更改行的位置; 如果**False**，本章将继续引用在上一章中的数据即使父**记录集**对象已更改行位置。  
  
## <a name="remarks"></a>备注  
 此属性适用于分层记录集，如支持的那些[适用于 OLE DB 的 Microsoft Data Shaping 服务](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)，并且必须在父类上设置**记录集**之前子**记录集**进行检索。 此属性简化了导航分层记录集。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [StayInSync 属性示例 (VB)](../../../ado/reference/ado-api/stayinsync-property-example-vb.md)   
 [Microsoft 数据整理服务用于 OLE DB （ADO 服务提供程序）](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)
