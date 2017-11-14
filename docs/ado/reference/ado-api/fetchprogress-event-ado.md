---
title: "FetchProgress 事件 (ADO) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- FetchProgress
- Recordset::FetchProgress
helpviewer_keywords:
- FetchProgress event [ADO]
ms.assetid: 301716fd-81fc-40eb-8a04-221ef7ab410e
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 606e91ca69d981cf4c1396109f0114ce0244dc3b
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="fetchprogress-event-ado"></a>FetchProgress 事件 (ADO)
**FetchProgress**定期在较长的异步操作以报告更多的行数当前已经检索到过程中调用事件[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
FetchProgress Progress, MaxProgress, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parameters  
 *进度*  
 A**长**值，该值指示当前提取操作检索到的记录数。  
  
 *MaxProgress*  
 A**长**希望检索值，该值指示最大记录数。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)状态值。  
  
 *pRecordset*  
 A**记录集**是正在数据库中检索的记录的对象的对象。  
  
## <a name="remarks"></a>注释  
 使用时**FetchProgress**其中的子**记录集**，请注意，*进度*和*MaxProgress*派生参数值从基础[游标服务](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)行集。 返回的值表示基础的行集，而不仅仅是当前章节中的记录数中的记录的总数。  
  
> [!NOTE]
>  若要使用**FetchProgress**与 Microsoft Visual Basic 中，Visual Basic 6.0 或更高版本是所需。  
  
## <a name="see-also"></a>另请参阅  
 [ADO 事件模型示例 （VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件处理程序摘要](../../../ado/guide/data/ado-event-handler-summary.md)

