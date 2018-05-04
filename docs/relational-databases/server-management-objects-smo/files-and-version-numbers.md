---
title: 文件和版本号 |Microsoft 文档
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: smo
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, versions
- components [SMO]
- files [SMO], components
- SMO [SQL Server], versions
- versions [SMO]
ms.assetid: 510907b6-e7a9-41bd-b892-d6d99a5118e1
caps.latest.revision: 34
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: b4833d716821b64a890815e2fa650caf6c665d46
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="files-and-version-numbers"></a>文件和版本号
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  所有必需 Microsoft.SqlServer.SqlManagementObjects NuGet 包中包含 SQL Server 管理对象 (SMO) 组件。 SMO 实现于几个托管程序集中。 您可以在客户端或服务器上开发 SMO 应用程序。  

>>[!Important]
SMO 程序集的文件版本显示为主要。**0**。Build.Revision。 但嵌入程序集版本为主要。**100**。Build.Revision。 这样做是为了分开 SMO 在每个应用程序中使用的版本，因此对其中一个更新不会影响任何其他。
>>
>>因此你应该**不**安装到全局程序集缓存 (GAC) 中的这些版本的程序集。 这样可能会导致其他应用程序，如[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Management Studio 中，若要中断。 
  
|文件|Description|  
|-----------|-----------------|  
|Microsoft.SqlServer.ConnectionInfo.dll|包含对连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的支持。|  
|Microsoft.SqlServer.ServiceBrokerEnum.dll|包含对编写 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Service Broker 的支持。 这仅在访问 Service Broker 的程序中是必需的。|  
|Microsoft.SqlServer.Smo.dll|包含大多数 SMO 类。|  
|Microsoft.SqlServer.SmoExtended.dll<br /><br /> Microsoft.SqlServer.Management.Sdk.Sfc.dll<br /><br /> Microsoft.SqlServer.SqlEnum.dll|包含对 SMO 类的支持。|  
|Microsoft.SqlServer.WmiEnum.dll|包含 Windows Management Instrumentation (WMI) 提供程序类。 这仅对使用 WMI 提供程序类的程序是必需的。|  
|Microsoft.SqlServer.RegSvrEnum.dll|包含注册服务器类。 这仅对使用注册服务器类的程序是必需的。|  
  
  
