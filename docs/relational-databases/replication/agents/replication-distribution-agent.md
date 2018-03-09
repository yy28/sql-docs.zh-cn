---
title: "复制分发代理 | Microsoft Docs"
ms.custom: 
ms.date: 02/23/2016
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
- Distribution Agent, executables
- agents [SQL Server replication], Distribution Agent
- Distribution Agent, parameter reference
- command prompt [SQL Server replication]
ms.assetid: 7b4fd480-9eaf-40dd-9a07-77301e44e2ac
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: b3a92cdd309e4bc4c60ff922b8444d810a2981cf
ms.sourcegitcommit: d8ab09ad99e9ec30875076acee2ed303d61049b7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/23/2018
---
# <a name="replication-distribution-agent"></a>复制分发代理
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
复制分发代理是一个可执行文件，它能将快照（对于快照复制和事务复制）和保存在分发数据库表中的事务（对于事务复制）移动到订阅服务器上的目标表中。  
  
> [!NOTE]  
>  可以按任意顺序指定参数。 如果未指定可选参数，将使用本地计算机上预定义的注册表设置中的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
distrib [-?]  
-Publisher server_name[\instance_name]  
-PublisherDB publisher_database  
-Subscriber server_name[\instance_name]  
-SubscriberDB subscriber_database   
[-AltSnapshotFolder alt_snapshot_folder_path]   
[-BcpBatchSize bcp_batch_size]  
[-CommitBatchSize commit_batch_size]  
[-CommitBatchThreshold commit_batch_threshold]  
[-Continuous]  
[-DefinitionFile def_path_and_file_name]  
[-Distributor distributor]  
[-DistributorLogin distributor_login]  
[-DistributorPassword distributor_password]  
[-DistributorSecurityMode [0|1]]  
[-EncryptionLevel [0|1|2]]  
[-ErrorFile error_path_and_file_name]  
[-ExtendedEventConfigFile configuration_path_and_file_name]  
[-FileTransferType [0|1]]  
[-FtpAddress ftp_address]  
[-FtpPassword ftp_password]   
[-FtpPort ftp_port]  
[-FtpUserName ftp_user_name]  
[-HistoryVerboseLevel [0|1|2|3]]  
[-Hostname host_name]  
[-KeepAliveMessageInterval keep_alive_message_interval_seconds]  
[-LoginTimeOut login_time_out_seconds]  
[-MaxBcpThreads]  
[-MaxDeliveredTransactions number_of_transactions]  
[-MessageInterval message_interval]  
[-OledbStreamThreshold oledb_stream_threshold]  
[-Output output_path_and_file_name]  
[-OutputVerboseLevel [0|1|2]]  
[-PacketSize packet_size]  
[-PollingInterval polling_interval]  
[-ProfileName profile_name]  
[-Publication publication]  
[-QueryTimeOut query_time_out_seconds]  
[-QuotedIdentifier quoted_identifier]  
[-SkipErrors native_error_id [:...n]]  
[-SubscriberDatabasePath subscriber_path]  
[-SubscriberLogin subscriber_login]  
[-SubscriberPassword subscriber_password]  
[-SubscriberSecurityMode [0|1]]  
[-SubscriberType [0|1|3]]  
[-SubscriptionStreams [1|2|...64]]  
[-SubscriptionTableName subscription_table]  
[-SubscriptionType [0|1|2]]  
[-TransactionsPerHistory [0|1|...10000]]  
[-UseDTS]  
[-UseInprocLoader]  
[-UseOledbStreaming]  
```  
  
## <a name="arguments"></a>参数  
 **-?**  
 输出所有可用的参数。  
  
 **-Publisher** *server_name*[**\\***i**nstance_name*]  
 发布服务器的名称。 为该服务器上的 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 默认实例指定 *server_name*。 为该服务器上的 *server_name***\\***instance_name* instance_name [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
 **-PublisherDB** *publisher_database*  
 发布服务器数据库的名称。  
  
 **-Subscriber** *server_name*[**\\***instance_name*]  
 订阅服务器的名称。 为该服务器上的 *默认实例指定* server_name [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。 为该服务器上的 *server_name***\\***instance_name* instance_name [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
 **-SubscriberDB** *subscriber_database*  
 订阅服务器数据库的名称。  
  
 **-AltSnapshotFolder** *alt_snapshot_folder_path*  
 包含订阅的初始快照的文件夹路径。  
  
 **-BcpBatchSize** *bcp_batch_size*  
 在一次大容量复制操作中发送的行数。  执行 **bcp in** 操作时，批的大小为要作为一个事务发送到服务器的行数，并且也是分发代理记录 bcp 进度消息之前必须发送的行数。 当执行 **bcp out** 操作时，将使用固定批大小 **1000** 。  
  
 **-CommitBatchSize** *commit_batch_size*  
 发出 COMMIT 语句前要发给订阅服务器的事务数。 默认值为 100。  
  
 **-CommitBatchThreshold**  *commit_batch_threshold*  
 发出 COMMIT 语句前要发给订阅服务器的复制命令数。 默认值为 1000。  
  
 **-Continuous**  
 指定代理是否尝试连续轮询已复制的事务。 如果指定了该参数，即使没有事务挂起，代理也将在轮询间隔期间轮询来自源的已复制事务。  
  
 **-DefinitionFile** *def_path_and_file_name*  
 代理定义文件的路径。 代理定义文件中包含代理的命令提示符参数。 文件的内容被当作可执行文件进行分析。 使用双引号 (") 指定包含任意字符的参数值。  
  
 **-Distributor** *distributor*  
 分发服务器名称。 对于分发服务器（推送）分发，该名称默认为本地分发服务器的名称。  
  
 **-DistributorLogin** *distributor_login*  
 分发服务器登录名。  
  
 **-DistributorPassword** *distributor_password*  
 分发服务器密码。  
  
 **-DistributorSecurityMode** [ **0**| **1**]  
 指定分发服务器的安全模式。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 值为 0，表示为  身份验证模式，值为 1，表示为 Windows 身份验证模式（默认）。  
  
 **-EncryptionLevel** [ **0** | **1** | **2** ]  
 分发代理建立连接时使用的安全套接字层 (SSL) 加密级别。  
  
|EncryptionLevel 值|Description|  
|---------------------------|-----------------|  
|**0**|指定不使用 SSL。|  
|**1**|指定使用 SSL，但是代理不验证 SSL 服务器证书是否已由可信的颁发者进行签名。|  
|**2**|指定使用 SSL，并验证证书。|  
  
 有关详细信息，请参阅[安全性概述（复制）](../../../relational-databases/replication/security/security-overview-replication.md)。  
  
 **-ErrorFile** *error_path_and_file_name*  
 分发代理生成的错误文件的路径和文件名。 在订阅服务器上应用复制事务时，在故障发生位置生成此文件；在发布服务器或分发服务器上出现的错误不记录在此文件中。 此文件包含失败的复制事务和相关的错误消息。 如果没有指定，则在分发代理的当前目录中生成此错误文件。 错误文件名为分发代理的名称，扩展名为 .err。 如果指定的文件名已存在，会将错误消息追加到该文件中。 此参数最多可包含 256 个 Unicode 字符。  
  
 **-ExtendedEventConfigFile** *configuration_path_and_file_name*  
 为扩展事件 XML 配置文件指定路径和文件名。 通过该扩展事件 XML 配置文件，您可以配置会话并且启用事件跟踪。  
  
 **-FileTransferType** [ **0**| **1**]  
 指定文件传输类型。  值为 **0** ，表示 UNC（通用命名约定），值为 1，表示 FTP（文件传输协议）。  
  
 **-FtpAddress** *ftp_address*  
 分发服务器的 FTP 服务网络地址。  未指定该参数时，使用 DistributorAddress。  如果未指定 **DistributorAddress** ，将使用 Distributor。  
  
 **-FtpPassword** *ftp_password*  
 用于连接到 FTP 服务的用户密码。  
  
 **-FtpPort** *ftp_port*  
 分发服务器 FTP 服务的端口号。 如果不指定，则使用 FTP 服务的默认端口号 (21)。  
  
 **-FtpUserName**  *ftp_user_name*  
 用于连接到 FTP 服务的用户名。  如果不指定，则使用 anonymous。  
  
 **-HistoryVerboseLevel** [ **0** | **1** | **2** | **3** ]  
 指定分发操作期间记录的历史信息量。 选择 1 可将历史日志记录对性能的影响减小到最低限度。  
  
|HistoryVerboseLevel 值|Description|  
|-------------------------------|-----------------|  
|**0**|进度消息将写入控制台或输出文件。 不在分发数据库中记录历史记录。|  
|**1**|默认值。 总是更新具有相同状态（启动、进行中、成功等）的上一历史记录消息。 如果不存在状态相同的上一记录，将插入新记录。|  
|**2**|除非记录为空闲消息或长时间运行的作业消息等信息（此时将更新上一记录），否则插入新的历史记录。|  
|**3**|始终插入新记录，除非它与空闲消息有关。|  
  
 **-Hostname** *host_name*  
 连接到发布服务器时使用的主机名。 此参数最多可包含 128 个 Unicode 字符。  
  
 **-KeepAliveMessageInterval** *keep_alive_message_interval_seconds*  
 在历史记录线程检查目前是否有连接在等待服务器响应之前等待的秒数。 在执行长时间运行的批处理时，减小该值可避免检查代理将分发代理标记为可疑。 默认值为 **300** 秒。  
  
 **-LoginTimeOut** *login_time_out_seconds*  
 登录超时前等待的秒数。 默认值为 15 秒。  
  
 **-MaxBcpThreads** *number_of_threads*  
 指定可以并行执行的大容量复制操作的数量。 同时存在的线程和 ODBC 连接的最大数量为 **MaxBcpThreads** 或显示在分发数据库中同步事务中的大容量复制请求数中较小的那一个。 **MaxBcpThreads** 的值必须大于 **0** ，并且不存在任何硬编码的上限。  默认值是处理器数目的 **2**倍，最大值为 8。 应用于使用并发快照选项在发布服务器上生成的快照时，不管为 **MaxBcpThreads**指定了什么数值，都将使用一个线程。  
  
 **-MaxDeliveredTransactions** *number_of_transactions*  
 一次同步期间应用于订阅服务器的推送事务或请求事务的最大数量。  值为 0，表示最大值为无穷多个事务。 订阅服务器可使用其他值缩短从发布服务器请求的同步的持续时间。  
  
> [!NOTE]  
>  如果同时指定了 -MaxDeliveredTransactions 和 -Continuous，分发代理将传送指定数目的事务，然后停止（即使指定了 -Continuous）。 在作业完成后，您必须重新启动分发代理。  
  
 **-MessageInterval**  *message_interval*  
 用于历史日志记录的时间间隔。 当达到以下参数值之一时，将记录一个历史记录事件：  
  
-   记录上一历史记录事件后，达到 **TransactionsPerHistory** 值。  
  
-   记录上一历史记录事件后，达到 **MessageInterval** 值。  
  
 如果源上没有可用的已复制事务，代理将向分发服务器报告无事务消息。 此选项可指定代理在报告另一条无事务消息前将等待多长时间。 在上次处理已复制事务后，如果代理在源上没有检测到任何可用的事务，则总是会报告一条无事务消息。 默认值为 60 秒。  
  
 **-OledbStreamThreshold** *oledb_stream_threshold*  
 指定二进制大型对象数据的最小大小（按字节计），如果超过此大小，数据将作为流进行绑定。 必须将 **–UseOledbStreaming** 指定为使用此参数。 值可以介于 400 个字节到 1048576 个字节之间，默认值为 16384 个字节。  
  
 **-Output** *output_path_and_file_name*  
 代理输出文件的路径。 如果未提供文件名，则向控制台发送该输出。 如果指定的文件名已存在，会将输出追加到该文件。  
  
 **-OutputVerboseLevel** [ **0**| **1**| **2**]  
 指定输出是否应提供详细内容。 如果详细级别为 0，则只输出错误消息。 如果详细级别为 1，则输出所有进度报告消息。  如果详细级别为 2（默认），则输出所有错误消息和进度消息，这对调试很有帮助。  
  
 **-PacketSize** *packet_size*  
 数据包大小（按字节计）。 默认值为 4096（字节）。  
  
 **-PollingInterval** *polling_interval*  
 对分发数据库进行已复制事务查询的频率（以秒计）。 默认值为 5 秒。  
  
 **-ProfileName** *profile_name*  
 指定用于代理参数的代理配置文件。 如果 **ProfileName** 为 NULL，则将禁用代理配置文件。 如果未指定 **ProfileName** ，则使用该代理类型的默认配置文件。 有关信息，请参阅[复制代理配置文件](../../../relational-databases/replication/agents/replication-agent-profiles.md)。  
  
 **-Publication**  *publication*  
 发布的名称。 只有将发布设置为总是使快照可用于新订阅或重新初始化的订阅时，此参数才有效。  
  
 **-QueryTimeOut** *query_time_out_seconds*  
 查询超时前等待的秒数。默认值为 1800 秒。  
  
 **-QuotedIdentifier** *quoted_identifier*  
 指定要使用的带引号的标识符字符。 该值的第一个字符表示分发代理使用的值。 如果使用不带有任何值的 **QuotedIdentifier** ，则分发代理使用一个空格。 如果未使用 **QuotedIdentifier** ，则分发代理使用订阅服务器支持的任意带引号的标识符。  
  
 **-SkipErrors** *native_error_id* [**:***...n*]  
 以冒号分隔的列表，指定此代理要跳过的错误号。  
  
 **-SubscriberDatabasePath** *subscriber_database_path*  
 如果 **SubscriberType** 为 **2** （允许建立到 Jet 数据库的连接，而无需 ODBC 数据源名称 (DSN)），则为 Jet 数据库（.mdb 文件）的路径。  
  
 **-SubscriberLogin** *subscriber_login*  
 订阅服务器登录名。 如果 **SubscriberSecurityMode** 为 **0** （对于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 身份验证），则必须指定此参数。  
  
 **-SubscriberPassword** *subscriber_password*  
 订阅服务器密码。 如果 **SubscriberSecurityMode** 为 **0** （对于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 身份验证），则必须指定此参数。  
  
 **-SubscriberSecurityMode** [ **0**| **1**]  
 指定订阅服务器的安全模式。  值为 0 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ，表示为  身份验证，值为 1，表示为 Windows 身份验证模式（默认）。  
  
 **-SubscriberType** [ **0**| **1**| **3**]  
 指定分发代理使用的订阅服务器连接类型。  
  
|SubscriberType 值|Description|  
|--------------------------|-----------------|  
|**0**|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|  
|**1**|ODBC 数据源|  
|**3**|OLE DB 数据源|  
  
 **-SubscriptionStreams** [**0**|**1**|**2**|...**64**]  
 每个分发代理允许的连接数，用于将成批更改并行应用于订阅服务器，同时保留在使用单线程时具有的多种事务特征。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 对于  发布服务器，支持介于 1 到 64 之间的值。 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 只有当发布服务器和分发服务器均在  或更高版本上运行时，才支持此参数。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 对于非  订阅服务器或对等订阅，不支持此参数或者参数必须为 0。  
  
> [!NOTE]  
>  如果有一个连接无法执行或提交，则所有连接将中止当前批处理，而且代理将用单独的流重试失败的批处理。 在重试阶段完成之前，订阅服务器上会存在临时事务不一致。 失败的批处理成功提交后，订阅服务器将恢复到事务一致状态。  
  
> [!IMPORTANT]  
>  将 **-SubscriptionStreams**的值指定为 2 或更大的数字时，订阅服务器接收事务的顺序可能与发布服务器提交事务的顺序不同。 如果此行为在同步期间导致约束冲突，则应使用 NOT FOR REPLICATION 选项禁止在同步期间强制执行约束。 有关详细信息，请参阅[控制同步期间触发器和约束的行为（复制 Transact-SQL 编程）](../../../relational-databases/replication/control-behavior-of-triggers-and-constraints-in-synchronization.md)。  
  
> [!NOTE]  
>  [!INCLUDE[tsql](../../../includes/tsql-md.md)]订阅流不适用于配置为传递  的项目。 若要使用订阅流，请改将项目配置为传递存储过程调用。  
  
 **-SubscriptionTableName** *subscription_table*  
 在给定订阅服务器上生成或使用的订阅表的名称。 如果未指定，将使用 [MSreplication_subscriptions (Transact-SQL)](../../../relational-databases/system-tables/msreplication-subscriptions-transact-sql.md) 表。 可将此选项用于不支持长文件名的数据库管理系统 (DBMS)。  
  
 **-SubscriptionType** [ **0**| **1**| **2**]  
 指定分发的订阅类型。  值为 **0** ，表示推送订阅，值为 **1** ，表示请求订阅，值为 2，表示匿名订阅。  
  
 **-TransactionsPerHistory** [ **0**| **1**|...**10000**]  
 指定历史日志记录的事务间隔。 如果自历史日志记录上一实例之后的已提交事务数大于此选项，将记录历史记录消息。 默认值为 100。 值 **0** 表示无限 **TransactionsPerHistory**。 See the preceding **–MessageInterval**parameter.  
  
 **-UseDTS**  
 必须指定为允许数据转换的发布的参数。  
  
 **-UseInprocLoader**  
 通过让分发代理在将快照文件应用于订阅服务器时使用 BULK INSERT 命令，提高初始快照的性能。 不推荐使用此参数，因为它与 XML 数据类型不兼容。 如果不复制 XML 数据，则可以使用此参数。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 此参数不可用于字符模式快照或非  订阅服务器。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 如果使用此参数，订阅服务器上的  服务帐户必须具有快照 .bcp 数据文件所在目录的读取权限。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 如果不使用此参数，代理（对于非 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 订阅服务器）或代理加载的 ODBC 驱动程序（对于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 订阅服务器）从文件中读取数据，因此不使用  服务帐户的安全上下文。  
  
 **-UseOledbStreaming**  
 指定此参数时，可以将二进制大型对象数据作为流进行绑定。 使用 **-OledbStreamThreshold** 指定大小（按字节计），超过此大小时将使用流。 **UseOledbStreaming** 默认为启用状态。 **UseOledbStreaming** 写入到 **C:\Program Files\Microsoft SQL Server\\<version\>\COM** 文件夹。  
  
## <a name="remarks"></a>Remarks  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 如果安装了  代理以在本地系统帐户而非域用户帐户（默认）下运行，则服务只能访问本地计算机。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 如果将以 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]代理身份运行的分发代理配置为在登录到  实例时使用 Windows 身份验证模式，则分发代理将失败。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 默认设置为  身份验证。 [View and Modify Replication Security Settings](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)有关更改安全帐户的详细信息，请参阅。  
  
 若要启动分发代理，请从命令提示符下执行 **distrib.exe** 。 有关信息，请参阅[复制代理可执行文件概念](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)。  
  
## <a name="change-history"></a>更改历史记录  
  
|更新的内容|  
|---------------------|  
| 添加了 -ExtendedEventConfigFile 参数。|  
  
## <a name="see-also"></a>另请参阅  
 [复制代理管理](../../../relational-databases/replication/agents/replication-agent-administration.md)  
  
  
