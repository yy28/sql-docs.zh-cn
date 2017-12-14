---
title: "在 Oracle 发布服务器上创建的对象 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Oracle publishing [SQL Server replication], objects created
ms.assetid: c58a124b-4da7-46e2-9292-af8ce9e6664b
caps.latest.revision: "33"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 84b3cf9e41c659753e428daff07b1c11efadaa94
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="objects-created-on-the-oracle-publisher"></a>在 Oracle 发布服务器上创建的对象
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)][!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 复制将数据库对象安装在 Oracle 发布服务器上以启用更改跟踪和转发（[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不会在 Oracle 发布服务器上安装任何二进制文件）。 下表列出了在将 Oracle 发布服务器标识为 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 分发服务器上的发布服务器时，在其上所创建的对象。 对象说明仅供参考。 不应对这些对象做任何修改。  
  
|Object Name|对象类型|说明|  
|-----------------|-----------------|-----------------|  
|HREPL_ArticleNlog_V|表|更改跟踪表，当对已发布的表中进行了更改时，可使用此表存储更改信息。 为每个已发布的表创建一个更改跟踪表。|  
|HREPL_Changes|表|Xactset 作业内部用来确定等待分配给事务集的更改数量的表。 有关此作业的详细信息，请参阅 [Performance Tuning for Oracle Publishers](../../../relational-databases/replication/non-sql/performance-tuning-for-oracle-publishers.md)（Oracle 发布服务器的性能优化）。|  
|HREPL_Distributor|表|分发服务器状态表，用于维护与 Oracle 发布服务器相关联的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 分发服务器的信息。|  
|HREPL_Event|表|事件表，用于同步快照和行计数请求。|  
|HREPL_Mutex|表|用于确保 Oracle 包过程 PopulatePollTable 未由日志读取器代理和数据库作业并发执行的表。|  
|HREPL_Poll|表|用于标识与几组已发布表的更改相关联的日志表项的表。|  
|HREPL_PublishedTables|表|包含事务发布中每个项目项的表。|  
|HREPL_Publisher|表|发布服务器状态表，用于维护发布服务器的特定信息。|  
|HREPL_SchemaFilter|表|包含在通过新建发布向导发布时不显示的架构的表。|  
|HREPL_XactsetCreateTimes|表|标识与每个事务集相关联的创建时间的表。|  
|HREPL_XactsetJob|表|包含用于 Xactset 作业的当前参数设置的表。|  
|HREPL_Pollid|序列|用于生成轮询 ID 的序列。|  
|HREPL_Seq|序列|用于对更改命令进行排序的序列。|  
|HREPL_Stmt|序列|用于生成语句 ID 的序列。|  
|HREPL|包和包正文|在发布服务器上创建的发布服务器支持代码的包。|  
|MSSQLSERVERDISTRIBUTOR|公共同义词|HREPL_Distributor 表的公共同义词。 如果将分发服务器配置为与 Oracle 发布服务器一起使用，而且此同义词已存在于数据库中，则应将其删除并重新创建。<br /><br /> 用 CASCADE 选项删除公共同义词和已配置的 Oracle 复制用户会删除 Oracle 发布服务器中的所有复制对象。|  
|HREPL_Len_I_J_K|函数|在 Oracle 发布包代码之外定义的、用于查询 LONG 列的长度（在为带有已发布 LONG 列的表生成参数化命令时使用）的函数。 为每个带有 LONG 列的已发布表创建一个函数。|  
|HREPL_DropPublisher|过程|在 Oracle 发布包代码之外定义的、用于删除 Oracle 发布服务器的过程。|  
|HREPL_ExecuteCommand|过程|在 Oracle 发布包代码之外定义的、用于在发布服务器上执行命令的过程。|  
|HREPL_ArticleN_Trigger_Row|触发器|为每个已发布表生成的、用于跟踪行更改的触发器。|  
|HREPL_ArticleN_Trigger_Stmt|触发器|为每个已发布表生成的、用于跟踪语句级更改的触发器。|  
|HREPL_Article_I_J|视图|为每个已发布表创建的、用于查询已发布表的视图。|  
|HREPL_Log_I_J_K|视图|为每个已发布表创建的、用于查询更改跟踪表的视图。|  
  
## <a name="see-also"></a>另请参阅  
 [配置 Oracle 发布服务器](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [有关 Oracle 发布的术语词汇表](../../../relational-databases/replication/non-sql/glossary-of-terms-for-oracle-publishing.md)   
 [Oracle Publishing Overview](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)  
  
  
