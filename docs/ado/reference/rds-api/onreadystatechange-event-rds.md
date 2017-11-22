---
title: "onReadyStateChange 事件 (RDS) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords: onReadyStateChange event [ADO]
ms.assetid: bf2ae3ac-bfe4-4709-b50a-ea7c282c3164
caps.latest.revision: "16"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7912a623ac6fabbbf2460025f38e2c76238af1e9
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="onreadystatechange-event-rds"></a>onReadyStateChange 事件 (RDS)
**OnReadyStateChange**事件时调用时的值[ReadyState](../../../ado/reference/rds-api/readystate-property-rds.md)属性更改。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性手册](https://www.microsoft.com/en-us/download/details.aspx?id=27416)有关详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>语法  
  
```  
  
onReadyStateChange  
```  
  
#### <a name="parameters"></a>Parameters  
 无。  
  
## <a name="remarks"></a>注释  
 **ReadyState**属性反映的进度[rds.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)对象，如它以异步方式检索数据插入其[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象。 使用**onReadyStateChange**事件来监视中的更改**ReadyState**它们发生的任何时候的属性。 这是比定期检查属性的值更高效。  
  
## <a name="applies-to"></a>适用范围  
 [DataControl 对象 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另请参阅  
 [ADO 事件模型示例 （VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件处理程序摘要](../../../ado/guide/data/ado-event-handler-summary.md)


