---
title: Analysis Services 常规属性 |Microsoft Docs
ms.date: 04/04/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0683a8eb03cb0d5d17072825cfc90f8c9ba2500e
ms.sourcegitcommit: 3cfedfeba377560d460ca3e42af1e18824988c07
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/05/2019
ms.locfileid: "59042386"
---
# <a name="general-properties"></a>常规属性
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支持下表中列出的服务器属性。 本主题介绍 msmdsrv.ini 文件中未专门介绍的那些服务器属性，如 Security、Network 或 ThreadPool。 有关更多服务器属性以及如何设置这些属性的详细信息，请参阅 [Analysis Services 中的服务器属性](../../analysis-services/server-properties/server-properties-in-analysis-services.md)。  
  
 **适用范围：** 多维和表格服务器模式下，除非另有说明  
  
## <a name="non-specific-category"></a>非特定类别  
 **AdminTimeout**  
 有符号 32 位整数属性，用于定义管理员超时值（秒）。 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 此属性的默认值为零 (0)，指示没有超时设置。  
  
 **AllowedBrowsingFolders**  
 一个字符串属性，它在分隔的列表中指定在 Analysis Services 对话框中保存、打开和查找文件时可浏览的文件夹。 Analysis Services 服务帐户必须对您添加到该列表的所有文件夹都具有读写权限。  
  
 **BackupDir**  
 一个字符串属性，事件作为 Backup 命令的一部分未指定路径中标识的默认情况下，存储备份文件的目录名称。  
 
**ClientCacheRefreshPolicy**适用于仅 Azure Analysis Services。 重写**计划的缓存刷新**设置所有 Power BI 数据集。 Live Connect 的所有报表将都遵循服务器级别设置而不考虑数据集级设置，或在其所在的工作区。

