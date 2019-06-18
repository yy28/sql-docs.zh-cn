---
title: ExecuteOptions 属性 (RDS) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- ExecuteOptions property [ADO], VBScript example
ms.assetid: 62a4fd88-afc3-4f1f-b978-40710a30c4e9
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 084faa615253c58d7b41214f9abfb4d3c8880bac
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66712611"
---
# <a name="executeoptions-property-rds"></a>ExecuteOptions 属性 (RDS)
指示是否启用异步执行。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回以下值之一。  
  
|常量|Description|  
|--------------|-----------------|  
|**adcExecSync**|执行的下一步刷新[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)以同步方式。|  
|**adcExecAsync**|默认值。 执行的下一步刷新**记录集**以异步方式。|  
  
> [!NOTE]
>  使用这些常量在每个可执行文件必须提供其声明。 您可以剪切并粘贴您要从文件 Adcvbs.inc，位于 RDS 库的默认安装文件夹中的常量声明。  
  
## <a name="remarks"></a>备注  
 如果**ExecuteOptions**设置为**adcExecAsync**，则此时将以异步方式执行下一步**刷新**上调用[rds。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)对象的**记录集**。  
  
 如果尝试调用[重置](../../../ado/reference/rds-api/reset-method-rds.md)，[刷新](../../../ado/reference/rds-api/refresh-method-rds.md)， [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md)， [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)，或[记录集](../../../ado/reference/rds-api/recordset-sourcerecordset-properties-rds.md)尽管可能会更改的另一个异步操作[rds。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)对象的**记录集**正在执行，就会出错。  
  
 如果在异步操作期间发生错误**rds。DataControl**对象的[ReadyState](../../../ado/reference/rds-api/readystate-property-rds.md)值从更改**adcReadyStateLoaded**到**adcReadyStateComplete**，和**记录集**属性值仍*Nothing*。  
  
## <a name="applies-to"></a>适用范围  
 [DataControl 对象 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>请参阅  
 [ExecuteOptions 和 FetchOptions 属性示例 (VBScript)](../../../ado/reference/rds-api/executeoptions-and-fetchoptions-properties-example-vbscript.md)   
 [Cancel 方法 (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)


