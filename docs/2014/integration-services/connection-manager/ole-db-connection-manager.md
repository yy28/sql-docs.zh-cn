---
title: OLE DB 连接管理器 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB connection manager
- data sources [Integration Services], connections
- connection managers [Integration Services], OLE DB
- connections [Integration Services], OLE DB
ms.assetid: 91e3622e-4b1a-439a-80c7-a00b90d66979
caps.latest.revision: 56
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 11b88bd8144651abfed39fb5b68316abc23f09a5
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37295137"
---
# <a name="ole-db-connection-manager"></a>OLE DB 连接管理器
  OLE DB 连接管理器使包能够用 OLE DB 访问接口连接到数据源。 例如，连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 OLE DB 连接管理器可以使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 11.0 OLEDB 提供程序不支持用于多子网故障转移群集的新连接字符串关键字 (MultiSubnetFailover=True)。 有关详细信息，请参阅[SQL Server 发行说明](http://go.microsoft.com/fwlink/?LinkId=247824)和博客文章[AlwaysOn 多子网故障转移和 SSIS](http://go.microsoft.com/fwlink/?LinkId=247825)，www.mattmasson.com 上。  
  
 有若干 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 任务和数据流组件使用 OLE DB 连接管理器。 例如，OLE DB 源和 OLE DB 目标使用这种连接管理器来提取和加载数据，而执行 SQL 任务可以使用这种连接管理器来连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库以运行查询。  
  
 OLE DB 连接管理器还用于在以使用 C++ 等语言的非托管代码编写的自定义任务中访问 OLE DB 数据源。  
  
 当将一个 OLE DB 连接管理器添加到包中，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]创建的连接管理器将解析为在运行时的 OLE DB 连接，设置该连接管理器属性，并将对该连接管理器`Connections`集合包。  
  
 `ConnectionManagerType`连接管理器属性设置为`OLEDB`。  
  
 可以按下列方式配置 OLE DB 连接管理器：  
  
-   提供配置为满足选定访问接口要求的特定连接字符串。  
  
-   包括要连接到的数据源的名称（取决于访问接口）。  
  
-   为选定的访问接口提供相应的安全凭据。  
  
-   指示是否在运行时保留从连接管理器中创建的连接。  
  
## <a name="logging"></a>日志记录  
 可以记录 OLE DB 连接管理器对外部数据访问接口所做的调用。 使用此日志记录功能，可以对 OLE DB 连接管理器与外部数据源的连接进行故障排除。 若要记录 OLE DB 连接管理器对外部数据访问接口所做的调用，请在包级别启用包日志记录并选择 **“诊断”** 事件。 有关详细信息，请参阅 [包执行的疑难解答工具](../troubleshooting/troubleshooting-tools-for-package-execution.md)。  
  
## <a name="configuration-of-the-oledb-connection-manager"></a>OLEDB 连接管理器的配置  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式设置属性。 有关可以在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请参阅 [配置 OLE DB 连接管理器](../configure-ole-db-connection-manager.md)。 有关以编程方式配置连接管理器的信息，请参阅开发人员指南中针对 **T:Microsoft.SqlServer.Dts.Runtime.ConnectionManager** 类的文档。  
  
## <a name="related-content"></a>相关内容  
  
-   social.technet.microsoft.com 上的 Wiki 文章 [SSIS 与 Oracle 连接器](http://go.microsoft.com/fwlink/?LinkId=220670) 。  
  
-   carlprothman.net 上的技术文章 [Connection Strings for OLE DB Providers](http://go.microsoft.com/fwlink/?LinkId=220744)（OLE DB 访问接口的连接字符串）。  
  
## <a name="see-also"></a>请参阅  
 [OLE DB 源](../data-flow/ole-db-source.md)   
 [OLE DB 目标](../data-flow/ole-db-destination.md)   
 [执行 SQL 任务](../control-flow/execute-sql-task.md)   
 [Integration Services &#40;SSIS&#41;的连接](integration-services-ssis-connections.md)  
  
  
