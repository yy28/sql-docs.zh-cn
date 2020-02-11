---
title: 具有对象的 RDS 编程模型 |Microsoft Docs
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
ms.openlocfilehash: 06bf7c811074ba70741fe77b06037f9f69c9cda4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67922462"
---
# <a name="rds-programming-model-with-objects"></a>RDS 编程模型和对象
RDS 的目标是通过诸如 IIS 这样的媒介获取和更新数据源。 编程模型指定完成此目标所需的活动序列。 对象模型指定其方法和属性影响编程模型的对象。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，Windows 操作系统中不再包含 RDS 服务器组件（有关详细信息，请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)）。 在 Windows 的未来版本中将删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 RDS 提供了执行以下一系列操作的方法：  
  
-   指定要在服务器上调用的程序，并获取从客户端（RDS）引用该程序的方法（代理）[。空间](../../../ado/reference/rds-api/dataspace-object-rds.md)）。  
  
-   调用服务器程序。 将参数传递给用于标识数据源的服务器程序和要发出的命令（proxy 或[RDS。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)）。  
  
-   服务器程序从数据源中获取[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象，通常使用 ADO。 （可选）在服务器上处理**Recordset**对象（[DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)）。  
  
-   服务器程序将最终的**记录集**对象返回到客户端应用程序（代理）。  
  
-   在客户端上，将**记录集**对象置于可由视觉对象（视觉对象和 RDS）轻松使用的窗体中 **。DataControl**）。  
  
-   对**Recordset**对象所做的更改将发送回服务器，并用于更新数据源（**RDS）。DataControl**或**RDSServer. DataFactory**）。  
  
## <a name="see-also"></a>另请参阅  
 [RDS 对象模型摘要](../../../ado/guide/remote-data-service/rds-object-model-summary.md)   
 [DataControl 对象（RDS）](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [DataFactory 对象（RDSServer）](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)   
 [空间对象（RDS）](../../../ado/reference/rds-api/dataspace-object-rds.md)   
 [RDS 方案](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [RDS 教程](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [Recordset 对象（ADO）](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [RDS 使用情况和安全性](../../../ado/guide/remote-data-service/rds-usage-and-security.md)


