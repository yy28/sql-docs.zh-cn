---
title: "Cancel 方法 (RDS) |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords:
- Cancel method [RDS]
ms.assetid: 560b5b3d-fba9-4275-8920-9c3e186134f7
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 870eeb951d945dd1d24ce35d89156be1971feb26
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="cancel-method-rds"></a>Cancel 方法 (RDS)
取消执行的挂起异步方法调用。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性手册](https://www.microsoft.com/en-us/download/details.aspx?id=27416)有关详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>语法  
  
```  
  
RDS.DataControl.Cancel  
```  
  
## <a name="remarks"></a>注释  
 当调用**取消**， [ReadyState](../../../ado/reference/rds-api/readystate-property-rds.md)自动设置为**adcReadyStateLoaded**，和[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)将为空。  
  
## <a name="applies-to"></a>适用范围  
 [DataControl 对象 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另请参阅  
 [取消方法示例 (VBScript)](../../../ado/reference/rds-api/cancel-method-example-vbscript.md)   
 [Cancel 方法 (ADO)](../../../ado/reference/ado-api/cancel-method-ado.md)   
 [执行方法 (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [正在执行方法 (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [正在执行方法 (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [ExecuteOptions 属性 (RDS)](../../../ado/reference/rds-api/executeoptions-property-rds.md)



