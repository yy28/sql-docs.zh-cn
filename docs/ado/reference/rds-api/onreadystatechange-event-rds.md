---
title: onReadyStateChange 事件（RDS） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- onReadyStateChange event [ADO]
ms.assetid: bf2ae3ac-bfe4-4709-b50a-ea7c282c3164
author: rothja
ms.author: jroth
ms.openlocfilehash: 00eb7b7084506de78262f4df2a4606c6756bbacb
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82751443"
---
# <a name="onreadystatechange-event-rds"></a>onReadyStateChange 事件 (RDS)
每当[ReadyState](../../../ado/reference/rds-api/readystate-property-rds.md)属性的值发生更改时，就会调用**onReadyStateChange**事件。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，Windows 操作系统中不再包含 RDS 服务器组件（有关详细信息，请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)）。 在 Windows 的未来版本中将删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>语法  
  
```  
  
onReadyStateChange  
```  
  
#### <a name="parameters"></a>参数  
 无。  
  
## <a name="remarks"></a>备注  
 **ReadyState**属性反映了 RDS 的进度[。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)对象，因为它将数据异步检索到其[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象中。 如果发生更改，请使用**onReadyStateChange**事件监视**ReadyState**属性中的更改。 这比定期检查属性值更有效。  
  
## <a name="applies-to"></a>应用于  
 [DataControl 对象 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另请参阅  
 [ADO 事件模型示例（VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件处理程序摘要](../../../ado/guide/data/ado-event-handler-summary.md)


