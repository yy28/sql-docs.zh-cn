---
title: 使用 Oracle CDC 服务 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 04be5896-2301-45f5-a8ce-5f4ef2b69aa5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2f8854dba3c1d998d572481c285ee75dc933e480
ms.sourcegitcommit: 706f3a89fdb98e84569973f35a3032f324a92771
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2019
ms.locfileid: "58658051"
---
# <a name="working-with-the-oracle-cdc-service"></a>使用 Oracle CDC 服务
  本节介绍 Oracle CDC 服务的一些重要概念。 本节中包含的概念是：  
  
-   [MSXDBCDC 数据库](#BKMK_MSXDBCDC)  
  
     本节介绍在此数据库中包含的表及其对 CDC 的重要性。  
  
-   [CDC 数据库](#BKMK_CDCdatabase)  
  
     本节提供了对 CDC 数据库的简要说明。 这些数据库是使用 Oracle CDC 设计器控制台创建的。 有关 CDC 数据库的详细信息，请参阅您安装的 CDC 设计器控制台随附的文档。  
  
-   [使用命令行配置 CDC 服务](#BKMK_CommandConfigCDC)  
  
     本节介绍了可用于配置 Oracle CDC 服务的命令行命令。  
  
##  <a name="BKMK_MSXDBCDC"></a> MSXDBCDC 数据库  
 MSXDBCDC (Microsoft External-Database CDC) 数据库是一种特殊的数据库，在您将 Oracle CDC 服务用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例时需要此类数据库。  
  
 此数据库的名称无法更改。 如果名为 MSXDBCDC 的数据库在主 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上存在并且包含并非 Oracle CDC 服务定义的其他表，则该主 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例将无法使用。  
  
 此数据库的主要用途是：  
  
-   作为与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例相关联的 Oracle CDC 服务的注册表。 此信息用于服务配置和设计组件，并且用于支持对不同节点上同名的多个 CDC 服务进行协调，以便指定哪一服务是活动服务。  
  
-   作为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中包含的 Oracle CDC 实例的注册表、处理各实例的 CDC 服务以及每个服务使用的配置版本。 此信息等效于 master 数据库的 **sys.databases** 表中的 **is_cdc_enabled** 列。 该 CDC 服务将定期扫描 **dbo.xdbcdc_databases** 表以便标识对 CDC 配置或捕获实例列表的更改。  
  
-   持有 **sysadmin**所有的用于帮助创建和维护 CDC 实例的存储过程。 这些存储过程类似于用于实现 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CDC 功能的系统过程。  
  
### <a name="creating-the-msxdbcdc-database"></a>创建 MSXDBCDC 数据库  
 必须首先创建 MSXDBCDC 数据库，然后才能定义 Oracle CDC 服务。 在一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上只能创建一个 MSXDBCDC 数据库。 在您为 Oracle CDC 准备 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库时创建 MSXDBCDC 数据库。 此操作可通过使用 Oracle CDC 服务配置控制台或通过运行 CDC 服务配置控制台生成的创建脚本来完成。  
  
 此数据库的所有者是 Oracle CDC 服务管理员，该管理员控制在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例下承载的所有 Oracle CDC 实例。  
  
 **请参阅：**  
  
 [如何为 CDC 准备 SQL Server](prepare-sql-server-for-cdc.md)  
  
### <a name="the-msxdbcdc-database-tables"></a>MSXDBCDC 数据库表  
 本节介绍 MSXDBCDC 数据库中的以下表。  
  
-   [dbo.xdbcdc_trace](#BKMK_dboxdbcdc_trace)  
  
-   [dbo.xdbcdc_databases](#BKMK_dboxdbcdc_databases)  
  
-   [dbo.xdbcdc_services](#BKMK_dboxdbcdc_services)  
  
###  <a name="BKMK_dboxdbcdc_trace"></a> dbo.xdbcdc_trace  
 此表存储 Oracle CDC 服务的跟踪信息。 此表中存储的信息包括显著的状态更改和跟踪记录。  
  
 Oracle CDC 服务将错误记录和某些信息记录写入 Windows 事件日志以及跟踪表。 在某些情况下，该跟踪表可能无法访问，此时，可从事件日志访问错误信息。  
  
 下面介绍在 **dbo.xdbcdc_trace** 表中包括的项。  
  
|项|Description|  
|----------|-----------------|  
|TIMESTAMP|写入跟踪日志时的准确 UTC 时间戳。|  
|type|包含以下值之一。<br /><br /> error<br /><br /> INFO<br /><br /> 跟踪|  
|节点|写入记录的节点的名称。|  
|status|状态表使用的状态代码。|  
|sub_status|状态表使用的子状态代码。|  
|status_message|状态表使用的状态消息。|  
|源 (source)|生成了跟踪记录的 Oracle CDC 组件的名称。|  
|text_data|在错误或跟踪记录包含文本负载时的附加文本数据。|  
|binary_data|在错误或跟踪记录包含二进制负载时的附加二进制数据。|  
  
 Oracle CDC 实例将根据更改表保持策略删除旧的跟踪表行。  
  
###  <a name="BKMK_dboxdbcdc_databases"></a> dbo.xdbcdc_databases  
 此表包含当前 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中用于 Oracle CDC 数据库的 CDC 服务的名称。 每个数据库都对应于一个 Oracle CDC 实例。 Oracle CDC 服务使用此表来确定哪些实例要启动或停止以及哪些实例要重新配置。  
  
 下表介绍在 **dbo.xdbcdc_databases** 表中包括的项。  
  
|项|Description|  
|----------|-----------------|  
|NAME|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中 Oracle 数据库的名称。|  
|config_version|相应 CDC 数据库 **xdbcdc_config** 表中上次更改的时间戳 (UTC) 或者此表中当前行的时间戳 (UTC)。<br /><br /> UPDATE 触发器将此项的值强制为 GETUTCDATE()。 **config_version** 使 CDC 服务可以标识需要检查是否有配置更改或启用/禁用的 CDC 实例。|  
|cdc_service_name|此项确定哪一 Oracle CDC 服务处理所选 Oracle 数据库。|  
|enabled|指示 Oracle CDC 实例是处于活动状态 (1) 还是被禁用 (0)。 在 Oracle CDC 服务启动时，只启动标记有启用 (1) 的实例。<br /><br /> **注意**：Oracle CDC 实例可能会由于无法重试的错误而被禁用。 在此情况下，必须在解决错误后手动重新启动该实例。|  
  
###  <a name="BKMK_dboxdbcdc_services"></a> dbo.xdbcdc_services  
 此表列出了与主 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例相关联的 CDC 服务。 此表由 CDC 设计器控制台用来确定为本地 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例配置的 CDC 服务的列表。 CDC 服务还使用该表确保只有一个正在运行的 Windows 服务处理给定的 Oracle CDC 服务名称。  
  
 下表介绍在 **dbo.xdbcdc_databases** 表中包括的捕获状态项。  
  
|项|Description|  
|----------|-----------------|  
|cdc_service_name|Oracle CDC 服务的名称（Windows 服务名称）。|  
|cdc_service_sql_login|Oracle CDC 服务用于连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名。 将创建一个名为 cdc_service 的新的 SQL 用户并且与该登录名相关联，然后将其作为 db_ddladmin、db_datareader 和 db_datawriter 固定数据库角色的成员为该服务处理的每个 CDC 数据库添加。|  
|ref_count|此项对安装了同一个 Oracle CDC 服务的计算机的数目进行计数。 每增加一个同名的 Oracle CDC 服务，该计数就会递增，并且在删除此类服务时该计数将递减。 当该计数器达到零时，将删除此行。|  
|active_service_node|当前正处理 CDC 服务的 Windows 节点的名称。 在该服务正确停止后，该列将设置为 Null，指示不再有处于活动状态的服务。|  
|active_service_heartbeat|此项跟踪当前 CDC 服务以便确定该服务是否仍处于活动状态。<br /><br /> 此项将定期使用处于活动状态的 CDC 服务的当前数据库 UTC 时间戳进行更新。 默认时间间隔为 30 秒，但可以配置该时间间隔。<br /><br /> 在某一挂起的 CDC 服务检测到在经过了配置的时间间隔后检测信号未更新，则该挂起的服务将尝试接管处于活动状态的 CDC 服务角色。|  
|选项|此项指定辅助选项，例如，跟踪或优化。 它是以 **name[=value][; ]** 的形式编写的。 该选项字符串使用与 ODBC 连接字符串相同的语义。 如果该选项为布尔值（值为 yes/no），则该值只能包含名称。<br /><br /> 跟踪具有以下可能值：<br /><br /> true<br /><br /> on<br /><br /> false<br /><br /> off<br /><br /> \<class name>[,class name>]<br /><br /> 默认值是 **false**秒。<br /><br /> <br /><br /> **service_heartbeat_interval** 是服务更新 active_service_heartbeat 列的时间间隔（秒）。 默认值为 **30**。 最大值为 **3600**。<br /><br /> **service_config_polling_interval** 是 CDC 服务检查配置更改的轮询时间间隔（秒）。 默认值为 **30**。 最大值为 **3600**。<br /><br /> **sql_command_timeout** 是使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的命令超时值。 默认值是 **1**秒。 最大值为 **3600**。|  
||  
  
### <a name="the-msxdbcdc-database-stored-procedures"></a>MSXDBCDC 数据库存储过程  
 本节介绍 MSXDBCDC 数据库中的以下存储过程。  
  
-   [dbo.xcbcdc_reset_db（数据库名称）](#BKMK_dboxcbcdc_reset_db)  
  
-   [dbo.xdbcdc_disable_db(dbname)](#BKMK_dboxdbcdc_disable_db)  
  
-   [dbo.xcbcdc_add_service(svcname,sqlusr)](#BKMK_dboxcbcdc_add_service)  
  
-   [dbo.xdbcdc_start(dbname)](#BKMK_dboxdbcdc_start)  
  
-   [dbo.xdbcdc_stop(dbname)](#BKMK_dboxdbcdc_stop)  
  
###  <a name="BKMK_dboxcbcdc_reset_db"></a> dbo.xcbcdc_reset_db（数据库名称）  
 此过程将清除 Oracle CDC 实例的数据。 在以下情况下将使用该过程：  
  
-   重新启动数据捕获并且忽略以前的数据，例如以下源数据库恢复或以下某些 Oracle 事务日志不可用的非活动情况。  
  
-   在 CDC 状态存在损坏时（特别是在任何 cdc.*tables 数据中）。  
  
 **dbo.xcbcdc_reset_db** 过程执行以下任务：  
  
-   停止 CDC 实例（如果处于活动状态）。  
  
-   截断更改表、 **cdc_lsn_mapping** 表和 **cdc_ddl_history** 表。  
  
-   清除 **cdc_xdbcdc_state** 表。  
  
-   清除每一行 **cdc_change_table**的 start_lsn 列。  
  
 若要使用 **dbo.xcbcdc_reset_db** 过程，用户必须是要命名的 CDC 实例数据库的 **db_owner** 数据库角色的成员，或者是 **sysadmin** 或 **serveradmin** 固定服务器角色的成员。  
  
 有关 CDC 表的详细信息，请参阅 CDC 设计器控制台的帮助系统中的“CDC 数据库”。  
  
###  <a name="BKMK_dboxdbcdc_disable_db"></a> dbo.xdbcdc_disable_db(dbname)  
 **dbo.xcbcdc_disable_db** 过程执行以下任务：  
  
-   删除 MSXDBCDC.xdbcdc_databases 表中所选 CDC 数据库的条目。  
  
 若要使用 **dbo.xcbcdc_disable_db** 过程，用户必须是要命名的 CDC 实例的 **db_owner** 数据库角色的成员，或者是 **sysadmin** 或 **serveradmin** 固定服务器角色的成员。  
  
 有关 CDC 表的详细信息，请参阅 CDC 设计器控制台的帮助系统中的“CDC 数据库”。  
  
###  <a name="BKMK_dboxcbcdc_add_service"></a> dbo.xcbcdc_add_service(svcname,sqlusr)  
 **dbo.xcbcdc_add_service** 过程将一个条目添加到 **MSXDBCDC.xdbcdc_services** 表，并且以 1 为增量加到 **MSXDBCDC.xdbcdc_services** 表中该服务名称的 ref_count 列上。 当 **ref_count** 为 0 时，将删除该行。  
  
 要使用 dbo.xcbcdc_add_service\<service name, username> 过程，用户必须是具有要命名的 CDC 实例数据库的 db_owner 数据库角色的成员，或者是具有 sysadmin 或 serveradmin 固定服务器角色的成员。  
  
###  <a name="BKMK_dboxdbcdc_start"></a> dbo.xdbcdc_start(dbname)  
 **dbo.xdbcdc_start** 过程将一个开始请求发送到处理所选 CDC 实例的 CDC 服务，以便开始更改处理。  
  
 若要使用 **dbo.xcdcdc_start** 过程，用户必须是 CDC 数据库的 **db_owner** 数据库角色的成员，或者是 **实例的** sysadmin **或** serveradmin [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 角色的成员。  
  
###  <a name="BKMK_dboxdbcdc_stop"></a> dbo.xdbcdc_stop(dbname)  
 **dbo.xdbcdc_stop** 过程将一个停止请求发送到处理所选 CDC 实例的 CDC 服务，以便停止更改处理。  
  
 若要使用 **dbo.xcdcdc_stop** 过程，用户必须是 CDC 数据库的 **db_owner** 数据库角色的成员，或者是 **实例的** sysadmin **或** serveradmin [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 角色的成员。  
  
##  <a name="BKMK_CDCdatabase"></a> CDC 数据库  
 在 CDC 服务中使用的每个 Oracle CDC 实例都与称作 CDC 数据库的特定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库相关联。 此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库在与 Oracle CDC 服务相关联的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中承载。  
  
 该 CDC 数据库包含特殊的 cdc 架构。 Oracle CDC 服务通过前缀为 **xdbcdc_** 的表名称使用此架构。 为安全和一致性目的使用此架构。  
  
 Oracle CDC 实例和 CDC 数据库都是使用 Oracle CDC 设计器控制台创建的。 有关 CDC 数据库的详细信息，请参阅您安装的 Oracle CDC 设计器控制台随附的文档。  
  
##  <a name="BKMK_CommandConfigCDC"></a> 使用命令行配置 CDC 服务  
 您可以从命令行操作 Oracle CDC 服务程序 (xdbcdcsvc.exe)。 该 CDC 服务程序是一种本机 32 位/64 位 Windows 可执行文件。  
  
 **另请参阅**  
  
 [如何使用 CDC 服务命令行界面](how-to-use-the-cdc-service-command-line-interface.md)  
  
### <a name="service-program-commands"></a>服务程序命令  
 本节介绍用于配置 CDC 服务的以下命令。  
  
-   [Config](#BKMK_config)  
  
-   [创建](#BKMK_create)  
  
-   [删除](#BKMK_delete)  
  
###  <a name="BKMK_config"></a> Config  
 使用 `Config` 可从脚本更新 Oracle CDC 服务配置。 该命令可用于仅更新 CDC 服务配置的特定部分（例如，在不知道非对称密钥密码的情况下仅更新连接字符串）。 该命令必须由计算机管理员运行。 以下是 `Config` 命令的一个示例。  
  
```  
"<path>xdbcdcsvc.exe" config  
     <cdc-service-name>  
     [connect= <sql-server-connection-string>]  
     [key= <asym-key-password>]  
     [svcacct= <windows-account> <windows-password>]  
     [sqlacct= <sql-username> <sql-password>]  
  
```  
  
 其中：  
  
 **cdc-service-name** 是要更新的 CDC 服务的名称。 这是必需参数。  
  
 **sql-server-connection-string** 是要更新的连接字符串。 如果该连接字符串包含空格或引号，则必须用双重引号 (") 将其括起来。 嵌入的引号通过双重引号转义。  
  
 **asym-key-password** 是要更新的密码。  
  
 **windows-account**、 **windows-password** 是要更新的服务的 Windows 帐户凭据。  
  
 **sql-username**、 **sql-password** 是要更新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证凭据。 如果 sqlacct 具有空的用户名和空的密码，则 Oracle CDC 服务将使用 Windows 身份验证连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
 **注意**：包含空格或双引号的任何参数都必须用双引号 (") 括起来。 嵌入的双引号必须双重使用（例如，若要使用 **"A#B" D** 作为密码，应输入 **""A#B"" D"**）。  
  
###  <a name="BKMK_create"></a> 创建  
 使用 `Create` 可从脚本创建 Oracle CDC 服务配置。 该命令必须由计算机管理员运行。 以下是 `Create` 命令的一个示例：  
  
```  
"<path>xdbcdcsvc.exe" create  
     <cdc-service-name>  
     [connect= "<sql-server-connection-string>"]  
     [key= <asym-key-password>]  
     [svcacct <windows-account> <windows-password>]  
     [sqlacct <sql-username> <sql-password>]  
```  
  
 其中：  
  
 **cdc-service-name** 是新创建的服务的名称。 如果已经有一个具有此名称的服务，则该程序将返回错误。 不应使用包含空格的长名称。 字符 "/" 和 "\\" 在服务名称中是无效字符。 这是必需参数。  
  
 **sql-server-connection-string** 是用于连接到与新的 Oracle CDC 服务相关联的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的连接字符串。  
  
 **asym-key-password** 是保护用于存储源数据库日志挖掘凭据的非对称密钥的密码。  
  
 **windows-account**、 **windows-password** 是与要创建的 Oracle CDC 服务相关联的帐户名称和密码。  
  
 **sql-username**、 **sql-password** 是用于连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帐户名称和密码。 如果上述这些参数是空的，则 Oracle CDC 服务将使用 Windows 身份验证连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
 **注意**：包含空格或双引号的任何参数都必须用双引号 (") 括起来。 嵌入的双引号必须双重使用（例如，若要使用 **"A#B" D** 作为密码，应输入 **""A#B"" D"**）。  
  
###  <a name="BKMK_delete"></a> 删除  
 使用 `Delete` 可从脚本完全删除 Oracle CDC 服务。 此命令必须由计算机管理员运行。 以下是 `Delete` 命令的一个示例。  
  
```  
"<path>xdbcdcsvc.exe" delete  
    <cdc-service-name>  
  
```  
  
 其中：  
  
 **cdc-service-name** 是要删除的 CDC 服务的名称。  
  
 **注意**：包含空格或双引号的任何参数都必须用双引号 (") 括起来。 嵌入的双引号必须双重使用（例如，若要使用 **"A#B" D** 作为密码，应输入 **""A#B"" D"**）。  
  
## <a name="see-also"></a>请参阅  
 [如何使用 CDC 服务命令行界面](how-to-use-the-cdc-service-command-line-interface.md)   
 [如何为 CDC 准备 SQL Server](prepare-sql-server-for-cdc.md)  
