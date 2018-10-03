---
title: onReadyStateChange 事件 (RDS) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 57cd3092eebaac19b953da5bbcf39b5d3ccfdcd5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47828755"
---
# <a name="onreadystatechange-event-rds"></a>onReadyStateChange 事件 (RDS)
**OnReadyStateChange**调用事件时的值[ReadyState](../../../ado/reference/rds-api/readystate-property-rds.md)属性更改。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/en-us/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>语法  
  
```  
  
onReadyStateChange  
```  
  
#### <a name="parameters"></a>Parameters  
 无。  
  
## <a name="remarks"></a>备注  
 **ReadyState**属性会反映出的进度[rds。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)对象以异步方式检索到的数据及其[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象。 使用**onReadyStateChange**事件来监视中的更改**ReadyState**属性时出现。 这是定期检查属性的值比效率更高。  
  
## <a name="applies-to"></a>适用范围  
 [DataControl 对象 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>请参阅  
 [ADO 事件模型示例 （VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件处理程序摘要](../../../ado/guide/data/ado-event-handler-summary.md)


