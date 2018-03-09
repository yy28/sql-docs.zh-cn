---
title: "SMO 命名空间 |Microsoft 文档"
ms.custom: 
ms.date: 08/02/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: smo
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- object models [SMO]
- SMO [SQL Server], namespaces
- namespaces [SMO]
- SQL Server Management Objects, namespaces
ms.assetid: 7bfabe4d-9f4c-4bc9-b998-93bd2b50ee8a
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 235af9320f130e7b5440491765c964b4fa1771de
ms.sourcegitcommit: cb2f9d4db45bef37c04064a9493ac2c1d60f2c22
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/12/2018
---
# <a name="smo-object-model-namespaces"></a>SMO 对象模型命名空间
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理对象 (SMO) 具有不同的命名空间。 不同的命名空间表示 SMO 中的不同功能区域。  
  
 在[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，SMO 程序集位于 C:\Program Files\Microsoft SQL Server\130\SDK\Assemblies\ 文件夹中。  
  
## <a name="namespaces"></a>命名空间  
 SMO 命名空间包括：  
  
|类|函数|  
|-----------|--------------|  
|<xref:Microsoft.SqlServer.Management.Smo>|包含实例类、 实用工具类和枚举用于以编程方式操作[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。|  
|<xref:Microsoft.SqlServer.Management.Common>|包含复制管理对象 (RMO) 和 SMO 共有的类，例如连接类。|  
|<xref:Microsoft.SqlServer.Management.Smo.Agent>|包含表示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理的类。|  
|<xref:Microsoft.SqlServer.Management.Smo.Wmi>|包含表示 WMI 提供程序的类。|  
|<xref:Microsoft.SqlServer.Management.Smo.RegisteredServers>|包含表示已注册的服务器的类。|  
|<xref:Microsoft.SqlServer.Management.Smo.Mail>|包含表示数据库邮件的类。|  
|<xref:Microsoft.SqlServer.Management.Smo.Broker>|包含表示 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 的类。|  
  
  