此属性的默认值为-1，允许所有后台缓存都刷新计划的缓存刷新的数据集设置中指定。 若要禁止所有后台缓存刷新中，指定零 (0)。

  
 **CollationName**  
 字符串属性，用于标识服务器排序规则。 有关详细信息，请参阅[语言和排序规则 (Analysis Services)](../../analysis-services/languages-and-collations-analysis-services.md)。  
  
 **CommitTimeout**  
 一个整数属性，它指定服务器出于提交事务的目的将等待获取写入锁的时间（毫秒）。 通常需要一个等待时间，因为服务器必须等待其他锁释放，然后才能获取提交事务的写入锁。  
  
 此属性的默认值为零 (0)，指示服务器将无限期等待。 有关与锁相关的属性的详细信息，请参阅 [SQL Server 2008 R2 Analysis Services 操作指南](http://go.microsoft.com/fwlink/?LinkID=225539)。  
  
 **CoordinatorBuildMaxThreads**  
 有符号 32 位整数属性，用于定义为生成分区索引分配的最大线程数。 如果增加此值，则可加快分区索引速度，同时增加内存使用的开销。 有关此属性的详细信息，请参阅 [SQL Server 2008 R2 Analysis Services 操作指南](http://go.microsoft.com/fwlink/?LinkID=225539)。  
  
 **CoordinatorCancelCount**  
 有符号 32 位整数属性，用于定义服务器应检查是否发生取消事件的频率（基于内部迭代计数）。 如果减小此值，则可加快检查取消事件的频率，同时将降低系统的整体性能。 在表格服务器模式下将忽略此属性。  
  
 **CoordinatorExecutionMode**  
 有符号 32 位整数属性，用于定义服务器将尝试的最大并行操作（包括处理操作和查询操作）数。 零 (0) 指示服务器将基于内部算法来决定。 正数指示最大操作总数。 如果是符号相反的负数，则指示每个处理器的最大操作数。  

 此属性的默认值为 -4，指示将服务器限制为每个处理器 4 个并行操作。 有关此属性的详细信息，请参阅 [SQL Server 2008 R2 Analysis Services 操作指南](http://go.microsoft.com/fwlink/?LinkID=225539)。  
  
 **CoordinatorQueryMaxThreads**  
 有符号 32 位整数属性，用于定义在查询解析期间每个分区段的最大线程数。 并发用户数越少，此值就会越高，同时会增加内存开销。 相反，如果并发用户数很大，则此值就可能降低。  
  
 **CoordinatorShutdownMode**  
 布尔值属性，用于定义协调器关闭模式。 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **DataDir**  
 字符串属性，用于标识存储数据的目录的名称。  
  
 **DeploymentMode**  
 确定 Analysis Services 服务器实例的操作上下文。 此属性称为服务器模式对话框、 消息和文档中。 此属性由 SQL Server 安装程序根据安装 Analysis Services 时所选择的服务器模式进行相应配置。 只应考虑在内部使用此属性，并且始终使用安装程序指定的值。  
  
 此属性的有效值包括以下项：  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|0|这是默认值。 它指定多维模式，用于支持使用 MOLAP、HOLAP 和 ROLAP 存储以及数据挖掘模型的多维数据库。|  
|1|指定 Analysis Services 实例已作为 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 部署的一部分安装。 不要更改作为 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 安装的一部分的 Analysis Services 实例的部署模式属性。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据将不再在该服务器上运行。|  
|2|指定用于承载使用内存中存储或 DirectQuery 存储的表格模型数据库的表格模式。|  
  
 每个模式与其他模式都是互斥的。 配置为表格模式的服务器不能运行包含多维数据集和维度的 Analysis Services 数据库。 如果基础计算机硬件能够支持，则您可以在同一台计算机上安装 Analysis Services 的多个实例并且对每个实例进行配置以便使用不同的部署模式。 请记住，Analysis Services 是一种消耗大量资源的应用程序。 仅推荐对于高端服务器，才在同一个系统上部署多个实例。  
  
 **EnableFast1033Locale**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **ExternalCommandTimeout**  
 一个整数属性，用于定义向外部服务器（包括关系数据源和外部 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务器）发出的命令的超时值（秒）。  
  
 此属性的默认值为 3600（秒）。  
  
 **ExternalConnectionTimeout**  
 一个整数属性，用于定义创建到外部服务器（包括关系数据源和外部 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务器）的连接的超时值（秒）。 如果在连接字符串中指定了连接超时，则忽略此属性。  
  
 此属性的默认值为 60（秒）。  
  
 **ForceCommitTimeout**  
 一个整数属性，它指定写入提交操作在取消先于当前命令（包括正在处理的查询）执行的其他命令之前应等待的时间（毫秒）。 这允许提交事务通过取消较低优先级的操作（例如查询）来继续。  
  
 此属性的默认值为 30 秒（30000 毫秒），指示在提交事务已等待 30 秒之前，其他命令不会被强制超时。  
  
> [!NOTE]  
>  被此事件取消的查询和进程将报告以下错误消息：“`Server: The operation has been cancelled`”  
  
 有关此属性的详细信息，请参阅 [SQL Server 2008 R2 Analysis Services 操作指南](http://go.microsoft.com/fwlink/?LinkID=225539)。  
  
> [!IMPORTANT]  
>  **ForceCommitTimeout** 适用于多维数据集处理命令和写回操作。  
  
 **IdleConnectionTimeout**  
 一个整数属性，指定处于非活动状态的连接的超时值（秒）。  
  
 此属性的默认值为零 (0)，指示空闲连接将不使用超时。  
  
 **IdleOrphanSessionTimeout**  
 一个整数属性，用于定义孤立会话将在服务器内存中保留的时间（秒）。 孤立会话是一种不再具有关联的连接的会话。 默认值为 120 秒。  
  
 **InstanceVisible**  
 一个布尔值属性，指示服务器实例对来自 SQL Server Browser 服务的发现实例请求是否可见。 默认值为 True。 如果将该属性设置为 false，则该实例对于 SQL Server Browser 不可见。  
  
 **语言**  
 字符串属性，用于定义语言（包括错误消息和数字格式）。 此属性优先级高于 CollationName 属性。  
  
 此属性的默认值为空，指示 CollationName 属性定义语言。  
  
 **LogDir**  
 字符串属性，用于标识包含服务器日志的目录的名称。 此属性仅适用于使用磁盘文件进行日志记录的情况，这一点与数据库表相反（默认行为）。  
  
 **MaxIdleSessionTimeout**  
 一个整数属性，用于定义空闲会话最大超时值（秒）。 默认值为零 (0)，该值指示会话永远不会超时。但是，如果服务器受到资源约束，空闲会话仍将被删除。  
  
 **MinIdleSessionTimeout**  
 一个整数属性，用于定义空闲会话最小超时值（秒）。 默认值为 2700 秒。 达到此时间后，服务器可以终止空闲会话，但只在需要释放内存时才这样做。  
  
 **端口**  
 一个整数属性，用于定义服务器侦听客户端连接所在的端口号。 如果未设置，服务器将动态查找第一个未使用的端口。  
  
 此属性的默认值为零 (0)，指示默认侦听端口 2383。 有关端口配置的详细信息，请参阅 [将 Windows 防火墙配置为允许 Analysis Services 访问](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)。  
  
 **ServerTimeout**  
 一个整数，用于定义查询的超时值（秒）。 默认值为 3600 秒（或 60 分钟）。 零 (0) 指定任何查询都不会超时。  
  
 **TempDir**  
 一个字符串属性，指定用于存储在处理、还原和其他操作过程中使用的临时文件的位置。 此属性的默认值由安装程序确定。 如果未指定，则默认为 Data 目录。  
  
## <a name="requestprioritization-category"></a>RequestPrioritization 类别  
 **已启用**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **StatisticsStoreSize**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 中的服务器属性](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [确定 Analysis Services 实例的服务器模式](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
