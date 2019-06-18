---
title: 数据库引擎实例 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: af9ae643-9866-4014-b36f-11ab556a773e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 2e38b572535011737f33ba1e4c438540ecdd6849
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62811228"
---
# <a name="database-engine-instances-sql-server"></a>数据库引擎实例 (SQL Server)
  [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例是作为操作系统服务运行的 `sqlservr.exe` 可执行程序的副本。 每个实例管理几个系统数据库以及一个或多个用户数据库。 每台计算机都可以运行 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的多个实例。 应用程序连接到实例，以便在实例管理的数据库中执行任务。  
  
## <a name="instances"></a>实例  
 一个 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例作为处理所有应用程序请求的服务操作，以便使用该实例管理的任何数据库中的数据。 它是应用程序所发出连接请求（登录名）的目标。 如果应用程序和实例分别位于单独的计算机上，则连接通过网络连接运行。 如果应用程序和实例位于同一台计算机上，则 SQL Server 连接可作为网络连接或内存中连接运行。 完成连接后，应用程序通过连接将 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句发送给实例。 实例将这些 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句解析为针对数据库中的数据和对象的操作；并且如果已将所需权限授予了登录凭据，，则实例会执行这些工作。 检索的任何数据都将返回到应用程序，同时还返回错误之类的任何消息。  
  
 可以在一台计算机上运行 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的多个实例。 一个实例可以是默认实例。 该默认实例没有名称。 如果某一连接请求仅指定计算机的名称，则会与默认实例建立连接。 命名实例是您在安装实例时指定实例名称的一种实例。 为了连接到该实例，连接请求必须同时指定计算机名称和实例名称。 不一定非要安装默认实例；在计算机上运行的所有实例都可以是命名实例。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|任务说明|主题|  
|----------------------|-----------|  
|介绍如何配置实例的属性。 配置文件位置和日期格式之类的默认值，或者配置实例使用内存或线程之类的操作系统资源的方式。|[配置数据库引擎实例 (SQL Server)](database-engine-instances-sql-server.md)|  
|介绍如何管理 [!INCLUDE[ssDE](../../includes/ssde-md.md)]实例的排序规则。 排序规则定义用于表示字符的位模式、排序之类的关联行为以及比较操作中是否区分大小写或重音。|[排序规则和 Unicode 支持](../../relational-databases/collations/collation-and-unicode-support.md)|  
|介绍如何配置链接服务器定义，这将允许 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句在某一实例下运行，以便使用在单独的 OLE DB 数据源中存储的数据。|[链接服务器（数据库引擎）](../../relational-databases/linked-servers/linked-servers-database-engine.md)|  
|介绍如何创建登录触发器，这将指定在验证了登录尝试后、但在开始使用实例中的资源之前要执行的操作。 登录触发器支持各种操作，例如记录连接活动，或者基于 Windows 和 SQL Server 执行的凭据身份验证之外的逻辑来限制登录。|[登录触发器](../../relational-databases/triggers/logon-triggers.md)|  
|介绍如何管理与 [!INCLUDE[ssDE](../../includes/ssde-md.md)]实例关联的服务。 这包括启动和停止服务或者配置启动选项之类的操作。|[管理数据库引擎服务](manage-the-database-engine-services.md)|  
|介绍如何执行服务器网络配置任务，例如启用协议、修改协议使用的端口或管道、配置加密、配置 SQL Server Browser 服务、在网络中显示或隐藏 SQL Server 数据库引擎以及注册服务器主体名称。|[服务器网络配置](server-network-configuration.md)|  
|介绍如何执行客户端网络配置任务，例如配置客户端协议以及创建或删除服务器别名。|[客户端网络配置](client-network-configuration.md)|  
|介绍可用于设计、调试和运行 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 脚本之类的脚本的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 编辑器。 介绍如何对 Windows PowerShell 脚本进行编码以便使用 SQL Server 组件。|[数据库引擎脚本](../../relational-databases/scripting/database-engine-scripting.md)|  
|介绍如何使用维护计划以便为实例指定常见管理任务的工作流。 工作流包含诸如备份数据库和更新统计信息以提高性能之类的任务。|[维护计划](../../relational-databases/maintenance-plans/maintenance-plans.md)|  
|介绍如何使用资源调控器来通过指定应用程序请求可使用的 CPU 和内存量的限制来管理资源使用和工作负荷。|[资源调控器](../../relational-databases/resource-governor/resource-governor.md)|  
|介绍数据库应用程序如何使用数据库邮件从 [!INCLUDE[ssDE](../../includes/ssde-md.md)]发送电子邮件。|[数据库邮件](../../relational-databases/database-mail/database-mail.md)|  
|介绍如何使用扩展事件来捕获可用于生成性能基准或诊断性能问题的性能数据。 扩展事件是用于收集性能数据的轻型、高度可伸缩的系统。|[扩展事件](../../relational-databases/extended-events/extended-events.md)|  
|介绍如何使用 SQL 跟踪以便生成自定义系统来捕获和记录 [!INCLUDE[ssDE](../../includes/ssde-md.md)]中的事件。|[SQL 跟踪](../../relational-databases/sql-trace/sql-trace.md)|  
|介绍如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Profiler 来捕获传入 [!INCLUDE[ssDE](../../includes/ssde-md.md)]实例的应用程序请求的跟踪。 可在以后为活动（例如性能测试或问题诊断）重播这些跟踪。|[SQL Server 事件探查器](../../tools/sql-server-profiler/sql-server-profiler.md)|  
|介绍变更数据捕获 (CDC) 和更改跟踪功能以及如何使用这些功能来跟踪数据库中的数据更改。|[跟踪数据更改 (SQL Server)](../../relational-databases/track-changes/track-data-changes-sql-server.md)|  
|介绍如何使用日志文件查看器来查找和查看不同日志（例如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 作业历史记录、SQL Server 日志和 Windows 事件日志）中的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误和消息。|[日志文件查看器](../../relational-databases/logs/log-file-viewer.md)|  
|介绍如何使用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 优化顾问来分析数据库并为解决潜在的性能问题提出建议。|[Database Engine Tuning Advisor](../../relational-databases/performance/database-engine-tuning-advisor.md)|  
|介绍在不接受标准连接时，生产数据库管理员如何与实例建立诊断连接。|[用于数据库管理员的诊断连接](diagnostic-connection-for-database-administrators.md)|  
|介绍如何使用不推荐使用的远程服务器功能来从 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的一个实例访问另一个实例。 此功能的首选机制是链接服务器。|[远程服务器](remote-servers.md)|  
|介绍 Service Broker 的消息传递和应用程序排队功能，并提供指向 Service Broker 文档的指针。|[Service Broker](sql-server-service-broker.md)|  
|介绍如何使用缓冲池扩展为数据库引擎缓冲池提供非易失性随机存取内存（固态驱动器）的无缝集成，以显著提高 I/O 吞吐量。|[缓冲池扩展文件](buffer-pool-extension.md)|  
  
## <a name="see-also"></a>请参阅  
 [sqlservr 应用程序](../../tools/sqlservr-application.md)   
 [数据库功能](../../relational-databases/database-features.md)   
 [数据库引擎跨实例功能](../database-engine-cross-instance-features.md)  
  
  
