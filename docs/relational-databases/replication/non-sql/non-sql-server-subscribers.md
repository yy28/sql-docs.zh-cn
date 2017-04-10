---
title: "非 SQL Server 订阅服务器 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "订阅 [SQL Server 复制]，非 SQL Server 订阅服务器"
  - "异类数据源，非 SQL Server 订阅服务器"
  - "异类数据源"
  - "异类数据源复制，非 SQL Server 订阅服务器"
  - "非 SQL Server 订阅服务器，关于非 SQL Server 订阅服务器"
  - "异类订阅服务器"
  - "异类订阅服务器，关于异类订阅服务器"
  - "订阅服务器 [SQL Server 复制]，非 SQL Server 订阅服务器"
  - "非 SQL Server 订阅服务器"
ms.assetid: 831e7586-2949-4b9b-a2f3-7b0b699b23ff
caps.latest.revision: 55
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 55
---
# 非 SQL Server 订阅服务器
  下列非 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 订阅服务器可通过推送订阅来订阅快照发布和事务发布。 支持所列每个数据库的两个最新版本使用所列 OLE DB 访问接口的最新版本进行订阅。  
  
 不推荐异类复制到非 SQL Server 订阅服务器。 不推荐使用 Oracle 发布。 若要移动数据，请创建使用变更数据捕获和 [!INCLUDE[ssIS](../../../includes/ssis-md.md)]的解决方案。  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
|数据库|操作系统|提供程序|  
|--------------|----------------------|--------------|  
|Oracle|Oracle 支持的所有平台|Oracle OLE DB 访问接口（由 Oracle 提供）|  
|IBM DB2|MVS、AS400、Unix、Linux、Windows（9.x 版除外）|Microsoft Host Integration Server (HIS) OLE DB 访问接口|  
  
 有关创建与 Oracle 和 IBM DB2 订阅的信息，请参阅 [Oracle 订阅服务器](../../../relational-databases/replication/non-sql/oracle-subscribers.md) 和 [IBM DB2 订阅服务器](../../../relational-databases/replication/non-sql/ibm-db2-subscribers.md)。  
  
## 非 SQL Server 订阅服务器的注意事项  
 在复制到非 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 订阅服务器时，请牢记下列注意事项：  
  
### 一般注意事项  
  
-   复制支持将表和索引视图作为表发布到非 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 订阅服务器（索引视图不能作为索引视图复制）。  
  
-   如果在新建发布向导创建发布，然后启用它为非 SQL Server 订阅服务器使用发布属性对话框中，在订阅数据库中的所有对象的所有者未指定为非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 订阅服务器，而对于 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 订阅服务器，则此属性设置为发布数据库中相应对象的所有者。  
  
-   如果发布中将包括 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 订阅服务器和非 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 订阅服务器，则必须在创建对 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 订阅服务器的任何订阅之前为非 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 订阅服务器启用发布。  
  
-   默认情况下，由快照代理为非 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 订阅服务器生成的脚本在 CREATE TABLE 语法中使用不带引号的标识符。 因此，名为“test”的已发布表按“TEST”复制。 若要为发布数据库中表使用相同的大小写，使用 **-QuotedIdentifier** 分发代理程序的参数。  **-QuotedIdentifier** 如果已发布的对象名称 （例如表、 列和约束） 包含空格或非数据库的版本中的保留的字的词，还必须使用参数[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 订阅服务器。 有关此参数的详细信息，请参阅 [Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)。  
  
-   运行分发代理时使用的帐户必须对 OLE DB 访问接口的安装目录具有读权限。  
  
-   默认情况下，对于非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 订阅服务器，分发代理使用 [(default destination)] 值对订阅数据库 ( **-SubscriberDB** 分发代理程序的参数):  
  
    -   对于 Oracle，一个服务器最多只有一个数据库，因此不必指定数据库。  
  
    -   对于 IBM DB2，在 DB2 连接字符串中指定数据库。 有关详细信息，请参阅 [为非 SQL Server 订阅服务器创建订阅](../../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md)。  
  
-   如果 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 分发服务器运行在 64 位平台上，必须使用相应 OLE DB 访问接口的 64 位版本。  
  
-   无论发布服务器和订阅服务器中的排序规则/代码页是什么，复制都以 Unicode 格式移动数据。 建议在发布服务器和订阅服务器之间复制时选择一个兼容的排序规则/代码页。  
  
-   如果在发布中添加或删除项目，必须重新初始化对非 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 订阅服务器的订阅。  
  
-   所有非 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 订阅服务器支持的约束只有：NULL 和 NOT NULL。 主键约束按唯一索引复制。  
  
-   不同的数据库处理 NULL 值的方式不同，这将影响空白值、空字符串和 NULL 的显示方式， 而显示方式又影响在定义了唯一约束的列中插入值的行为。 例如，Oracle 允许唯一列中有多个 NULL 值，而 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 仅允许唯一列中存在一个 NULL 值。  
  
     另一个因素是当列被定义为 NOT NULL 时，如何处理 NULL 值、空字符串和空白值。 有关如何为 Oracle 订阅服务器解决此问题的信息，请参阅 [Oracle Subscribers](../../../relational-databases/replication/non-sql/oracle-subscribers.md)。  
  
-   删除该订阅时，不从非 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 订阅服务器中删除与复制有关的元数据（事务序列表）。  
  
### 符合订阅服务器数据库的要求  
  
-   已发布的架构和数据必须符合订阅服务器中的数据库的要求。 例如，如果非 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库的最大行大小比 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 小，必须确保已发布的架构和数据不超过此大小。  
  
-   复制到非 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 订阅服务器的表将采用订阅服务器中的数据库的表命名约定。  
  
-   非 SQL Server 订阅服务器不支持 DDL。 有关架构更改的详细信息，请参阅 [发布数据库上进行架构更改](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)。  
  
### 复制功能支持  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 提供了两种订阅类型：推送订阅和请求订阅。 非 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 订阅服务器必须使用推送订阅，在这种订阅中，分发代理运行在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 分发服务器中。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 提供了两种快照格式︰ 本机 bcp 模式和字符模式。 非 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 订阅服务器需要字符模式快照。  
  
-   非 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 订阅服务器不能使用即时更新订阅或排队更新订阅，也不能作为对等拓扑中的节点。  
  
-   非 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 订阅服务器不能从备份中自动初始化。  
  
## 另请参阅  
 [异类数据库复制](../../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [订阅发布](../../../relational-databases/replication/subscribe-to-publications.md)  
  
  