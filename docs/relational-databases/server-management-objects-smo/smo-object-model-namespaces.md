---
title: SMO 命名空间 |Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- object models [SMO]
- SMO [SQL Server], namespaces
- namespaces [SMO]
- SQL Server Management Objects, namespaces
ms.assetid: 7bfabe4d-9f4c-4bc9-b998-93bd2b50ee8a
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e5b7f7ef0f36823eb59d4c821b2b8a8b24fc716c
ms.sourcegitcommit: f3f83ef95399d1570851cd1360dc2f072736bef6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2019
ms.locfileid: "70148599"
---
# <a name="smo-object-model-namespaces"></a>SMO 对象模型命名空间
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理对象 (SMO) 具有不同的命名空间。 不同的命名空间表示 SMO 中的不同功能区域。  
  
 在[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中, SMO 程序集位于 C:\Program Files\Microsoft SQL Server\130\SDK\Assemblies\ 文件夹中。  
  
## <a name="namespaces"></a>命名空间  
 SMO 命名空间包括：  
  
|类|Functions|  
|-----------|--------------|  
|<xref:Microsoft.SqlServer.Management.Smo>|包含用于以编程方式操作[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的实例类、实用工具类和枚举。|  
|<xref:Microsoft.SqlServer.Management.Common>|包含复制管理对象 (RMO) 和 SMO 共有的类，例如连接类。|  
|<xref:Microsoft.SqlServer.Management.Smo.Agent>|包含表示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理的类。|  
|<xref:Microsoft.SqlServer.Management.Smo.Wmi>|包含表示 WMI 提供程序的类。|  
|<xref:Microsoft.SqlServer.Management.Smo.RegisteredServers>|包含表示已注册的服务器的类。|  
|<xref:Microsoft.SqlServer.Management.Smo.Mail>|包含表示数据库邮件的类。|  
|<xref:Microsoft.SqlServer.Management.Smo.Broker>|包含表示 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 的类。|  
  
  
