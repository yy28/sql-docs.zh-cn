---
title: 链接服务器（数据库引擎）| Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB, linked servers
- OLE DB provider, linked servers
- server management [SQL Server], linked servers
- linked servers [SQL Server]
- distributed queries [SQL Server], linked servers
- servers [SQL Server], linked
- remote servers [SQL Server], linked servers
- linked servers [SQL Server], about linked servers
ms.assetid: 6ef578bf-8da7-46e0-88b5-e310fc908bb0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8c2909eeebde268b52ecaeff5a20a982831e7569
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62743491"
---
# <a name="linked-servers-database-engine"></a>链接服务器（数据库引擎）
  配置链接服务器以支持 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]之外对 OLE DB 数据源执行命令。 通常，配置链接服务器是为了支持 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 实例或诸如 Oracle 等其他数据库产品上执行包含表的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]语句。 许多类型的 OLE DB 数据源都可配置为链接服务器，包括 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Access 和 Excel。 链接服务器具有以下优点：  
  
-   能够访问 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]之外的数据。  
  
-   能够对企业内的异类数据源发出分布式查询、更新、命令和事务。  
  
-   能够以相似的方式确定不同的数据源。  
  
 你可以使用 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 或 [sp_addlinkedserver (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql) 语句配置链接服务器。 OLE DB 访问接口的类型和所需的参数的数量大不相同。 例如，一些访问接口要求你使用 [sp_addlinkedsrvlogin (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql)之外对 OLE DB 数据源执行命令。 某些 OLE DB 访问接口允许 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 更新数据 OLE DB 源上的数据。 其他访问接口可能仅提供只读数据访问权限。 有关每个 OLE DB 访问接口的信息，请查看该 OLE DB 访问接口的文档。  
  
## <a name="linked-server-components"></a>链接服务器组件  
 链接服务器定义指定了下列对象：  
  
-   OLE DB 访问接口  
  
-   OLE DB 数据源  
  
 “OLE DB 访问接口”  是管理特定数据源并与其交互的 DLL。 “OLE DB 数据源”  标识可通过 OLE DB 访问的特定数据库。 虽然通过链接服务器定义查询的数据源通常是数据库，但 OLE DB 访问接口对各种文件和文件格式仍可用。 这些文件和文件格式包括文本文件、电子表格数据和全文内容搜索的结果。  
  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序 (PROGID:SQLNCLI11) 是适用于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的官方 OLE DB 提供程序。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 分布式查询旨在与任何实现所需 OLE DB 接口的 OLE DB 访问接口一起使用。 但是， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 仅针对 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口和特定访问接口进行过测试。  
  
## <a name="linked-server-details"></a>链接服务器详细信息  
 下图显示了链接服务器配置的基础。  
  
 ![客户端层、服务器层和数据库服务器层](../../database-engine/media/lsvr.gif "客户端层、服务器层和数据库服务器层")  
  
 通常，链接服务器用于处理分布式查询。 当客户端应用程序通过链接服务器执行分布式查询时， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 将分析命令并向 OLE DB 发送请求。 行集请求的形式可以是对该访问接口执行查询或从该访问接口打开基表。  
  
 为使数据源能通过链接服务器返回数据，该数据源的 OLE DB 访问接口 (DLL) 必须与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]的实例位于同一服务器上。  
  
 使用第三方 OLE DB 访问接口时，运行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服务的帐户必须具有对安装访问接口的目录及其所有子目录的读取权限和执行权限。  
  
## <a name="managing-providers"></a>管理访问接口  
 有一组选项可以控制 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 如何加载和使用注册表中指定的 OLE DB 访问接口。  
  
## <a name="managing-linked-server-definitions"></a>管理链接服务器定义  
 设置链接服务器时，请在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中注册连接信息和数据源信息。 完成注册后，可以用单个逻辑名称来引用该数据源。  
  
 可以使用存储过程和目录视图来管理链接服务器定义：  
  
-   通过运行 **sp_addlinkedserver**创建链接服务器定义。  
  
-   通过对 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sys.servers **系统目录视图执行查询，查看有关在** 的特定实例中定义的链接服务器的信息。  
  
-   通过运行 **sp_dropserver**删除链接服务器定义。 还可以使用此存储过程删除远程服务器。  
  
 还可以使用 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 来定义链接服务器。 在对象资源管理器中，右键单击“服务器对象”  ，选择“新建”  ，再选择“链接服务器”  。 通过右键单击链接服务器名称并选择“删除”  ，可以删除链接服务器定义。  
  
 对链接服务器执行分布式查询时，请对每个要查询的数据源指定由四个部分组成的完全限定的表名。 这个四部分名称应采用格式_linked_server_name.catalog_ **。 _`schema`_ .** _object_name_。  
  
> [!NOTE]  
>  可以定义链接服务器指回（环回）到在其上定义它们的服务器。 当在单服务器网络中测试使用分布式查询的应用程序时，环回服务器是很有用的。 环回链接服务器专用于测试，许多操作（如分布式事务）不支持该服务器。  
  
## <a name="related-tasks"></a>Related Tasks  
 [创建链接服务器（SQL Server 数据库引擎）](create-linked-servers-sql-server-database-engine.md)  
  
 [sp_addlinkedserver (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql)  
  
 [sp_addlinkedsrvlogin (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql)  
  
 [sp_dropserver (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-dropserver-transact-sql)  
  
## <a name="related-content"></a>相关内容  
 [sys.servers (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-servers-transact-sql)  
  
 [sp_linkedservers (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-linkedservers-transact-sql)  
  
  
