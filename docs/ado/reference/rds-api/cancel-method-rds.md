---
title: Cancel 方法（RDS） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Cancel method [RDS]
ms.assetid: 560b5b3d-fba9-4275-8920-9c3e186134f7
author: rothja
ms.author: jroth
ms.openlocfilehash: d9d8c0a478fd21c924752e6ebccc72767f8050f8
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82746402"
---
# <a name="cancel-method-rds"></a>Cancel 方法 (RDS)
取消执行挂起的异步方法调用。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，Windows 操作系统中不再包含 RDS 服务器组件（有关详细信息，请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)）。 在 Windows 的未来版本中将删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>语法  
  
```  
  
RDS.DataControl.Cancel  
```  
  
## <a name="remarks"></a>备注  
 调用**Cancel**时， [ReadyState](../../../ado/reference/rds-api/readystate-property-rds.md)会自动设置为**adcReadyStateLoaded**，并且[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)将为空。  
  
## <a name="applies-to"></a>应用于  
 [DataControl 对象 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另请参阅  
 [Cancel 方法示例（VBScript）](../../../ado/reference/rds-api/cancel-method-example-vbscript.md)   
 [Cancel 方法（ADO）](../../../ado/reference/ado-api/cancel-method-ado.md)   
 [CancelBatch 方法（ADO）](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [CancelUpdate 方法（ADO）](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [CancelUpdate 方法（RDS）](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [ExecuteOptions 属性 (RDS)](../../../ado/reference/rds-api/executeoptions-property-rds.md)


