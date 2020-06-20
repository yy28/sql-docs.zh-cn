---
title: SQL Server 配置管理器帮助 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Configuration Manager, help
ms.assetid: 6e909911-39a6-469b-b22a-3afdfd08a30b
author: stevestein
ms.author: sstein
ms.openlocfilehash: e72dc4e7e589359d59d16ea7eae8a131689045d3
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85000675"
---
# <a name="sql-server-configuration-manager-help"></a>SQL Server 配置管理器帮助
  使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器可以配置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务和网络连接。 若要创建或管理数据库对象、配置安全性以及编写 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查询，请使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 有关 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的详细信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书。  
  
 本节包含了按 F1 后看到的有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器中各对话框的帮助主题。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器无法配置 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 之前的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本。  
  
## <a name="services"></a>服务  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器管理与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]相关的服务。 尽管其中许多任务可以使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 服务对话框来完成，但值得注意的是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器还可以对其管理的服务执行更多的操作（例如，在服务帐户更改后应用正确的权限）。 使用标准的 Windows 服务对话框配置任何 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务都可能会造成服务无法正常工作。  
  
 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器可以完成下列服务任务：  
  
-   启动、停止和暂停服务  
  
-   将服务配置为自动启动或手动启动，禁用服务，或者更改其他服务设置  
  
-   更改 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务所使用的帐户的密码  
  
-   使用跟踪标志（命令行参数）启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   查看服务的属性  
  
## <a name="sql-server-network-configuration"></a>SQL Server 网络配置  
 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器可以完成下列与此计算机上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务相关的任务：  
  
-   启用或禁用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 网络协议  
  
-   配置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 网络协议  
  
> [!NOTE]  
>  有关如何配置协议和连接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的简短教程，请参阅 [教程：数据库引擎入门](../../relational-databases/tutorial-getting-started-with-the-database-engine.md)。  
  
## <a name="sql-server-native-client-configuration"></a>SQL Server Native Client 配置  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 客户端通过使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 网络库连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器可以完成下列与此计算机上的客户端应用程序相关的任务：  
  
-   对于此计算机上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 客户端应用程序，指定连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例时的协议顺序。  
  
-   配置客户端连接协议。  
  
-   对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 客户端应用程序，创建 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的别名，使客户端能够使用自定义连接字符串进行连接。  
  
 有关这些任务的详细信息，请参阅每个任务的 F1 帮助。  
  
#### <a name="to-open-sql-server-configuration-manager"></a>打开 SQL Server 配置管理器  
  
-   在“开始”**** 菜单上，依次指向“所有程序”****、“Microsoft SQL Server”****（版本）、“配置工具”****，然后单击“SQL Server 配置管理器”****。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 服务](../../../2014/tools/configuration-manager/sql-server-services.md)   
 [SQL Server 网络配置](sql-server-network-configuration.md)   
 [SQL Native Client 11.0 配置](../../../2014/tools/configuration-manager/sql-native-client-11-0-configuration.md)   
 [选择网络协议](../../../2014/tools/configuration-manager/choosing-a-network-protocol.md)  
  
  
