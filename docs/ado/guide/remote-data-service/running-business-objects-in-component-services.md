---
title: "在组件服务中运行业务对象 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: component services in RDS [ADO]
ms.assetid: 3077d0b6-42d6-4f10-8e5d-42e6204f1109
caps.latest.revision: "17"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: df0d9faf78e4e63053e96f5513d38a31af0ca827
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="running-business-objects-in-component-services"></a>在组件服务中运行业务对象
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性手册](https://www.microsoft.com/en-us/download/details.aspx?id=27416)有关详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 业务对象可以是可执行文件 (.exe) 或动态链接库 (.dll)。 用于运行业务对象的配置取决于该对象是.dll 或.exe 文件：  
  
-   可以通过 DCOM 调用作为.exe 文件创建的业务对象。 如果这些业务对象使用通过 Internet 信息服务 (IIS)，它们是受其他封送处理的数据，这将降低客户端性能。  
  
-   创建，因为可以通过 IIS，使用.dll 文件的业务对象，因此还通过 HTTP。 它们还可通过 DCOM 只能通过组件服务，或通过 Microsoft Transaction Server，如果你使用的 Windows NT。 业务对象 Dll 将需要在对其进行访问通过 IIS 的 IIS 服务器计算机上注册。 有关如何配置在 DCOM 上运行的 DLL 的信息，请参阅明[启用 DCOM 上运行的 DLL](../../../ado/guide/remote-data-service/enabling-a-dll-to-run-on-dcom.md)。  
  
> [!NOTE]
>  通过使用作为组件服务组件实现的中间层上的业务对象时**GetObjectContext**， **SetComplete**，和**异常**，业务对象可以使用组件服务 （或 MTS，如果你使用的 Windows NT） 要跨多个客户端调用保持其状态的上下文对象。 本方案是，可以使用 DCOM，通常受信任的客户端和 intranet 中的服务器之间实现。 在这种情况下， [rds.DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md)对象和[CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md)事务上下文对象替换为在客户端的方法和**CreateInstance**方法，由**ITransactionContext**接口，并由组件服务实现。  
  
## <a name="see-also"></a>另请参阅  
 [RDS 基础知识](../../../ado/guide/remote-data-service/rds-fundamentals.md)


