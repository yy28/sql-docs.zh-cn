---
title: FetchProgress 事件 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- FetchProgress
- Recordset::FetchProgress
helpviewer_keywords:
- FetchProgress event [ADO]
ms.assetid: 301716fd-81fc-40eb-8a04-221ef7ab410e
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 9f7b31524a6c54846072fdce8cca76189c7034ad
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66698085"
---
# <a name="fetchprogress-event-ado"></a>FetchProgress 事件 (ADO)
**FetchProgress**耗时较长的异步操作以报告更多的行数当前已检索到过程中定期调用事件[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
FetchProgress Progress, MaxProgress, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parameters  
 *进度*  
 一个**长**值，该值指示当前提取操作中检索的记录数。  
  
 *MaxProgress*  
 一个**长**需要检索值，该值指示最大记录数。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)状态值。  
  
 *pRecordset*  
 一个**记录集**是正在为其检索记录的对象的对象。  
  
## <a name="remarks"></a>备注  
 使用时**FetchProgress**具有一个子**记录集**，请注意，*进度*并*MaxProgress*派生参数值从基础[游标服务](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)行集。 返回的值表示基础行集，而不仅仅是当前的一章中的记录数中的记录的总数。  
  
> [!NOTE]
>  若要使用**FetchProgress**使用 Microsoft Visual Basic、 Visual Basic 6.0 或更高版本是所需。  
  
## <a name="see-also"></a>请参阅  
 [ADO 事件模型示例 （VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件处理程序摘要](../../../ado/guide/data/ado-event-handler-summary.md)
