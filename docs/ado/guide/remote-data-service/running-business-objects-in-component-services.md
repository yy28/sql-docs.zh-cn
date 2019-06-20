---
title: 在组件服务中运行业务对象 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- component services in RDS [ADO]
ms.assetid: 3077d0b6-42d6-4f10-8e5d-42e6204f1109
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f64909f4f7db1f765d233878631eb90a4760531e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66704211"
---
# <a name="running-business-objects-in-component-services"></a>在组件服务中运行业务对象
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 业务对象可以是可执行文件 (.exe) 或动态链接库 (.dll)。 用于运行业务对象的配置取决于该对象是.dll 或.exe 文件：  
  
-   可以通过 DCOM 调用业务对象创建为.exe 文件。 如果这些业务对象使用通过 Internet 信息服务 (IIS)，它们是受其他封送处理的数据，这将降低客户端性能。  
  
-   创建.dll 文件可以通过 IIS，使用业务对象，因此还通过 HTTP。 它们还可通过 DCOM 只能通过组件服务，或通过 Microsoft Transaction Server，如果您使用的 Windows NT。 业务对象的 Dll 将需要通过 IIS 访问这些在 IIS 服务器计算机上注册。 有关如何配置 DCOM 上运行的 DLL 的信息，请参阅部分中，[启用 DCOM 上运行的 DLL](../../../ado/guide/remote-data-service/enabling-a-dll-to-run-on-dcom.md)。  
  
> [!NOTE]
>  通过使用作为组件服务组件实现的中间层业务对象时**GetObjectContext**， **SetComplete**，并**SetAbort**，业务对象可使用组件服务 （或 MTS，如果您使用的 Windows NT） 要在多个客户端调用之间维护其状态的上下文对象。 可以使用 DCOM，通常受信任的客户端和 intranet 中的服务器之间实现此方案。 在这种情况下， [rds。DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md)对象和[CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md)事务上下文对象替换为在客户端上的方法和**CreateInstance**方法，由**ITransactionContext**接口，并由组件服务实现。  
  
## <a name="see-also"></a>请参阅  
 [RDS 基础知识](../../../ado/guide/remote-data-service/rds-fundamentals.md)


