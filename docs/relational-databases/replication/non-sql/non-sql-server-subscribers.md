---
title: "非 SQL Server 订阅服务器 | Microsoft Docs"
ms.custom: 
ms.date: 08/29/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- subscriptions [SQL Server replication], non-SQL Server Subscribers
- heterogeneous data sources, non-SQL Server Subscribers
- heterogeneous data sources
- heterogeneous database replication, non-SQL Server Subscribers
- non-SQL Server Subscribers, about non-SQL Server Subscribers
- heterogeneous Subscribers
- heterogeneous Subscribers, about heterogeneous Subscribers
- Subscribers [SQL Server replication], non-SQL Server Subscribers
- non-SQL Server Subscribers
ms.assetid: 831e7586-2949-4b9b-a2f3-7b0b699b23ff
caps.latest.revision: 55
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 05497c347c94b42bb22488560c89b7f9a7783a4d
ms.openlocfilehash: feeb6962b9505dd33594f423fff08ca7ca1ff61f
ms.contentlocale: zh-cn
ms.lasthandoff: 08/30/2017

---
# <a name="non-sql-server-subscribers"></a>非 SQL Server 订阅服务器  
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

下列非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 订阅服务器可通过推送订阅来订阅快照发布和事务发布。 支持所列每个数据库的两个最新版本使用所列 OLE DB 访问接口的最新版本进行订阅。  
  
 不推荐异类复制到非 SQL Server 订阅服务器。 不推荐使用 Oracle 发布。 若要移动数据，请创建使用变更数据捕获和 [!INCLUDE[ssIS](../../../includes/ssis-md.md)]的解决方案。  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
|数据库|操作系统|提供程序|  
|--------------|----------------------|--------------|  
|Oracle|Oracle 支持的所有平台|Oracle OLE DB 访问接口（由 Oracle 提供）|  
|IBM DB2|MVS、AS400、Unix、Linux、Windows（9.x 版除外）|Microsoft Host Integration Server (HIS) OLE DB 访问接口|  

