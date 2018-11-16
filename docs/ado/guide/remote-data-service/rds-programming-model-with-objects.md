---
title: RDS 编程模型和对象 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS programming model [ADO]
- RDS objects [ADO]
ms.assetid: 07ce0ef0-72f1-48f4-823d-1b65d28c0926
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b60f402cdc7ba861a0d0550a92d16fa7dd1f59b7
ms.sourcegitcommit: 1a5448747ccb2e13e8f3d9f04012ba5ae04bb0a3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/12/2018
ms.locfileid: "51557845"
---
# <a name="rds-programming-model-with-objects"></a>RDS 编程模型和对象
RDS 的目标是获得访问权限并更新数据源通过 IIS 等中介。 编程模型指定来实现此目标所需的活动序列。 对象模型指定其方法和属性会影响编程模型的对象。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 RDS 提供了方法来执行以下操作序列：  
  
-   指定的服务器上，要调用的程序并获取方式 （代理） 来引用它从客户端 ([rds。数据空间](../../../ado/reference/rds-api/dataspace-object-rds.md))。  
  
-   调用服务器程序。 将参数传递给服务器程序，用于标识数据源和要发出的命令 (代理或[rds。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md))。  
  
-   服务器程序获得[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)从数据源，通常通过使用 ADO 对象。 （可选）**记录集**在服务器上处理对象 ([提高](../../../ado/reference/rds-api/datafactory-object-rdsserver.md))。  
  
-   服务器程序将返回最后一个**记录集**到客户端应用程序 （代理） 的对象。  
  
-   在客户端**记录集**对象放到可以轻松地使用由 visual 控件的窗体 (可视控件和**rds。DataControl**)。  
  
-   将更改为**记录集**发送回发到服务器和用于更新数据源对象 (**rds。DataControl**或**提高**)。  
  
## <a name="see-also"></a>请参阅  
 [RDS 对象模型摘要](../../../ado/guide/remote-data-service/rds-object-model-summary.md)   
 [DataControl 对象 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [DataFactory 对象 (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)   
 [DataSpace 对象 (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)   
 [RDS 方案](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [RDS 教程](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [RDS 使用情况和安全性](../../../ado/guide/remote-data-service/rds-usage-and-security.md)


