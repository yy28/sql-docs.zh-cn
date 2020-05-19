---
title: ReadyState 属性（RDS） |Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- ReadyState property [ADO]
ms.assetid: 5be75bc7-1171-4440-a37e-c8cc6b5cd865
author: rothja
ms.author: jroth
ms.openlocfilehash: c5e1eb89c0e4c7dcbef736d2968a4ffd97a37b93
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82751221"
---
# <a name="readystate-property-rds"></a>ReadyState 属性 (RDS)
指示[DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)对象在其[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)对象中检索数据时的进度。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，Windows 操作系统中不再包含 RDS 服务器组件（有关详细信息，请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)）。 在 Windows 的未来版本中将删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回以下值之一。  
  
|值|说明|  
|-----------|-----------------|  
|**adcReadyStateLoaded**|当前查询仍在执行，未提取行。 **DataControl**对象的**记录集**不可用。|  
|**adcReadyStateInteractive**|当前查询检索到的初始行集已存储在**DataControl**对象的**记录集中**，可供使用。 仍在提取剩余行。|  
|**adcReadyStateComplete**|当前查询检索到的所有行都存储在**DataControl**对象的**记录集中**，可供使用。<br /><br /> 如果操作由于错误而中止，或者**记录集**对象未初始化，则也会存在此状态。|  
  
> [!NOTE]
>  每个使用这些常量的客户端可执行文件都必须为其提供声明。 你可以从文件 Adcvbs 中剪切并粘贴所需的常量声明，该文件位于 RDS 库的默认安装文件夹中。  
  
## <a name="remarks"></a>备注  
 在异步查询操作期间，使用[onReadyStateChange](../../../ado/reference/rds-api/onreadystatechange-event-rds.md)事件监视**ReadyState**属性中的更改。 这比定期检查属性值更有效。  
  
 如果在异步操作过程中发生错误，则**ReadyState**属性更改为**adcReadyStateComplete**，[状态](../../../ado/reference/ado-api/state-property-ado.md)属性从**adStateExecuting**更改为**adStateClosed**，而**Recordset**对象的[值](../../../ado/reference/ado-api/value-property-ado.md)属性则不*会。*  
  
## <a name="applies-to"></a>应用于  
 [DataControl 对象 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另请参阅  
 [ReadyState 属性示例（VBScript）](../../../ado/reference/rds-api/readystate-property-example-vbscript.md)   
 [Cancel 方法（RDS）](../../../ado/reference/rds-api/cancel-method-rds.md)   
 [ExecuteOptions 属性 (RDS)](../../../ado/reference/rds-api/executeoptions-property-rds.md)


