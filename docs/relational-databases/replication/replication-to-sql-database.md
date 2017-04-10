---
title: "复制到 SQL 数据库 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "06/29/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "SQL 数据库复制"
  - "复制, SQL 数据库"
ms.assetid: e8484da7-495f-4dac-b38e-bcdc4691f9fa
caps.latest.revision: 15
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 15
---
# 复制到 SQL 数据库
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 复制可以配置为 [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]。  
  
 **支持的配置：**  
  
-    [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以是实例的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 运行在本地或实例 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 云中的 Azure 虚拟机中运行。 有关详细信息，请参阅 [SQL Server on Azure Virtual Machines overview（Azure 虚拟机上的 SQL Server 概述）](https://azure.microsoft.com/documentation/articles/virtual-machines-sql-server-infrastructure-services/)。  
  
-   [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 必须是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发布服务器的推送订阅服务器。  
  
-   不能将分发数据库和复制代理放置在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]上。  
  
-   支持快照和单向事务复制。 不支持对等事务复制和合并复制。  
  
## 版本  
 发布服务器和分发服务器必须至少为以下任一版本：  
  
-   [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP1 CU3  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] RTM CU10  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 CU8  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 应为 SP3  
  
 尝试配置复制，使用较旧版本可能导致错误编号 MSSQL_REPL20084 （该进程无法连接到订阅服务器。） 和 MSSQL_REPL40532 (无法打开服务器 \< 名称> 登录所请求的。 登录失败。）。  
  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 订阅服务器必须至少是 V12 且能处于任何区域。  
  
 若要使用的所有功能 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 您必须使用最新版本的 [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) 和 [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx)。  
  
## 注释  
 可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或在发布服务器上执行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句配置复制。 不能使用 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 门户配置复制。  
  
 复制只能使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证登录名以连接到 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]。  
  
 复制的表必须具有主键。  
  
 必须拥有现有 Azure 订阅和现有 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] V12。  
  
 在单个发布 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以支持这两个 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (在本地和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在 Azure 虚拟机) 的订阅服务器。  
  
 复制管理、 监视和故障排除必须从在本地执行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 仅支持 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 的推送订阅。  
  
 仅 `@subscriber_type = 0` 中支持 **sp_addsubscription** SQL database。  
  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 不支持的双向、 即时、 可更新的、 或对等复制。  
  
## 复制体系结构  
 ![replication-to-sql-database](../../relational-databases/replication/media/replication-to-sql-database.png "replication-to-sql-database")  
  
## 方案  
  
#### 典型的复制方案  
  
1.  对在本地创建事务复制发布 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库。  
  
2.  在本地上 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用 **新建订阅向导** 或 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句，以创建推送到订阅 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]。  
  
3.  初始数据集通常是由快照代理创建并由分发代理分发和应用的快照。 初始数据集还可以通过备份或其他方式提供，例如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]。  
  
#### 数据迁移方案  
  
1.  使用事务复制来将数据从本地复制 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]。  
  
2.  重定向客户端或中间层应用程序来更新 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 副本。  
  
3.  停止更新表的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本并删除发布。  
  
## 限制  
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
  
 待定限制：  
  
-   复制排序规则  
  
-   SP 的序列化事务中的执行  
  
## 示例  
 创建发布和推送订阅。 有关详细信息，请参阅：  
  
-   [创建发布](../../relational-databases/replication/publish/create-a-publication.md)  
  
-   [创建推送订阅](../../relational-databases/replication/create-a-push-subscription.md) 使用 [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] 作为订阅服务器上的逻辑服务器名称 (例如 **N'azuresqldbdns.database.windows.net**) 和 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 为目标数据库名称 (例如 **AdventureWorks**)。  
  
## 另请参阅  
 [创建发布](../../relational-databases/replication/publish/create-a-publication.md)   
 [创建推送订阅](../../relational-databases/replication/create-a-push-subscription.md)   
 [复制类型](../../relational-databases/replication/types-of-replication.md)   
 [监视和 #40;复制和 #41;](../../relational-databases/replication/monitor/monitoring-replication.md)   
 [初始化订阅](../../relational-databases/replication/initialize-a-subscription.md)  
  
  