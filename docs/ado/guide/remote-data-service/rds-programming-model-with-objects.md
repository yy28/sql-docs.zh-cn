---
title: RDS 的编程模型和对象 |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS programming model [ADO]
- RDS objects [ADO]
ms.assetid: 07ce0ef0-72f1-48f4-823d-1b65d28c0926
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c9501b819e664e4b0841140f6b3d835773d2e2ed
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35274076"
---
# <a name="rds-programming-model-with-objects"></a>RDS 的编程模型和对象
RDS 的目标是访问和更新数据源通过如 IIS 媒介。 编程模型指定实现此目标所需的活动序列。 对象模型指定其方法和属性会影响的编程模型的对象。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性手册](https://www.microsoft.com/en-us/download/details.aspx?id=27416)有关详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 RDS 提供执行以下操作序列的方式：  
  
-   指定要在服务器上，调用程序并获取的方法 （代理） 来引用它从客户端 ([rds.DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md))。  
  
-   调用服务器程序。 将参数传递给服务器计划，用于标识数据源和要发出的命令 (代理或[rds.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md))。  
  
-   服务器计划获取[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)从数据源，通常通过使用 ADO 的对象。 （可选）**记录集**在服务器上处理对象 ([提高](../../../ado/reference/rds-api/datafactory-object-rdsserver.md))。  
  
-   服务器程序将返回最后一个**记录集**到客户端应用程序 （代理） 的对象。  
  
-   在客户端，**记录集**对象放到可以轻松地使用由 visual 控件的窗体 (可视控件和**rds.DataControl**)。  
  
-   更改为**记录集**发送回发到服务器和用于更新数据源对象 (**rds.DataControl**或**提高**)。  
  
## <a name="see-also"></a>请参阅  
 [RDS 对象模型摘要](../../../ado/guide/remote-data-service/rds-object-model-summary.md)   
 [DataControl 对象 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [DataFactory 对象 (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)   
 [DataSpace 对象 (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)   
 [RDS 方案](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [RDS 教程](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [RDS 使用情况和安全性](../../../ado/guide/remote-data-service/rds-usage-and-security.md)


