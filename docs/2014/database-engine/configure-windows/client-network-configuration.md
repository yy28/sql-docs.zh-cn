---
title: 客户端网络配置 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- client configuration [SQL Server], connections
- Database Engine [SQL Server], network configurations
- connections [SQL Server], client configuration
- client connections [SQL Server], about client network connections
- client computers [SQL Server]
- client connections [SQL Server]
- network connections [SQL Server], client configuration
ms.assetid: c382eacd-0a0c-40a4-958f-9b774eb2d734
caps.latest.revision: 38
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 08c3fe4ab1df9ba768e88ab427dd597d1e083363
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36126701"
---
# <a name="client-network-configuration"></a>客户端网络配置
  借助客户端软件，客户端计算机能够连接到网络上的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。 “客户端”是前端应用程序，它使用服务器（如 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]）提供的服务。 这种应用程序所驻留的计算机称为“客户端计算机” 。  
  
 在最简单的情况下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 客户端可与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例驻留在同一计算机上。 而通常一个客户端通过网络可以连接到一个或多个远程服务器。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的客户端/服务器体系结构允许通过网络无缝地管理多个客户端和服务器。 默认的客户端配置可以满足大多数情况。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 客户端可以包括各种应用程序，例如：  
  
-   OLE DB 使用者  
  
     这些应用程序使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例。 OLE DB 访问接口在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以及将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据作为 OLE DB 行集使用的客户端应用程序之间担当中介。 **sqlcmd** 命令提示实用工具和 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]都是 OLE DB 应用程序的例子。  
  
-   ODBC 应用程序  
  
     这些应用程序包括随 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]早期版本安装的客户端实用工具（例如 **osql** 命令提示实用工具）以及使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的其他应用程序。  
  
-   DB-Library 客户端  
  
     这些应用程序包括 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **isql** 命令提示实用工具和写入 DB-Library 的客户端。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对使用 DB-Library 的客户端应用程序的支持仅限于 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 功能。  
  
> [!NOTE]  
>  尽管 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 仍然支持来自使用 DB-Library 和嵌入式 SQL API 的现有应用程序的连接，但不包含对使用这些 API 的应用程序进行编程工作所需的文件或文档。 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的未来版本将不再支持来自 DB-Library 或嵌入式 SQL 应用程序的连接。 请不要使用 DB-Library 或嵌入式 SQL 来开发新的应用程序。 修改现有的应用程序时，请删除 DB-Library 或嵌入式 SQL 的任何依赖项。 请使用 SQLClient 命名空间或诸如 OLE DB 或 ODBC 的 API，而不使用这些 API。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不包含运行这些应用程序所需的 DB-Library DLL。 若要运行 DB-Library 或嵌入式 SQL 应用程序，必须有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.5 版、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 版或 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]提供的 DB-Library DLL。  
  
 无论哪种类型的应用程序，管理客户端的主要操作都包括配置它与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]服务器组件的连接。 根据您的实际要求，客户端管理的范围可以小到输入服务器名称，大到生成自定义配置项库，以便满足各种多服务器环境。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client DLL 包含网络库并由安装程序安装。 在新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安装过程中不会启用网络协议。 升级的安装会启用以前启用的协议。 基础网络协议作为 Windows 安装的一部分（或通过“控制面板”中的“网络”）进行安装。 下列工具用于管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 客户端：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器  
  
     客户端和服务器网络组件都使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器进行管理，它组合了早期版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 网络实用工具、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 客户端网络实用工具和服务管理器。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器是一个 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 管理控制台 (MMC) 管理单元。 它还在 Windows 计算机管理器管理单元中显示为一个节点。 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器，可以启用、禁用、配置各个网络库，以及指定其优先级。  
  
-   安装  
  
     运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序可在客户端计算机上安装网络组件。 如果从命令提示符处启动安装程序，则可以在安装过程中启用或禁用各个网络库。  
  
-   ODBC 数据源管理器  
  
     通过 ODBC 数据源管理器，您可以在运行 Microsoft Windows 操作系统的计算机上创建和修改 ODBC 数据源。  
  
## <a name="in-this-section"></a>本节内容  
 [配置客户端协议](configure-client-protocols.md)  
  
 [创建或删除供客户端使用的服务器别名（SQL Server 配置管理器）](create-or-delete-a-server-alias-for-use-by-a-client.md)  
  
 [登录到 SQL Server](logging-in-to-sql-server.md)  
  
 [打开 ODBC 数据源管理器](open-the-odbc-data-source-administrator.md)  
  
 [检查 ODBC SQL Server 驱动程序版本 (Windows)](check-the-odbc-sql-server-driver-version-windows.md)  
  
## <a name="related-content"></a>相关内容  
 [服务器网络配置](server-network-configuration.md)  
  
 [管理数据库引擎服务](manage-the-database-engine-services.md)  
  
  