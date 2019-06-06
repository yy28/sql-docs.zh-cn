---
title: ReadyState 属性 (RDS) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: e71447143e08ebf117b6fe0eab002569ec48d020
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66694876"
---
# <a name="readystate-property-rds"></a>ReadyState 属性 (RDS)
指示的进度[DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)检索到的数据对象及其[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回以下值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**adcReadyStateLoaded**|仍在执行当前查询和已提取的任何行。 **DataControl**对象的**记录集**不是可供使用。|  
|**adcReadyStateInteractive**|一组初始检索当前查询的行的已存储在**DataControl**对象的**记录集**和可供使用。 仍在获取剩余行。|  
|**adcReadyStateComplete**|检索当前查询的所有行都存储在**DataControl**对象的**记录集**和可供使用。<br /><br /> 此状态也将存在，如果操作中止，因为出现错误，或如果**记录集**对象未初始化。|  
  
> [!NOTE]
>  使用这些常量在每个客户端的可执行文件必须提供其声明。 您可以剪切并粘贴您要从文件 Adcvbs.inc，位于 RDS 库的默认安装文件夹中的常量声明。  
  
## <a name="remarks"></a>备注  
 使用[onReadyStateChange](../../../ado/reference/rds-api/onreadystatechange-event-rds.md)事件来监视中的更改**ReadyState**异步查询操作过程中的属性。 这是定期检查属性的值比效率更高。  
  
 如果异步操作，期间出错**ReadyState**属性更改为**adcReadyStateComplete**，则[状态](../../../ado/reference/ado-api/state-property-ado.md)属性从更改**adStateExecuting**到**adStateClosed**，并**记录集**对象[值](../../../ado/reference/ado-api/value-property-ado.md)属性仍将*执行任何操作*.  
  
## <a name="applies-to"></a>适用范围  
 [DataControl 对象 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>请参阅  
 [ReadyState 属性示例 (VBScript)](../../../ado/reference/rds-api/readystate-property-example-vbscript.md)   
 [Cancel 方法 (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)   
 [ExecuteOptions 属性 (RDS)](../../../ado/reference/rds-api/executeoptions-property-rds.md)