Oracle 版本信息：  
[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 支持下列异类事务复制和快照复制方案：  
  
-   将数据从 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 发布到非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 订阅服务器。  

-   将数据发布到 Oracle 以及从 Oracle 发布数据具有以下限制条件：  
  | |2016 或更早版本 |2017 或更高版本 |
  |-------|-------|--------|
  |从 Oracle 复制 |仅支持 Oracle 10g 或更早版本 |仅支持 Oracle 10g 或更早版本 |
  |复制到 Oracle |最高为 Oracle 12c |不支持 |


 不推荐异类复制到非 SQL Server 订阅服务器。 不推荐使用 Oracle 发布。 若要移动数据，请创建使用变更数据捕获和 [!INCLUDE[ssIS](../../../includes/ssis-md.md)]的解决方案。  

有关创建 Oracle 和 IBM DB2, 订阅的信息，请参阅 [Oracle 订阅服务器](../../../relational-databases/replication/non-sql/oracle-subscribers.md) 和 [IBM DB2 Subscribers](../../../relational-databases/replication/non-sql/ibm-db2-subscribers.md)的解决方案。  
  
## <a name="considerations-for-non-sql-server-subscribers"></a>非 SQL Server 订阅服务器的注意事项  
 在复制到非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 订阅服务器时，请牢记下列注意事项：  
  
### <a name="general-considerations"></a>一般注意事项  
  
-   复制支持将表和索引视图作为表发布到非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 订阅服务器（索引视图不能作为索引视图复制）。  
  
-   在新建发布向导中创建发布，然后使用“发布属性”对话框为非 SQL Server 订阅服务器启用此发布时，不要为非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 订阅服务器指定订阅数据库中所有对象的所有者，对于 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 订阅服务器，应设置为发布数据库中相应对象的所有者。  
  
-   如果发布中包括 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 订阅服务器和非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 订阅服务器，则必须在创建对[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 订阅服务器的任何订阅之前为非 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 订阅服务器启用发布。  
  
-   默认情况下，由快照代理为非 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 订阅服务器生成的脚本在 `CREATE TABLE` 语法中使用不带引号的标识符。 因此，名为“test”的已发布表按“TEST”复制。 若要使用与发布数据库中的表相同的大小写，请使用分发代理的 **-QuotedIdentifier** 参数。 如果非 **订阅服务器中已发布的对象名称（如表、列和约束）包含空格或相应版本数据库中保留的字词，则还必须使用** -QuotedIdentifier[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 参数。 有关此参数的详细信息，请参阅 [复制分发代理](../../../relational-databases/replication/agents/replication-distribution-agent.md)。  
  
-   运行分发代理时使用的帐户必须对 OLE DB 访问接口的安装目录具有读权限。  
  
-   默认情况下，对于非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 订阅服务器，分发代理对订阅数据库使用 [(default destination)] 值（分发代理的 **-SubscriberDB** 参数）：  
  
    -   对于 Oracle，一个服务器最多只有一个数据库，因此不必指定数据库。  
  
    -   对于 IBM DB2，在 DB2 连接字符串中指定数据库。 有关详细信息，请参阅 [为非 SQL Server 订阅服务器创建订阅](../../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md)。  
  
-   如果 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 分发服务器运行在 64 位平台上，必须使用相应 OLE DB 访问接口的 64 位版本。  
  
-   无论发布服务器和订阅服务器中的排序规则/代码页是什么，复制都以 Unicode 格式移动数据。 建议在发布服务器和订阅服务器之间复制时选择一个兼容的排序规则/代码页。  
  
-   如果在发布中添加或删除项目，必须重新初始化对非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 订阅服务器的订阅。  
  
-   所有非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 订阅服务器支持的约束只有：NULL 和 NOT NULL。 主键约束按唯一索引复制。  
  
-   不同的数据库处理 NULL 值的方式不同，这将影响空白值、空字符串和 NULL 的显示方式， 而显示方式又影响在定义了唯一约束的列中插入值的行为。 例如，Oracle 允许唯一列中有多个 NULL 值，而 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 仅允许唯一列中存在一个 NULL 值。  
  
     另一个因素是当列被定义为 NOT NULL 时，如何处理 NULL 值、空字符串和空白值。 有关如何为 Oracle 订阅服务器解决此问题的信息，请参阅 [Oracle 订阅服务器](../../../relational-databases/replication/non-sql/oracle-subscribers.md)。  
  
-   删除该订阅时，不从非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 订阅服务器中删除与复制有关的元数据（事务序列表）。  
  
### <a name="conforming-to-the-requirements-of-the-subscriber-database"></a>符合订阅服务器数据库的要求  
  
-   已发布的架构和数据必须符合订阅服务器中的数据库的要求。 例如，如果非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库的最大行大小比 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]小，必须确保已发布的架构和数据不超过此大小。  
  
-   复制到非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 订阅服务器的表将采用订阅服务器中的数据库的表命名约定。  
  
-   非 SQL Server 订阅服务器不支持 DDL。 有关架构更改的详细信息，请参阅[对发布数据库进行架构更改](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)。  
  
### <a name="replication-feature-support"></a>复制功能支持  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 提供了两种订阅类型：推送订阅和请求订阅。 非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 订阅服务器必须使用推送订阅，在这种订阅中，分发代理运行在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 分发服务器中。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 提供了两种快照格式：本机 bcp 模式和字符模式。 非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 订阅服务器需要字符模式快照。  
  
-   非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 订阅服务器不能使用即时更新订阅或排队更新订阅，也不能作为对等拓扑中的节点。  
  
-   非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 订阅服务器不能从备份中自动初始化。  
  
## <a name="see-also"></a>另请参阅  
 [异类数据库复制](../../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [订阅发布](../../../relational-databases/replication/subscribe-to-publications.md)  
  
  

