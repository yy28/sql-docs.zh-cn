---
title: ReadyState 属性 (RDS) |Microsoft 文档
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: sql
ms.prod_service: drivers
ms.component: reference
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- ReadyState property [ADO]
ms.assetid: 5be75bc7-1171-4440-a37e-c8cc6b5cd865
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0d3ee96351ee6b09c259d4dc70e11c590c222962
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="readystate-property-rds"></a>ReadyState 属性 (RDS)
指示进度的[DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)对象，如它检索到的数据及其[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性手册](https://www.microsoft.com/en-us/download/details.aspx?id=27416)有关详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回下列值之一。  
  
|“值”|Description|  
|-----------|-----------------|  
|**adcReadyStateLoaded**|仍在执行当前的查询和已提取的任何行。 **DataControl**对象的**记录集**不是可供使用。|  
|**adcReadyStateInteractive**|已存储在由当前的查询检索的行的初始集**DataControl**对象的**记录集**和可供使用。 仍在获取剩余行。|  
|**adcReadyStateComplete**|由当前的查询检索所有行都存储在**DataControl**对象的**记录集**和可供使用。<br /><br /> 如果由于错误，中止操作，或者，也将存在此状态**记录集**对象未初始化。|  
  
> [!NOTE]
>  使用这些常量每个客户端的可执行文件必须提供其声明。 你可剪切并粘贴文件 Adcvbs.inc，位于 RDS 库的默认安装文件夹中的所需的常量声明。  
  
## <a name="remarks"></a>注释  
 使用[onReadyStateChange](../../../ado/reference/rds-api/onreadystatechange-event-rds.md)事件来监视中的更改**ReadyState**属性执行异步查询操作的过程。 这是比定期检查属性的值更高效。  
  
 如果一个异步操作过程中发生错误**ReadyState**属性更改为**adcReadyStateComplete**、[状态](../../../ado/reference/ado-api/state-property-ado.md)属性更改从**adStateExecuting**到**adStateClosed**，和**记录集**对象[值](../../../ado/reference/ado-api/value-property-ado.md)属性保持*执行任何操作*.  
  
## <a name="applies-to"></a>适用范围  
 [DataControl 对象 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另请参阅  
 [ReadyState 属性示例 (VBScript)](../../../ado/reference/rds-api/readystate-property-example-vbscript.md)   
 [Cancel 方法 (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)   
 [ExecuteOptions 属性 (RDS)](../../../ado/reference/rds-api/executeoptions-property-rds.md)


