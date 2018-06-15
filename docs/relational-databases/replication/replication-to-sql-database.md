---
title: 复制到 SQL 数据库 | Microsoft Docs
ms.custom: ''
ms.date: 04/24/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Database replication
- replication, SQL Database
ms.assetid: e8484da7-495f-4dac-b38e-bcdc4691f9fa
caps.latest.revision: 15
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 5e3099ebb18883a99b5815b3db3e40f178b22234
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32964242"
---
# <a name="replication-to-sql-database"></a>复制到 SQL 数据库
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  可以将[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 复制配置为 [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]。  
 
 ### <a name="supported-configurations"></a>**支持的配置：**  
 -  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以是在本地运行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例，或者是在云中的 Azure 虚拟机上运行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例。 有关详细信息，请参阅 [SQL Server on Azure Virtual Machines overview（Azure 虚拟机上的 SQL Server 概述）](https://azure.microsoft.com/documentation/articles/virtual-machines-sql-server-infrastructure-services/)。  
 - [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 必须是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发布服务器的推送订阅服务器。  
 -  不能将分发数据库和复制代理放置在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]上。  
 - 支持快照和单向事务复制。 不支持对等事务复制和合并复制。  
 
 ## <a name="versions"></a>版本  
 - 发布服务器和分发服务器必须至少为以下任一版本：  
   
 -   [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)]  
 
 -   [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]  
   
 -   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP1 CU3  
   
 -   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] RTM CU10  
   
 -   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 CU8  
   
 -   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 应为 SP3  
   
 - 尝试使用较旧版本配置复制可能会导致出现错误代码 MSSQL_REPL20084（进程无法连接到订阅服务器。）和 MSSQL_REPL40532（无法打开登录所请求的服务器 \<名称>。 登录失败。）。  
 
 - [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 订阅服务器必须至少是 V12 且能处于任何区域。  
   
 - 若要使用 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 的所有功能，必须使用最新版本的 [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) 和 [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx)。  
   
 ## <a name="remarks"></a>Remarks  
 - 可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或在发布服务器上执行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句配置复制。 不能使用 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 门户配置复制。  
   
 - 复制只能使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证登录名以连接到 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]。  
   
 - 复制的表必须具有主键。  
   
 - 必须拥有现有 Azure 订阅和现有 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] V12。  
   
 - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上的单个发布可以支持 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 订阅服务器（本地和 Azure 虚拟机中的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ）。  
   
 - 必须从本地 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]执行复制管理、监视和故障排除。  
   
 - 仅支持 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 的推送订阅。  
   
 - 用于 SQL 数据库的 `@subscriber_type = 0` 仅支持 **@subscriber_type = 0** 。  
   
 - [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 不支持双向、即时、可更新或对等复制。      
   
 ## <a name="replication-architecture"></a>复制体系结构  
 ![replication-to-sql-database](../../relational-databases/replication/media/replication-to-sql-database.png "replication-to-sql-database")  
   
 ## <a name="scenarios"></a>方案  
   
 ### <a name="typical-replication-scenario"></a>典型的复制方案  
   
 1.  在本地 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库上创建事务复制发布。  
   
 2.  在本地 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上使用 **新建订阅向导** 或 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句以创建 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]的推送订阅。  
   
 3.  初始数据集通常是由快照代理创建并由分发代理分发和应用的快照。 初始数据集还可以通过备份或其他方式提供，例如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]。  
   
 #### <a name="data-migration-scenario"></a>数据迁移方案  
   
 1.  使用事务复制来将本地 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中的数据复制到 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]。  
   
 2.  重定向客户端或中间层应用程序以更新 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 副本。  
   
 3.  停止更新表的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本并删除发布。  
   
 ## <a name="limitations"></a>限制  
  [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 订阅不支持以下选项：  
   
 -   复制文件组关联  
   
 -   复制表分区方案  
   
 -   复制索引分区方案  
   
 -   复制用户定义的统计信息  
   
 -   复制默认值绑定  
   
 -   复制规则绑定  
   
 -   复制全文索引  
   
 -   复制 XML XSD  
   
 -   复制 XML 索引  
   
 -   复制权限  
   
 -   复制空间索引  
   
 -   复制筛选索引  
   
 -   复制数据压缩属性  
   
 -   复制稀疏列属性  
   
 -   将文件流转换为 MAX 数据类型  
   
 -   将 hierarchyid 转换为 MAX 数据类型  
   
 -   将空间转换为 MAX 数据类型  
   
 -   复制扩展属性  
   
 -   复制权限  
   
### <a name="limitations-to-be-determined"></a>待定限制 
 
 -   复制排序规则  
   
 -   SP 的序列化事务中的执行  
   
 ## <a name="examples"></a>示例  
  创建发布和推送订阅。 有关详细信息，请参阅：  
   
 -   [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)  
   
 -   通过将 [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] 逻辑服务器名称用作订阅服务器（例如 **N'azuresqldbdns.database.windows.net'**）并将 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 名称用作目标数据库（例如 **AdventureWorks**）来[创建推送订阅](../../relational-databases/replication/create-a-push-subscription.md)。  
   
 ## <a name="see-also"></a>另请参阅  
 - [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 - [创建推送订阅](../../relational-databases/replication/create-a-push-subscription.md)   
 - [复制类型](../../relational-databases/replication/types-of-replication.md)   
 - [监视（复制）](../../relational-databases/replication/monitor/monitoring-replication.md)   
 - [初始化订阅](../../relational-databases/replication/initialize-a-subscription.md)  
