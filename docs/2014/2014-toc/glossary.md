---
title: 术语表 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- definitions [SQL Server]
- glossary [SQL Server]
- terminology [SQL Server]
ms.assetid: 0e8a7967-b407-4e01-b8c4-3eabe2820df5
author: heidisteen
ms.author: heidist
ms.openlocfilehash: 1f55c4388fdc75eb531e74ffb6ffc5f24804c163
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2020
ms.locfileid: "84528293"
---
# <a name="glossary"></a>术语表

<!--
Metadata 'ms.technology:' is restricted to a maximum of one value.
So I am erasing all the values shown below.  (GeneMi , 2019/04/19)

ms.technology:
  - "analysis-services"
  - "analysis-services/data-mining"
  - "analysis-services/multidimensional-tabular"
  - "data-quality-services"
  - "database-engine"
  - "integration-services"
  - "master-data-services"
  - "replication"
  - "reporting-services-native"
  - "reporting-services-sharepoint"
-->

## <a name="terms"></a>术语  
  
|术语|定义|  
|----------|----------------|  
|action|最终用户启动的、针对所选多维数据集或其某部分执行的操作。|  
|ActiveX 数据对象 (ActiveX Data Objects)|与符合 OLE DB 的数据源进行通信以便连接到、检索、处理和更新数据的数据访问接口。|  
|ActiveX 数据对象（多维）(ActiveX Data Objects (Multidimensional))|一组基于对象的高级数据访问接口，它不依赖于语言，并且针对多维数据应用进行了优化。|  
|适配器主机 (adapter host)|根抽象类适配器，用于定义在 ENQUEUE 交互点处适配器与 StreamInsight 服务器之间的握手。 它提供所有必需的适配器服务（如内存管理）和异常处理。|  
|ADO|与符合 OLE DB 的数据源进行通信以便连接到、检索、处理和更新数据的数据访问接口。|  
|ADO MD|一组基于对象的高级数据访问接口，它不依赖于语言，并且针对多维数据应用进行了优化。|  
|ADOMD.NET|.NET 托管的数据访问接口，提供对多维数据源（例如 Microsoft SQL Server Analysis Services）的访问。|  
|聚合函数|对多个值执行计算并返回单个值的函数。|  
|聚合查询 (aggregate query)|通过包括聚合函数（例如 Sum 或 Avg）来汇总多行信息的查询（SQL 语句）。|  
|aggregation|包含用于联机分析处理 (OLAP) 多维数据集的预先计算数据的表或结构。 聚合支持针对多维数据库的快速且高效的查询。|  
|聚合前缀 (aggregation prefix)|与系统定义的 ID 组合使用的字符串，用来为分区的聚合表生成唯一的名称。|  
|聚合包装 (aggregation wrapper)|将一个 COM 对象封装到另一个 COM 对象内的包装。|  
|alias|用于某个对象（例如文件或数据集合）的替代标签。|  
|别名类型 (alias type)|基于 SQL Server 系统数据类型之一的用户定义的数据类型，可指定某个数据类型、长度和为 Null 性。|  
|对齐 (alignment)|当索引与其对应的表建立在同一个分区方案之上时的情况。|  
|分配单元 (allocation unit)|可以作为一个整体进行操作的一组页。 属于某一分配单元的页由索引分配映射 (IAM) 页进行跟踪。 一个分配单元由 IAM 页链以及在该 IAM 页链中标记为已分配的所有页构成。 一个分配单元最多只能包含一个 IAM 链，并且一个 IAM 链必须属于一个且仅限一个分配单元。|  
|AMO|Analysis Services 随附的 .NET 命名空间的集合，用于为客户端应用程序提供管理功能。|  
|分析管理对象|Analysis Services 随附的 .NET 命名空间的集合，用于为客户端应用程序提供管理功能。|  
|分析数据 (analytical data)|提供与空间数据相关联的值的数据。 例如，空间数据定义某个地区中各市县的位置，而分析数据提供每个市县的人口数。|  
|祖先 (ancestor)|树结构中给定元素是其子级的元素。 等效于父元素。|  
|祖先元素 (ancestor element)|树结构中给定元素是其子级的元素。 等效于父元素。|  
|定位点端 (anchor cap)|顶端宽度要大于线条宽度的线条顶端。|  
|定位点成员 (anchor member)|递归 CTE 的第一个调用包括一个或多个由 UNION ALL、UNION、EXCEPT 或 INTERSECT 运算符联接的 CTE_query_definition。 由于这些查询定义形成了 CTE 结构的基准结果集，所以它们被称为“定位点成员”。|  
|动画管理器 (animation manager)|用于管理（创建、计划和控制）动画的动画应用程序和中央编程接口的核心组件。|  
|匿名订阅 (anonymous subscription)|一种请求订阅，不保存有关这种订阅及相应订阅服务器的详细信息。|  
|ANSI 到 OEM 转换 (ANSI to OEM conversion)|当数据从使用特定的代码页存储字符数据的数据库传输到计算机上使用不同代码页的某一客户端应用程序时必须发生的字符转换。 通常，基于 Windows 的客户端计算机使用 ANSI/ISO 代码页，但某些数据库（出于兼容原因）可能会使用 OEM 代码页。|  
|API 服务器游标 (API server cursor)|为了支持 API（如 ODBC、OLE DB、ADO 和 DB-Library）的游标函数而生成的服务器游标。|  
|API 支持|应用程序用来请求和执行计算机的操作系统所执行的低级别服务的一组例程。 这些例程通常执行维护任务，例如管理文件和显示信息。|  
|应用程序角色|为满足应用程序的安全性需要而创建的一种 SQL Server 角色。|  
|应用程序时间 (application time)|由必须将其应用程序时间传达给 StreamInsight 服务器（以便所有临时运算符都会引用事件的时间戳，而永远不会引用主机的系统时钟）的应用程序提供的时钟时间。|  
|应用分支 (apply branch)|应用于事件组的操作集。|  
|仲裁端口 (arbitration port)|缓存主机为确定群集中某个缓存主机是否变得不可用而使用的 TCP/IP 端口。 用于仲裁的端口号在各个缓存主机上可以不同。|  
|ARIMA|用于确定按时间顺序进行的观察中的依赖关系的一种方法，该方法还支持倍乘季节性。|  
|article|发布中的组件。 例如，表、列或行。|  
|程序集 (assembly)|一种以 SQL Server 中的对象形式包含类元数据和托管代码的托管应用程序模块，在 SQL Server 中可通过引用程序集来创建 CLR 函数、存储过程、触发器、用户定义聚合和用户定义类型。|  
|相关数组 (associative array)|由键的集合和值的集合构成的数组，其中的每个键都与一个值相关联。 键和值可以是任何类型。|  
|Atom 馈送 (atom feed)|包含与内容有关的元数据（例如语言版本和上次修改内容的日期）并且通过使用 Atom 发布协议 (AtomPub) 发送到订阅服务器的一种 XML 结构。|  
|原子 (atomic)|与所有事务数据修改都必须执行的操作相关；要么执行所有事务数据修改，要么不执行任何数据修改。|  
|attribute|在数据库中存在的信息（财务或非财务）的一个特性或附加部分。|  
|属性层次结构 (attribute hierarchy)|包含单个属性的平面层次结构（通常具有一个“所有”级别和一个成员级别）。 它是从维度表中的一列创建的（如果多维数据集支持）。|  
|属性关系 (attribute relationship)|与属性关联的层次结构，包含基于维度表中对应列的单个级别。|  
|属性类型 (attribute type)|某一属性包含的信息的类型，例如时间维度中的季度或月份，可由服务器和客户端应用程序实现特定的处理。|  
|审核|操作系统用于检测和记录与安全相关的事件（例如尝试创建、访问或删除文件和目录之类的对象）的过程。 此类事件的记录存储于称作安全日志的文件中，其内容仅可用于具有正确权限的人士。|  
|authentication|是指通过验证实体提供的凭据来验证用户、计算机、过程或其他实体身份的过程。 凭据的常见形式有数字签名、智能卡、生物统计数据以及用户名和密码的组合。|  
|验证器 (authenticator)|由一方用来证明另一方知道某个密钥的数据结构。 在 Kerberos 身份验证协议中，身份验证因子包括用于防止重播攻击的时间戳并且使用密钥分发中心 (KDC) 颁发的会话密钥进行加密。|  
|authorization|将访问某些信息、服务或功能的权限授予个人、计算机进程或设备的过程。 授权派生自人员、计算机进程或请求访问的设备的标识，并且通过身份验证进行验证。|  
|自动提交模式|用于数据库引擎的默认事务管理模式。 数据库引擎自动为每个单独的 Transact-SQL 语句启动一个事务。 在该语句完成后，将基于该语句是成功还是失败来提交或回滚事务。|  
|自动一致性检查 (auto-consistency check)|在检测到不一致的副本时自动对保护的数据源运行一致性检查的一种功能。|  
|自动故障转移 (automatic failover)|在丢失主副本时自动发生的故障转移。|  
|自动恢复 (automatic recovery)|每次重新启动 SQL Server 时发生的恢复。|  
|自动保护 (auto-protection)|在 DPM 中，一种为保护自动标识和添加新数据源的功能。|  
|自动回归集成移动平均 (autoregressive integrated moving average)|用于确定按时间顺序进行的观察中的依赖关系的一种方法，该方法还支持倍乘季节性。|  
|轴|一个元组集。 每个元组是一个成员向量。 一组轴定义一个多维数据集的坐标。|  
|备份集 (backup set)|已经备份并存储在一个文件或者一个或多个磁带上的文件、文件夹和其他数据的集合。|  
|均衡层次结构 (balanced hierarchy)|一种所有叶节点与根节点的距离都相同的维度层次结构。|  
|基准备份 (base backup)|数据库或文件的数据备份，差异备份就是完全或部分基于该备份进行的。 基准备份是数据库或文件的最近的完整备份或文件备份。|  
|基本数据类型 (base data type)|任何系统提供的数据类型，例如 char、varchar、binary 和 varbinary。 用户定义的数据类型将从基本数据类型派生。|  
|base object|同义词引用的对象。|  
|基表 (base table)|数据库中永久存储的表。 基表可由视图、游标、SQL 语句和存储过程引用。|  
|基本标记地图 (basic marker map)|在每个位置（如城市）显示一个标记并且变化标记颜色、大小和类型的地图。|  
|或批处理|分组在一起的一组请求或事务。|  
|批处理作业 (batch job)|无需用户交互即可运行的一组计算机进程。|  
|批处理 (batch processing)|批处理文件的执行。|  
|blittable 类型 (blittable type)|具有唯一特性并且在内存中为托管环境和非托管环境具有完全相同的显示的一种数据类型。 此数据类型可直接共享。|  
|BLOB|异常巨大的二进制数据离散包（例如以数字数据格式存储的图片或乐曲曲目），或足够存放此类值的任何变量或表列。 指定“二进制大型对象”通常表示在数据库中存储并被视作未解释字节序列的数据包。|  
|block|位于 BEGIN 和 END 之间的一种 Transact-SQL 语句。|  
|块状游标 (block cursor)|行集大小大于 1 的游标。|  
|阻塞事务 (blocking transaction)|导致另一个事务的失败的事务。|  
|布尔表达式 (Boolean expression)|生成布尔值（true 或 false）的表达式。 此类表达式可以涉及比较（测试值是否相等，或对于非布尔值， \< [less than] or > [大于] 关系）和逻辑组合（使用布尔运算符，如 and、or 和 XOR）的布尔表达式。|  
|布尔运算符 (Boolean operator)|设计为与布尔值协同使用的运算符。 在编程中最常用的四个公用布尔运算符是 AND（逻辑与）、OR（逻辑或）、XOR（异或）或 NOT（逻辑反）。|  
|绑定流 (bound stream)|包含生成事件所需的所有信息的事件流。 信息或者是已经实例化的数据源，或者非常充分足以让 StreamInsight 服务器启动该数据源。|  
|边界框|将容纳对象的路径、形状或组的最小矩形区域。|  
|浏览模式 (browse mode)|一种功能，使用它可以扫描数据库行并且每次更新一行的值。|  
|B 树 (B-tree)|用于存储数据库索引的一种树结构。|  
|气泡图 (bubble map)|一种地理图，它在特定位置的上方显示一个圆形，其中，圆形的半径与某一数值成比例。|  
|缓冲池 (buffer pool)|为索引和表数据页保留的内存块。|  
|缓冲区大小 (buffer size)|为临时存储数据而保留的内存区域的大小。|  
|内置函数 (built-in functions)|作为 Transact-SQL 和多维表达式语言的一部分提供的一组预定义函数。|  
|BUILTIN\Administrators|用户帐户（本地管理员）|  
|大容量复制|复制大量数据的操作。|  
|大容量导出 (bulk export)|将大量数据行从 SQL Server 表复制到数据文件中。|  
|大容量导入|将大量数据（通常分批）从数据文件或存储库复制到其他数据存储库中。|  
|大容量加载 (bulk load)|将大量行插入表的操作。|  
|大容量日志备份 (bulk log backup)|包含大容量操作更改的日志和数据页的备份。 不允许执行时间点恢复。|  
|大容量行集提供程序 (bulk rowset provider)|供 OPENROWSET 指令用来从文件读取数据的提供程序。 在 SQL Server 2005 中，OPENROWSET 无需将数据文件中的数据加载到目标表，便可读取这些数据。 这使您可在单个 SELECT 语句中使用 OPENROWSET。|  
|大容量日志恢复模式 (bulk-logged recovery model)|一种数据库恢复模式，可在完整记录其他事务的同时最小限度地记录大容量操作（例如索引创建和大容量导入）。 大容量日志恢复可提高大容量操作的性能，并且旨在用作对完整恢复模式的补充。|  
|Business Intelligence Development Studio|用于商业智能解决方案开发人员的项目开发和管理工具。 可用于设计将来自 Microsoft SQL Server Analysis Services (SSAS)、Microsoft SQL Server Integration Services (SSIS) 和 Microsoft SQL Server Reporting Services (SSRS) 的项目集成在一起的端到端商业智能解决方案。|  
|业务逻辑 (business logic)|对业务执行所需的数据处理的应用程序部分。 它表示执行数据输入、更新、查询和报表处理的例程，尤其是针对在后台发生的处理，而非在屏幕上显示数据所要求的显示逻辑。|  
|业务逻辑处理程序 (business logic handler)|允许在同步过程中运行自定义代码的一种合并复制功能。|  
|业务逻辑处理程序框架 (business logic handler framework)|通过使用业务逻辑处理程序框架，您可以编写合并同步过程中调用的托管代码程序集。|  
|业务规则 (business rules)|用于运行业务的逻辑规则|  
|缓存老化 (cache aging)|确定缓存行何时过期且必须刷新的缓存机制。|  
|缓存客户端 (cache client)|使用 Windows Server AppFabric 客户端 API 进行通信并且将数据存储于 Windows Server AppFabric 分布式缓存系统的一种 .NET 应用程序。|  
|缓存群集 (cache cluster)|分布式缓存服务的实例化，它由协同工作以便存储和分发数据的缓存主机服务的一个或多个实例构成。 数据存储于内存中，以便最大限度地缩短针对数据请求的响应时间。 此群集技术不同于 Windows 群集。|  
|缓存失效 (cache invalidation)|标记缓存中的对象以便该对象将不再由任何缓存客户端使用的过程。 当对象保留在缓存中的时间长于缓存超时值时（此时缓存将到期）发生。|  
|缓存项 (cache item)|存储于缓存中并且具有与该对象关联的附加信息（例如标记和版本）的对象。 可以使用 GetCacheItem 客户端 API 从缓存群集中提取缓存项。|  
|缓存通知 (cache notification)|可由针对缓存群集的多种缓存操作触发的异步通知。 缓存通知可用于调用应用程序方法或自动使本地缓存的对象失效。|  
|缓存操作 (cache operation)|在可触发缓存通知的区域或缓存项上发生的事件。|  
|缓存端口 (cache port)|缓存主机用于将数据传输到缓存客户端和从缓存客户端接收数据的 TCP/IP 端口。 用于缓存端口并且可在各缓存主机上不同的端口号。 这些设置在群集配置设置中维护。|  
|缓存区域 (cache region)|缓存内数据的容器，它将所有缓存对象一起放置于单个缓存主机中。 通过缓存区域，可使用称作标记的说明性字符串搜索该缓存区域中所有缓存的对象。|  
|缓存服务 (cache service)|内存中的分布式缓存解决方案使用户可通过让终端用户更易接触数据而生成高度可伸缩和高响应应用程序。|  
|缓存标记 (cache tag)|可与在某一区域中存储的各缓存对象相关联的一个或多个基于可选字符串的标识符。 区域允许您基于一个或多个标记检索缓存对象。|  
|服务器端编程模式 (cache-side programming pattern)|一种编程模式，在这个模式中，如果数据不在缓存中存在，则应用程序（而非分布式缓存系统）必须将数据重新从原始数据源加载到缓存中。|  
|支持缓存的应用程序 (cache-enabled application)|使用 Windows Server AppFabric 缓存客户端在缓存群集上的缓存中存储数据的一种应用程序。|  
|计算列 (calculated column)|显示数学或逻辑运算或表达式（而非存储的数据）的结果的一种列。|  
|计算字段 (calculated field)|在查询中定义的、显示表达式结果而非显示存储数据的字段。 每次表达式中的值发生变化时，都会重新计算该值。|  
|计算成员 (calculated member)|在运行时使用表达式计算其值的维度成员。 计算成员值可从其他成员的值派生。|  
|计算条件 (calculation condition)|一种多维表达式 (MDX) 逻辑表达式，用来确定是否要对计算子多维数据集中的某个单元应用某个计算公式。|  
|计算公式 (calculation formula)|一种多维表达式 (MDX)，用于为计算子多维数据集中的单元提供值（依据应用的计算条件）。|  
|计算传递 (calculation pass)|多维数据集中的一个计算阶段，在此阶段中将计算适用计算的结果。|  
|计算传递号 (calculation pass number)|用于表示计算传递的序号位置。|  
|计算子多维数据集 (calculation subcube)|用来创建计算单元定义的多维数据集单元集。 该单元集由 MDX 集表达式的组合进行定义。|  
|回调 (callback)|用于对回调网络的用户进行身份验证的过程。 在回调过程中，网络将验证调用方的用户名和密码，挂起然后返回调用，通常是返回到预先授权的号码。 此过程将禁止对帐户的未授权访问，即使个体的登录 ID 和密码已被盗。|  
|调用级别接口 (call-level interface)|ODBC 为供应用程序使用支持的接口。|  
|候选键 (candidate key)|对于表中的每一行，具有唯一值的一列或一组列。|  
|端帽 (cap)|表示包含未连接端（例如线条、笔画的末端）的路径。 您可以通过应用四个端帽样式之一，更改每个笔画末端的外形：平端帽、圆端帽、方形端帽和三角形端帽。|  
|基数|可在关系的每一方存在的实体的数目。|  
|传送视图 (carousel view)|在 PowerPivot 库中，预览区域居中并且紧接在当前缩略图之前和之后的缩略图与预览区域相邻的一种专门的视图。|  
|级联删除 (cascading delete)|对于在表之间强制引用完整性的关系，在删除主表中的记录时对相关表中的所有相关记录进行的一种删除。|  
|级联更新 (cascading update)|对于在表之间强制引用完整性的关系，在更改主表中的记录时对相关表中的所有相关记录进行的一种更新。|  
|case|一种抽象数据视图，以属性和与其他事例的关系为特征。|  
|事例键 (case key)|指事例的元素，通过该元素在事例集内引用该事例。|  
|目录视图|构成 SQL Server 系统目录的内置视图。|  
|灾难性错误 (catastrophic error)|导致系统或程序突然失败并且没有希望恢复的一种错误。 灾难性错误的一个例子是无法处理的未捕获的异常。|  
|CD 封套 (CD sleeve)|用于装 CD 的套子。|  
|CD-ROM|一种存储介质，其特点是高容量（大约 650 MB）并且使用激光而非磁性方式来读取数据。|  
|单元|多维数据集中包含值的属性集，由从每个维度选择一个成员时的交集指定。|  
|单元集 (cellset)|ADO MD 中的一个对象，包含通过多维查询从多维数据集或其他单元集中选择的单元的集合。|  
|集中注册模型 (centralized registration model)|从管理策略中删除所有证书订阅方参与的注册模型。 对于工作流，指定为发起方的用户将发起请求并且注册代理将执行该请求。|  
|CEP|基于声明的查询和模式规范从多个源连续增量处理事件流，滞后时间几乎为零。|  
|CEP 引擎 (CEP engine)|Microsoft StreamInsight 的核心引擎和适配器框架组件。 StreamInsight 服务器可用于处理和分析与复杂事件处理应用程序关联的事件流。|  
|CERN|位于瑞士日内瓦的一个物理研究中心，在这里在 Tim Berners-Lee 的领导下于 1989 年进行万维网的原始开发，从而促进科学界各成员的交流。|  
|证书 (certificate)|通常用于身份验证以及帮助保护网络上信息的数字文档。 证书将公钥绑定到持有对应私钥的实体。 证书由颁发这些证书的证书颁发机构进行数字签名，可以针对用户、计算机或服务颁发证书。|  
|证书注册 (certificate enrollment)|请求、接收和安装证书的过程。|  
|证书颁发者 (certificate issuer)|向有关对象颁发证书的证书授权机构。|  
|Certificate Lifecycle Manager 客户端 (Certificate Lifecycle Manager Client)|协助最终用户管理其智能卡的一套 Certificate Lifecycle Manager (CLM) 客户端工具。 这些工具包括 Smart Card Self Service Control、Smart Card Personalization Control 和 Certificate Profile Update Control。 请参见 Smart Card Self-Service Control、Smart Card Personalization Control、Certificate Profile Update Control。|  
|证书管理员 (certificate manager)|具有适当的 CLM 权限以便管理其他 CLM 用户或管理 CLM 应用程序本身的 Certificate Lifecycle Manager (CLM) 用户。|  
|证书管理员 Web 门户 (certificate manager Web portal)|在 Certificate Lifecycle Manager (CLM) 服务器上运行的一种 Web 应用程序。 此门户允许证书管理员管理其他用户的证书和智能卡。 证书订阅方和证书管理员 Web 门户全都通过相同的通用资源指示符 (URL) 进行访问；但是，显示的内容基于用户的角色和权限。|  
|Certificate Profile Update Control|一种 ActiveX 控件，该控件可自动进行客户端计算机上 Certificate Lifecycle Manager (CLM) 配置文件的更新。|  
|证书吊销 (certificate revocation)|吊销数字证书的过程。|  
|证书订阅方 (certificate subscriber)|需要证书（可具有智能卡，也可以不具有智能卡）的用户。 证书订阅者可以访问仅可为用户自己的证书执行的少量功能。|  
|证书订阅方 Web 门户 (certificate subscriber Web portal)|在 Certificate Lifecycle Manager (CLM) 服务器上运行的一种 Web 应用程序。 此 CLM 服务器组件在自助服务模式下直接与用户交互。 该特定功能基于 Active Directory 组成员身份和权限。 证书订阅方和证书管理员 Web 门户全都通过相同的通用资源指示符 (URL) 进行访问；但是，显示的内容基于用户的角色和权限。|  
|证书模板 (certificate template)|基于其用途指定证书的格式和内容的一种 Windows 结构。 在从 Windows 企业证书颁发机构 (CA) 请求证书时，证书请求方可以从基于证书模板的多种证书类型中进行选择。|  
|更改应用方 (change applier)|为成批的更改执行冲突检测、冲突处理和更改应用的对象。|  
|更改传播 (change propagation)|将来自一个副本的更改应用于另一个副本的过程。|  
|更改脚本 (change script)|一种文本文件，包含编辑会话期间对数据库进行的所有更改所对应的 SQL 语句（按照更改发生的顺序）。|  
|更改单元 (change unit)|在存储区中更改跟踪的最小单元。 在更改传播中，仅必须发送更改的单元；而在冲突检测中，对相同单元的独立更改将被视为冲突。|  
|变化的维度 (changing dimension)|一种具有灵活的成员结构的维度，用来支持对结构和数据的频繁更改。|  
|字符编码 (character encoding)|一组字符和一组数字之间的一对一映射。|  
|字符集 (character set)|具有某种共同关系的一组字母、数字和其他字符。 例如，标准 ASCII 字符集包括构成 ASCII 编码方案的字母、数字、符号和控制代码。|  
|图表数据区域 (chart data region)|报表布局中以图形格式显示数据的报表项。|  
|checkpoint|数据库引擎将脏缓冲区页写入磁盘的事件。 每个检查点将在上个检查点是脏的且尚未写入磁盘的所有页写入磁盘。|  
|校验和 (checksum)|用于测试数据中是否存在可能会在传输数据或者将数据写入磁盘时发生的错误的计算值。 通过按顺序将数据的所有字节与一系列算术或逻辑运算组合在一起，为给定数据块区计算校验和。 在传输或存储数据后，使用已传输或存储的数据（可能错误）以相同的方式计算新的校验和。 如果这两个校验和不匹配，将发生错误，并且应该再次传输或存储数据。 校验和无法检测出所有错误，并且不能用于纠正有错误的数据。|  
|子级|在树结构中，某一节点与其上一级之间的关系。|  
|历史记录 (chronicle)|存储单个应用程序的状态信息的表。 例如事件历史记录，此类历史记录可以存储用于计划的订阅的事件数据。|  
|块区 (chunk)|指定量的数据。|  
|CIDER Shell|一种具有选项卡式界面的 UI 容器，用于承载 TSQLEditor 组件和来自 TSQL 查询执行的相关输出。|  
|声明标识 (claims identity)|表示特定的用户、应用程序、计算机或其他实体的唯一标识符；通过此类标识，无需多次输入凭据，即可访问多个资源，例如应用程序和网络资源。 它还使资源能够验证来自实体的请求。|  
|无错关闭 (clean shutdown)|一种没有错误的系统关闭。|  
|明文 (clear text)|未加密或已解密形式的数据。|  
|明文 (cleartext)|未加密或已解密形式的数据。|  
|CLI|ODBC 为供应用程序使用支持的接口。|  
|点击流分析 (clickstream analysis)|点击流数据是用户在各页之间切换并且在某一网站内单击项时生成的信息，通常存储于日志文件中。 网站设计人员可以使用点击流数据改进用户的站点体验。|  
|点击链接型报表 (clickthrough report)|当点击呈现的报表生成器报表中的数据时显示相关报表模型数据的报表。|  
|客户端|要集成到 Microsoft Sync Framework 体系结构的服务、应用程序或设备。|  
|客户端|连接到或请求其他计算机或程序的一种计算机或程序。|  
|客户端代码生成 (client code generation)|基于在中间层公开的操作和实体为客户端项目生成代码的操作。 RIA 服务链接必须在客户端和服务器项目之间存在。|  
|客户端游标 (client cursor)|在客户端实现的游标。 整个结果集首先传输到客户端，接着客户端 API 软件从这一缓存的结果集实现游标功能。|  
|客户端统计信息窗格 (Client Statistics pane)|承载客户端统计信息输出的选项卡之一。|  
|客户端订阅 (client subscription)|合并发布的一种订阅，使用发布服务器的优先级值来检测冲突和解决冲突。|  
|客户端类型 (client type)|确定缓存客户端的工作方式以及对您的应用程序性能的影响的信息。 有两种客户端类型：简单客户端类型和路由客户端类型。|  
|CLM 审核 (CLM Audit)|Active Directory 中的一种 Certificate Lifecycle Manager (CLM) 扩展权限，它允许生成和显示 CLM 策略模板、在配置文件模板内定义管理策略以及生成 CLM 报告。|  
|CLM 凭据 (CLM credentials)|可用于向 Certificate Lifecycle Manager (CLM) 验证用户身份的用户帐户信息。 这些凭据可以采用域凭据或一次性密码的形式。|  
|CLM 注册 (CLM Enroll)|Active Directory 中的一种 Certificate Lifecycle Manager (CLM) 扩展权限，它允许用户指定在使用模板颁发证书时收集的工作流和数据。 此扩展权限仅适用于配置文件模板。|  
|CLM 注册代理 (CLM Enrollment Agent)|Active Directory 中的一种 Certificate Lifecycle Manager (CLM) 扩展权限，它允许用户或组代表其他用户执行证书请求。 颁发的证书的主题将包含目标用户的名称，而不是请求者的名称。|  
|CLM 恢复 (CLM Recover)|Active Directory 中的一种 Certificate Lifecycle Manager (CLM) 扩展权限，它允许从证书颁发机构数据库启动加密密钥恢复。|  
|CLM 续订 (CLM Renew)|Active Directory 中的一种 Certificate Lifecycle Manager (CLM) 扩展权限，它允许启动、运行或完成注册请求。 续订请求将使用具有新有效期的新证书替换其到期日期附近的用户证书。|  
|CLM 报告 (CLM reports)|与 Certificate Lifecycle Manager (CLM) 内的凭据管理活动相关的审核信息。|  
|CLM 请求注册 (CLM Request Enroll)|Active Directory 中的一种 Certificate Lifecycle Manager (CLM) 扩展权限，它允许启动、运行或完成注册请求。|  
|CLM 请求恢复 (CLM Request Recover)|Active Directory 中的一种 Certificate Lifecycle Manager (CLM) 扩展权限，它允许从证书颁发机构数据库启动加密密钥恢复。|  
|CLM 请求续订 (CLM Request Renew)|Active Directory 中的一种 Certificate Lifecycle Manager (CLM) 扩展权限，它允许启动、运行或完成注册请求。 续订请求将使用具有新有效期的新证书替换其到期日期附近的用户证书。|  
|CLM 请求撤消 (CLM Request Revoke)|Active Directory 中的证书生命周期管理器（CLM）扩展权限，它允许在证书有效期到期之前吊销证书。 例如，如果用户的计算机或智能卡已泄露（被盗），则这是必需的。|  
|CLM 请求取消阻止智能卡 (CLM Request Unblock Smart Card)|Active Directory 中的证书生命周期管理器（CLM）扩展权限，它允许重置智能卡的用户个人标识号（PIN），允许访问智能卡上的密钥材料以及重新建立该材料。|  
|CLM 撤消 (CLM Revoke)|Active Directory 中的证书生命周期管理器（CLM）扩展权限，它允许在证书有效期到期之前吊销证书。 例如，如果用户的计算机或智能卡已泄露（被盗），则这是必需的。|  
|时钟向量 (clock vector)|表示对副本的更新的时钟向量元素的集合。 在 0 和时钟周期数之间发生的任何更改都将包含在该向量中。|  
|时钟向量元素 (clock vector element)|表示对副本的更改的由副本密钥和时钟周期数构成的一对值。|  
|CLR 函数 (CLR function)|通过引用 SQL Server 程序集创建的函数，其实现在 .NET Framework 公共语言运行时 (CLR) 中创建的程序集中定义。|  
|CLR 存储过程|通过引用 SQL Server 程序集而创建的存储过程，其实现在 .NET Framework 公共语言运行时 (CLR) 中创建的程序集中定义。|  
|CLR 触发器 (CLR trigger)|通过引用 SQL Server 程序集创建的触发器，其实现在 .NET Framework 公共语言运行时 (CLR) 中创建的程序集中定义。|  
|CLR 用户定义类型 (CLR user-defined type)|通过引用 SQL Server 程序集创建的用户定义数据类型，其实现在 .NET Framework 公共语言运行时 (CLR) 中创建的程序集中定义。|  
|群集配置存储位置 (cluster configuration storage location)|持有群集配置信息的共享位置（或共享存储位置）。 它可以是共享文件或数据库。|  
|群集磁盘资源 (cluster disk resource)|群集存储设备上的磁盘。|  
|群集节点 (cluster node)|服务器群集中的单独计算机。|  
|群集端口 (cluster port)|缓存主机用于管理缓存群集的 TCP/IP 端口。 用于群集端口的端口号在各缓存主机上可以不同。 这些设置在群集配置设置中维护。|  
|群集修复 (cluster repair)|一种修复操作，在此操作中，所有丢失或损坏的文件都将被替换，所有丢失或损坏的注册表项都将被替换，并且所有丢失或无效的配置值都将设置为默认值。|  
|聚集索引|一种通过键值的逻辑顺序来确定表中相应行的物理顺序的基于 B 树的索引。|  
|群集服务器 (clustered server)|属于服务器群集的服务器。|  
|聚类分析|一种对数据进行分析并根据记录在多维属性空间中的位置对它们进行分组的数据挖掘方法。|  
|粗粒度锁 (coarse-grained lock)|适用于大量代码或数据的锁。|  
|代码访问安全性 (code access security)|由公共语言运行时提供的一种机制。通过此机制，托管代码由安全策略授予权限并且这些权限是强制应用的，以帮助限制允许代码执行的操作。|  
|代码元素 (code element)|能够代表要处理或交换的编码文本单位的最小位组合。|  
|代码页 (code page)|将程序使用的字符代码（码位值）与键盘上的键或显示上的字符相关的一种表。 这提供对不同国家或地区的字符集和键盘布局的支持。|  
|码位 (code point)|能够代表要处理或交换的编码文本单位的最小位组合。|  
|冷延迟 (cold latency)|首次使用工作流并且 XOML 或 XAML 需要编译时所用的时间。|  
|冷备用 (cold standby)|在几小时或几天中提供可用性的第二个数据中心。|  
|collation|确定如何比较、排序和显示数据的一组规则。|  
|collection|包含一组相关对象的对象。 在集合中发生更改时某一对象在集合中的位置可更改；因此，任何特定对象在集合中的位置都可能变化。|  
|收集项 (collection item)|一种收集器类型的实例，它使用一组特定的输入属性和收集频率创建，并且用于收集特定类型的数据。|  
|收集模式 (collection mode)|收集数据并将其上载到管理数据仓库的频率。|  
|收集组 (collection set)|用户可通过用户界面与之交互的一组收集项。|  
|收集器类型 (collector type)|SQL Server Integration Services 包的逻辑包装，该包提供收集数据和将数据上载到管理数据仓库的实际机制。|  
|并置 (collocate)|选择包含相关数据的已分区表并且与分区列上的此表相联接。|  
|归置 (collocation)|根据等效的分区函数对已分区的表和索引进行分区的一种情况。|  
|色阶 (color range)|可用于显示设备的颜色范围。|  
|颜色规则 (color rule)|应用于多边形、线条和表示点或多边形中心点的标记的填充颜色的一种规则。|  
|色阶 (color scale)|仅显示颜色规则的结果一种标准。|  
|柱形图|数据库表的每一行中的区域，它为该表建模的对象的某个属性存储数据值。|  
|列绑定 (column binding)|Analysis Services 对象与数据源视图中列的绑定。|  
|列分隔符 (column delimiter)|在要导入/导出的 CSV 文件中用来分隔列的字符。|  
|列筛选器 (column filter)|限制要包含在快照发布、事务发布或合并发布中的列的筛选器。|  
|列模式配置文件|一种报表，它包含涵盖字符串列中指定百分比的值的一组正则表达式。|  
|列集 (column set)|一种泛型 XML 表示形式，它将表的所有稀疏列组合成为一种结构化的输出。|  
|列级排序规则 (column-level collation)|支持在单个实例中使用多种排序规则。|  
|列级约束 (column-level constraint)|创建或更改表时在列定义内指定的约束定义。|  
|列网格 (Columns Grid)|表设计器中的一种可编辑网格结构，列出表的各列以及与每一列有关的其他信息。|  
|列存储索引|在一组单独的磁盘页中存储每一列，而非每页存储多行。|  
|COM|一种基于对象的编程模型，用于提高软件的互操作性；它使两个或多个应用程序或组件可以轻松地进行合作，即使它们是由不同的供应商、在不同的时间、用不同的语言编写的，或者正在运行不同操作系统的不同计算机上运行，也不例外。|  
|命令缓冲区 (command buffer)|内存中用于保存用户输入的命令的区域。 通过命令缓冲区，用户无需重新键入整个命令就重复命令、编辑过去的命令以便更改某些参数或纠正错误、撤消命令或获取过去的命令的列表。|  
|命令提示符|操作系统和用户之间的一个接口，在其中，用户键入传递到命令解释器以便执行的文本的命令语言字符串。|  
|命令关系 (command relationship)|基于自然语言问题或命令向硬件提供指令。|  
|提交 (commit)|一种保存自启动事务以来对数据库、多维数据集或维度进行的所有更改的操作。|  
|提交预览 (Commit Preview)|显示在提交操作过程中要执行的操作的窗口的标题。|  
|提交|已记入日志并且无法回滚的事务的一种特性。|  
|顺势指标公式 (commodity channel index formula)|一种公式，该公式根据移动平均线计算商品的日平均价格的平均偏差。 大于 100 的值指示商品处于超买状态，低于 100 的值指示商品处于超卖状态。|  
|比较器 (comparator)|比较两项以确定它们是否相等的设备。 例如，在电子行业中，比较器是比较两个输入电压并指出其中较高电压的电路。|  
|编译错误 (compilation error)|在编译应用程序时发生的错误。 这些编译错误通常是由于错误输入了语法而发生。|  
|编译时间 (compile time)|执行程序编译所需的时间长度。 编译时间的范围可以是几秒钟，也可以是许多小时，具体长短依赖于程序的大小和复杂程度、编译器的速度以及硬件性能。|  
|数据库完整还原 (complete database restore)|对数据库完整备份以及自数据库完整备份以来所做的最近数据库差异备份（如果存在）和日志备份（如果存在）的还原。|  
|复杂事件处理 (complex event processing)|基于声明的查询和模式规范从多个源连续增量处理事件流，滞后时间几乎为零。|  
|组件对象模型 (Component Object Model)|一种基于对象的编程模型，用于提高软件的互操作性；它使两个或多个应用程序或组件可以轻松地进行合作，即使它们是由不同的供应商、在不同的时间、用不同的语言编写的，或者正在运行不同操作系统的不同计算机上运行，也不例外。|  
|可组合 (composable)|与通过使用查询组件（对象或运算符）将复杂查询构成为可重复使用的构造块的能力相关。 这是通过将查询组件链接在一起或通过相互封装查询组件来完成的。|  
|组合环境 (composed environment)|从虚拟机创建的虚拟环境。 这些虚拟机是在 Microsoft 测试管理器的外部创建的并且已部署在主机组上。|  
|组合索引 (composite index)|一种使用表中多列对数据创建索引的索引。|  
|组合键 (composite key)|其定义由文件中的两个或以上的字段、表中的多列或关系中的多个属性构成的键。|  
|复合层次结构 (compositional hierarchy)|在概念上属于某一层次结构的一组实体，例如父实体和子实体。 数据操作要求这些实体将被视作单个单元。|  
|计算列 (computed column)|表中的虚拟列，其值在运行时计算得到。|  
|计算字段 (computed field)|使用 Transact-SQL 表达式计算得到的格式化通知中的值。|  
|COM 结构的存储文件 (COM-structured storage file)|由 Data Transformation Services (DTS) 用于存储已保存 DTS 包的版本历史记录的组件对象模型 (COM) 复合文件。|  
|串联 (concatenation)|将两个或更多个字符串或表达式组合成一个字符串或表达式，或者将两个或更多个二进制字符串或表达式组合成一个二进制字符串或表达式的过程。|  
|concurrency|使多个用户能够同时访问和更改共享数据的进程。 实体框架实现开放式并发模型。|  
|并发冲突 (concurrency conflict)|当同一项或变更单位在以后将进行同步的两个不同副本上发生变更时发生的冲突。|  
|并发模型 (concurrency model)|应用程序可设计为负责使用相同缓存数据的并发操作的一种方式。 Windows Server AppFabric 支持乐观和悲观并发模型。|  
|并发操作 (concurrent operation)|一种计算机操作，在此操作中，两个或以上的进程（程序）有权访问微处理器的时间，并因此接近于同时执行。 因为微处理器可以使用比人们所能觉察出的小得多的时间单位，所以并发进程好像是同时发生，但实际上并非这样。|  
|条件表达式 (conditional expression)|生成布尔值（true 或 false）的表达式。 此类表达式可以涉及比较（测试值是否相等，或对于非布尔值， \< [less than] or > [大于] 关系）和逻辑组合（使用布尔运算符，如 and、or 和 XOR）的布尔表达式。|  
|有条件拆分 (conditional split)|对数据库完整备份以及自数据库完整备份以来所做的最近数据库差异备份（如果存在）和日志备份（如果存在）的还原。|  
|配置文件 (config file)|一个文件，其中包含可由计算机读取的软硬件操作规范，或包含有关另一个文件或特定用户的信息，例如用户的登录 ID。|  
|配置|对于一台微机，是指系统的所有内外部组件，包括内存、磁盘驱动器、键盘、显卡和一般不太重要的附加硬件，如鼠标、调制解调器或打印机。 软件（操作系统和各种设备驱动程序）、用户通过配置文件（例如 IBM PC 和兼容机上的 AUTOEXEC.BAT 和 CONFIG.SYS 文件）进行的选择并且有时候是硬件（开关和跳线）都需要“对配置进行配置”才能正常工作。 尽管可以通过添加更多内存或磁盘容量等更改系统配置，但系统的基本结构（其体系结构）保持不变。|  
|配置文件|一个文件，其中包含可由计算机读取的软硬件操作规范，或包含有关另一个文件或特定用户的信息，例如用户的登录 ID。|  
|配置工具|在 SQL Server 中，表示允许用户启用、禁用、启动或停止 SQL Server 安装的功能、服务和远程连接的菜单项。|  
|冲突检测|在不知道另一副本的情况下确定一个副本执行了哪些运算的过程，例如两个副本对同一项进行本地更新时。|  
|冲突解决方法 (conflict resolution method)|用于确定在发生冲突时将哪个变更写入存储区的方法。 一般冲突解决方法如下：后写入者胜出、源胜出、目标胜出、自定义解决方法或延迟解决方法。 对于自定义解决方法，解决应用程序读取冲突日志中的冲突并选择一种解决方法。 对于延迟解决方法，记录冲突时同时记录发生冲突的变更数据以及变更的生成知识。|  
|冲突解决程序 (conflict resolver)|用于解决冲突情况的特殊机制。|  
|连接控制器|一种连接技术，其中，基于不同数据访问技术的应用程序（.NET 或本机 Win32）可以共享相同的连接信息。 可为此类客户端应用程序集中管理连接信息。|  
|连接管理器|与数据源所进行的运行时连接的逻辑表示形式。|  
|连接字符串 (connection string)|一系列定义资源位置以及与资源进行连接的方式的参数。|  
|一致性单位 (consistency unit)|数据同步的最小单位。 由于一起发送具有相同一致性单位的所有变更，因此在仅应用一致性单位的一部分时将不中断同步。|  
|constant|不是计算得出并因此不会发生更改的数值或字符串值。|  
|约束冲突 (constraint conflict)|违反有关项或变更单位的约束（如文件夹的关系或文件系统中同名数据的位置）的冲突。|  
|约束违反 (constraint violation)|在未满足限制条件时发生的冲突。|  
|包含的数据库|一种 SQL Server 数据库，它包含定义和访问数据库所需的所有用户身份验证、数据库设置和元数据，并且对安装了数据库的 SQL Server 数据库引擎实例没有配置依赖关系。|  
|容器 (container)|提供包结构的一种控制流元素。|  
|内容格式化程序 (content formatter)|分发服务器上用于将原始通知数据转换为可读消息的部分。|  
|内容密钥 (content key)|在发布和使用期间，用于同时对受保护的内容进行加密和解密的密钥。|  
|争用 (contention)|在网络上，争用某一通信线路或网络资源的情况。|  
|上下文窗格 (Context pane)|表设计器中的一种树视图，列出与某个表相关的对象。|  
|上下文切换 (context switch)|更改检查执行语句或执行操作的权限时所依据的标识。|  
|延续介质 (continuation media)|在初始介质已满后使用的允许备份操作继续进行的可移动备份介质系列。|  
|延续磁带 (continuation tape)|介质簇中第一个磁带用完之后，为了保持介质簇的连续性而使用的磁带。|  
|contract|一个 Service Broker 对象，用于定义可在给定会话中交换的消息类型。|  
|控制流|执行任务的一组连接的控制流元素。|  
|控制中断报表 (control-break report)|一种报表，用于汇总用户定义的组或分行中的数据。 遇到不同的数据时，将触发一个新组。|  
|控制流语言|控制触发器、存储过程和批处理中的 SQL 语句和语句块的执行流的 Transact-SQL 关键字。|  
|会话端点 (conversation endpoint)|代表会话参与方的对象。|  
|会话组 (conversation group)|一组相关的 Service Broker 会话。 同一会话组中的消息一次只能由一个服务程序进行处理。|  
|会话句柄 (conversation handle)|用来唯一定义一个会话的句柄。|  
|凸包 (convex hull)|在欧几里得平面或欧几里得空间中包含 X 的最小凸点集合。|  
|坐标系统 (coordinate system)|在 n 维空间中，定位到某一点（称为原点）的一组 n 个线性独立的向量。 一组坐标指定空间中的某一点（或者距原点的向量），其方法是指示沿每个向量到达该点（或者向量尖端）的距离。|  
|相关子查询 (correlated subquery)|引用外部语句中列的子查询。 将对外部语句中的每个候选行运行内部查询。|  
|计数窗口 (count window)|具有可变窗口大小的一种窗口，它针对每个不同的事件开始时间沿着时间线移动。|  
|副署 (countersign)|签署已由其他方签署的文档。|  
|CPU 忙 (CPU busy)|一种 SQL Server 统计信息，报告中央处理器 (CPU) 在 SQL Server 工作上花费的时间（毫秒）。|  
|爬网 (crawl)|跨内容编译和维护某一索引的过程。|  
|凭据|包含标识以及用于获取访问本地和网络资源的身份证明的信息。 凭据的示例包括用户名和密码、智能卡与证书。|  
|跨数据库所有权链|跨多个数据库的所有权链接。|  
|交叉验证|用于评估数据挖掘模型的精确性的方法。|  
|CTI 事件 (CTI event)|一种特殊的标点事件，用来指示现有事件的完整性。|  
|多维数据集|一个经过组织和汇总，形成由一组维度和度量值定义的多维结构的数据集。|  
|多维数据集角色 (cube role)|对多维数据集具有相同访问权限的用户和组的集合。 在您向某一多维数据集分配数据库角色时将创建多维数据集角色，并且该角色将仅应用于该多维数据集。|  
|当前时间增量事件 (current time increment event)|一种特殊的标点事件，用来指示现有事件的完整性。|  
|cursor|映射到一个结果集并在该结果集内的一行中确立位置的实体。|  
|游标降级 (cursor degradation)|返回一种不同于用户所声明的游标类型的游标。|  
|游标库 (cursor library)|ODBC 和应用程序编程接口 (API) 的一部分，用于实现客户端游标。|  
|自定义汇总 (custom rollup)|为某一维度级别或成员自定义的聚合计算，它将替代多维数据集的度量值的聚合函数。|  
|自定义规则 (custom rule)|角色中的一种规范，限制该角色中的用户有权访问的维度成员或多维数据集单元。|  
|自定义变量 (custom variable)|包开发人员提供的变量。|  
|自定义卷 (custom volume)|一种卷，此类卷不位于 DPM 存储池中，并且指定为对保护组成员存储副本和恢复点。|  
|循环保护 (cyclic protection)|一种保护类型，它由两个 DPM 服务器提供保护，其中的每个服务器都保护另一个服务器上的数据。|  
|DAC|一种应用程序，它捕获客户端-服务器或 3 层应用程序使用的 SQL Server 数据库和实例对象。|  
|DAC 实例 (DAC instance)|在数据库引擎的某一实例上部署的 DAC 的副本。 在数据库引擎的同一实例上可以有多个 DAC 实例。|  
|DAC 包|一种包含为 DAC 定义的所有对象的 XML 清单；在开发人员生成 DAC 项目时将创建该包。|  
|DAC 包文件 (DAC package file)|作为 DAC 包的容器的 XML 文件。|  
|DAC 位置策略 (DAC placement policy)|由一组条件构成的 PBM 策略，这些条件作为针对可部署 DAC 的 SQL Server 的目标实例的先决条件。|  
|DAC 项目 (DAC project)|数据库开发人员用于创建和开发 DAC 的 Visual Studio 项目。 在 Visual Studio 和 VSTS 源代码控制、版本控制和开发项目管理中完全支持 DAC 项目。|  
|数据适配器 (data adapter)|用于将数据提交到数据库、Web 服务和可扩展标记语言 (XML) 文件以及从其检索数据的一种对象。|  
|数据备份 (data backup)|包含一个或多个数据文件的完整映像的任意备份。|  
|数据装箱 (data binning)|根据定义的条件将数据分组到特定的 bin 或组中的过程。|  
|数据块 (data block)|在 text、ntext 和 image 数据中，数据块指在应用程序与 SQL Server 实例之间一次传输的数据单元。 此术语还可用于表示这些数据类型的存储单元。|  
|数据共存 (data co-location)|DPM 中的一项功能，可用于在单个卷或同一个磁带上保护多个数据源。 这使得您可以在每个卷或磁带上存储更多数据。|  
|数据连接 (data connection)|指定与数据库文件或服务器有关的名称、类型、位置和其他信息（可选）的一种连接。|  
|数据控制语言 (Data Control Language)|SQL 语句的子集，用来控制对数据库对象的权限。|  
|数据收敛 (data convergence)|发布服务器和订阅服务器上匹配的数据。|  
|数据损坏 (data corruption)|内存或磁盘中的数据被无意中更改以致其意义因此被改变或毁坏的一个过程。|  
|数据定义 (data definition)|数据库中的特性、属性和对象。|  
|数据定义语言 (data definition language)|定义数据库的所有特性和属性（特别是记录布局、字段定义、键字段、文件位置和存储策略）的一种语言。|  
|数据描述语言 (data description language)|定义数据库的所有特性和属性（特别是记录布局、字段定义、键字段、文件位置和存储策略）的一种语言。|  
|数据字典 (data dictionary)|包含与某一数据库系统中的所有数据库有关的数据的数据库。 数据字典存储所有不同的架构和文件规范及其位置。 数据字典还包含与哪些程序使用哪些数据以及哪些用户对哪些报表感兴趣有关的信息。|  
|数据元素 (data element)|数据的单个单元。|  
|数据爆炸 (data explosion)|由于存储聚合数据而引起多维结构（例如多维数据集）的大小呈指数级增长。|  
|数据扩展插件 (data extension)|处理特定类型的数据源的数据的一种插件。 例如 Microsoft OLE DB Provider for DB2。|  
|数据馈送|采用 Atom 1.0 格式的一种 XML 数据流。|  
|数据流|数据通过一组连接的元素（提取、转换和加载数据）进行的移动。|  
|数据流组件 (data flow component)|操作数据的 SQL Server 2005 Integration Services 的组件。|  
|数据流引擎 (data flow engine)|在包中执行数据流的引擎。|  
|数据流任务 (data flow task)|封装在源和目标之间移动数据的数据流引擎并且提供在移动数据的同时转换、清除和修改数据的功能的任务。|  
|数据完整性 (data integrity)|数据的精确性并且其符合其预期值，特别是在传输或处理后。|  
|数据操作语言 (data manipulation language)|用于检索和操作数据的 SQL 语句的子集。 DML 语句通常以 SELECT INSERT UPDATE 或 DELETE 开头。|  
|数据市场 (data mart)|数据仓库内容的子集，往往包含针对部门级别或针对特定业务领域的数据。|  
|数据成员 (data member)|在父子层次结构中与父成员关联的子成员。 数据成员包含其父成员的数据值，而不是该父成员的子级的聚合值。|  
|数据挖掘|通过使用高级统计工具在数据库或其他计算机存储库中标识商业上有用的模式或关系的过程。|  
|数据挖掘扩展插件 (data mining extension)|在 Analysis Services 中，指的是以编程方式执行数据挖掘任务的语句。|  
|数据挖掘模型定型 (data mining model training)|数据挖掘模型用于通过计算一组已知和可预测的数据来估计模型参数的过程。|  
|数据处理扩展插件 (data processing extension)|处理特定类型的数据源的数据的一种插件（类似于数据库驱动程序）。|  
|数据处理器组件 (Data Processor component)|处理数据的报表服务器引擎的组件。|  
|数据配置文件查看器 (Data Profile Viewer)|一种独立的实用工具，可以通过可选的深化功能以摘要的格式和以详细信息的格式显示配置文件输出。|  
|数据访问接口|特定于某个目标类型的已知数据源，用于为收集器类型提供数据。|  
|数据抽取 (data pump)|在 SQL Server 2000 Transformation Services (DTS) 中使用的一种组件，用于在异类数据存储区之间导入、导出和转换数据。|  
|数据区域 (data region)|一种报表项，用于为来自基础数据集的迭代数据提供数据操作和显示功能。|  
|数据清理 (data scrubbing)|根据来自多个联机事务处理 (OLTP) 系统的数据生成数据仓库的过程。|  
|数据段 (data segment)|包含程序所使用的数据的内存或辅助存储区部分。|  
|数据集 (data set)|相关信息的集合，由可在数据处理中视作单元的单独元素构成。|  
|数据源视图 (data source view)|一个命名的数据库对象（例如基于一个或多个数据源的表、视图、关系和存储过程）选集，用来定义 Analysis Services 数据库中的 OLAP 和数据挖掘对象所引用的架构。 它还可用于为 DTS 任务、转换和数据适配器定义源、目标和查找表。|  
|数据管理人员 (data steward)|负责在元数据注册表中维护数据元素的人士。|  
|数据分流 (data tap)|从 SQL Server Integration Services 中的指定路径收集数据。 在 SSIS 包执行时分流的数据可写入 CSV 文件，并且客户可以指定要分流的数据流。|  
|数据查看器 (data viewer)|一种图形工具，用于数据在运行时在两个数据流组件之间移动时显示数据。|  
|数据仓库|长时间存储操作数据的数据库。 然后，这些数据由 Operations Manager 报表服务器用来生成报表。 默认情况下，此数据库的名称为 OperationsManagerDW。|  
|数据仓库|长时间存储操作数据的数据库。 然后，这些数据由 Operations Manager 报表服务器用来生成报表。 默认情况下，此数据库的名称为 OperationsManagerDW。|  
|数据库管理员 (database administrator)|管理数据库的人士。 数据库管理员确定数据库的内容、内部结构和访问策略，定义安全性和完整性，并且监视性能。|  
|数据库目录 (database catalog)|数据库的一部分，包含数据库中所有对象的定义以及该数据库的定义。|  
|数据库关系图 (database diagram)|数据库架构的任何部分的图形表示形式。 它可以是整个数据库结构，也可以是其中的一部分。 该关系图包括表、表中所包含的列以及表之间的关系。|  
|数据库引擎|可访问数据库管理系统 (DBMS) 的一个或多个程序模块。|  
|Database Engine Tuning Advisor|一种用于优化物理数据库设计的工具，可帮助用户选择和创建一组最佳的索引、索引视图和分区。|  
|数据库资源管理器 (Database Explorer)|一种简单的数据库管理工具，使用户能够执行各种数据库操作，例如创建新表、查询和修改现有表以及其他数据库开发功能。|  
|数据库文件 (database file)|构成数据库的物理文件之一。|  
|数据库语言 (database language)|用于访问、查询、更新和管理关系数据库系统中的数据的语言。|  
|数据库管理系统 (database management system)|物理数据库和用户之间的软件层。 该 DBMS 管理对数据库的所有访问。|  
|数据库管理器 (database manager)|物理数据库和用户之间的软件层。 该 DBMS 管理对数据库的所有访问。|  
|数据库镜像|将对读写数据库（主体数据库）所做的每次更新立即重新生成到驻留在单独的数据库引擎实例（镜像服务器）中的该数据库的只读镜像（镜像数据库）中。 在生产环境中，该镜像服务器位于其他的计算机上。 通过还原（但不恢复）主体数据库的完整备份可创建镜像数据库。|  
|数据库镜像监视器|用于监视某一服务器实例上镜像数据库的任何子集的工具。|  
|数据库镜像伙伴 (database mirroring partner)|一对用作镜像数据库的角色切换伙伴的服务器实例中的一个。|  
|数据库镜像伙伴 (database mirroring partners)|一对用作镜像数据库的角色切换伙伴的服务器实例。|  
|数据库项目 (database project)|一个或多个数据连接（数据库与访问该数据库所需的信息）的集合。|  
|数据库引用 (database reference)|解析为数据库的路径、表达式或文件名。|  
|数据库角色|对 Analysis Services 数据库具有相同访问权限的用户和组的集合。|  
|数据库架构 (database schema)|数据库的表、字段、数据类型以及主键和外键的名称。|  
|数据库脚本 (database script)|用于创建数据库对象的语句的集合。|  
|database snapshot|快照创建那一刻的数据库的只读、静态视图。|  
|数据库结构 (database structure)|数据库的表、字段、数据类型以及主键和外键的名称。|  
|数据库视图|视图创建那一刻的源数据库的只读、静态快照。|  
|数据定义查询 (data-definition query)|包含数据定义语言 (DDL) 语句的 SQL 特定的查询。 这些语句可用于创建或更改数据库中的对象。|  
|数据驱动订阅 (data-driven subscription)|为订阅值（例如，员工电子邮件地址的列表）生成输出的一种订阅。|  
|datareader|由 ADO.NET 查询返回的一种数据流。|  
|数据层应用程序 (data-tier application)|一种应用程序，它捕获客户端-服务器或 3 层应用程序使用的 SQL Server 数据库和实例对象。|  
|数据层应用程序实例 (data-tier application instance)|在数据库引擎的某一实例上部署的 DAC 的副本。 在数据库引擎的同一实例上可以有多个 DAC 实例。|  
|数据层应用程序包 (data-tier application package)|一种包含为 DAC 定义的所有对象的 XML 清单；在开发人员生成 DAC 项目时将创建该包。|  
|date|一种 SQL Server 系统数据类型，用于存储从公元元年 1 月 1 日到公元 9999 年 12 月 31 日的日期值。|  
|DB|对其进行格式设置或排列以便允许轻松地搜索和检索的数据的集合。|  
|DBCS|可使用多个字节来表示单个字符的字符集。 DBCS 包括某些由 1 个字节构成的字符以及某些由 2 个字节构成的字符。 中文、日语和韩语等语言使用 DBCS。|  
|DBMS|物理数据库和用户之间的软件层。 该 DBMS 管理对数据库的所有访问。|  
|DDL|定义数据库的所有特性和属性（特别是记录布局、字段定义、键字段、文件位置和存储策略）的一种语言。|  
|DDL 触发器 (DDL trigger)|一种特殊的触发器，它在响应数据定义语言 (DDL) 语句时执行。|  
|deadlock|两个用户各拥有一个数据块的锁，并尝试获取对方的数据块锁时出现的情况。|  
|决策支持 (decision support)|旨在支持发现业务趋势所需的复杂分析的系统。|  
|决策树|由某些数据挖掘方法生成的树状数据模型。 决策树可用于预测。|  
|声明 (declaration)|标识符与和其相关的信息的绑定。 例如，生成某一常量的声明意味着将该常量的名称与其值绑定。 声明通常在程序的源代码中出现；实际绑定可在编译时或运行时发生。|  
|声明性管理框架 (Declarative Management Framework)|SQL Server 管理的基于策略的系统。|  
|声明性管理框架方面 (Declarative Management Framework Facet)|一组逻辑的预定义属性，它们在基于策略的管理中模拟某些类型的托管目标（例如数据库、表、登录名、视图等）的行为或特性。|  
|声明性引用完整性 (declarative referential integrity)|定义为强制表之间正确关系的表定义的一部分的外键约束。|  
|专用管理员连接 (dedicated administrator connection)|一种专用连接，可供管理员在数据库引擎将不响应日常连接时连接到服务器。|  
|default|在用户未指定替代项时程序自动使用的值。 假定某个程序正常工作而必须采用某一值或选项时默认值内置于该程序中。|  
|默认数据库|用户登录到 SQL Server 后立即与其建立连接的数据库。|  
|默认实例 (default instance)|与安装计算机具有相同名称的 SQL Server 实例。|  
|default language|在用户未指定语言时 SQL Server 为错误和消息使用的人类语言。|  
|默认成员 (default member)|在没有为维度指定成员的情况下，查询中所使用的维度成员。|  
|默认结果集 (default result set)|SQL Server 用于将结果集返回到客户端的默认模式。|  
|脱离 (defection)|从多服务器操作中删除一台服务器。|  
|延迟的事务 (deferred transaction)|在恢复的前滚阶段完成时未提交并且在数据库启动过程中由于回滚所需的数据处于脱机状态而无法回滚的事务。 此数据可驻留在某一页或文件中。|  
|退化维度 (degenerate dimension)|维度与度量值组之间的关系，在这种关系中，维度主表与度量值组表相同。|  
|DEK|与加密算法一起使用以便对数据进行加密和解密的位字符串。|  
|退化的注册模型 (delegated registration model)|一种注册模型，在此模型中，并非证书订阅方的某一人士发起证书事务。 然后，该证书订阅方通过提供一次性密码来完成该事务。|  
|DELETE 子句 (DELETE clause)|包含 DELETE 关键字和关联参数的 DML 语句的一部分。|  
|删除级别 (delete level)|在 Data Transformation Services 中，指的是要从数据仓库中删除的数据量和数据类型。|  
|分隔标识符 (delimited identifier)|数据库中的一种对象，该对象由于名称不符合常规标识符的格式设置规则，因此必须使用特殊字符（分隔符）。|  
|传递通道 (delivery channel)|分发服务器和传递服务之间的管道。|  
|传递通道类型 (delivery channel type)|传递通道的协议，如简单邮件传输协议 (SMTP) 或文件传输协议。|  
|传递扩展插件 (delivery extension)|将报表传递到特定目标（例如，电子邮件传递）的插件。|  
|传递协议 (delivery protocol)|用于将通知消息路由到外部传递系统的通信规则集。|  
|使非规范化 (denormalize)|用于将冗余引入到表中，以便合并相关表中的数据。|  
|部署|若要生成某一 DAC 实例，或者直接从 DAC 包生成，或者从以前导入到 SQL Server 实用工具的 DAC 生成。|  
|已部署环境 (deployed environment)|位于团队项目主机组并由 Microsoft Test Manager 控制的虚拟机组。 已部署环境可以正在运行或已停止。|  
|取消排队 (dequeue)|从队列中删除。|  
|派生列 (derived column)|通过对转换输入列应用表达式来创建新列值的转换。|  
|反序列化 (deserialization)|以应用程序可使用的对象形式将来自序列存储格式的对象转换为二进制格式的过程。 此过程在使用 Get 客户端 API 从缓存群集检索对象时发生。|  
|目标|将数据加载到数据存储区或创建内存中数据集的 SSIS 数据流组件。|  
|目标|提供自己的当前知识、从源提供程序接受变更列表，检测该列表与自己的项之间是否有冲突并将变更应用到自己的数据存储的一种同步提供程序。|  
|目标适配器 (destination adapter)|用来向数据存储区中加载数据的数据流组件。|  
|目标提供程序 (destination provider)|提供自己的当前知识、从源提供程序接受变更列表，检测该列表与自己的项之间是否有冲突并将变更应用到自己的数据存储的一种同步提供程序。|  
|检测 (detect)|发现任何情况。|  
|设备类型 (device type)|开发人员定义列表中的一个值，用来指定给定应用程序支持的设备类型。|  
|标注 (diacritic)|放在字符上方、下方或中间的标记，用于指示与未标记状态相比语音值的变化。|  
|标注字符 (diacritical mark)|放在字符上方、下方或中间的标记，用于指示与未标记状态相比语音值的变化。|  
|方言 (dialect)|用于分析字符串或查询语句的语法和一般规则。|  
|菱形关系 (diamond-shape relationship)|一种属性关系链，它可以拆分和重新联接，但是不包含冗余关系。 例如，"日 >月->年" 和 "日" >季度->年份具有相同的起点和终点，但没有任何共同关系。|  
|差异器 (differencer)|与创建 DifferencingService 对象的工具之间的接口。|  
|差异备份 (differential backup)|只包含自上次数据备份（差异备份所基于的备份）以来对数据库所做更改的备份。|  
|差异基准 (differential base)|数据库或其文件或文件组子集中所有数据的最新一次完整备份。|  
|摘要传递 (digest delivery)|一种通知发送方法，它在某一批处理内合并多个通知并且将生成的消息发送到订阅服务器。|  
|数字证书 (digital certificate)|通常用于身份验证以及帮助保护网络上信息的数字文档。 证书将公钥绑定到持有对应私钥的实体。 证书由颁发这些证书的证书颁发机构进行数字签名，可以针对用户、计算机或服务颁发证书。|  
|维度|将数据组织到多个层中的多维数据集的一种结构属性。 例如，Geography 维度可以包含成员 Country、Region、State 或 Province 以及 City。|  
|维度表达式 (dimension expression)|返回维度的有效多维表达式 (MDX)。|  
|维度粒度 (dimension granularity)|一个特定的维度相对于特定度量值组可用的最低级别。 “本质”或物理粒度始终针对将主维度表联接到主事实表的键。|  
|维度层次结构 (dimension hierarchy)|一种按每个成员都有一个父成员和零个或更多个子成员的方式组织维度成员的逻辑树结构。|  
|维度级别 (dimension level)|维度层次结构中成员集的名称，该集的所有成员与层次结构的根元素的距离相同。 例如，时间层次结构可以包含年、月和日级别。|  
|维度成员 (dimension member)|维度中的单个位置或项。 维度成员可以是用户定义的或预定义的，并且可具有与其相关联的属性。|  
|维度成员属性 (dimension member property)|维度成员的特性。 维度成员属性可以是字母数字、布尔值或日期/时间数据类型，并且可以是用户定义的或预定义的。|  
|维度表 (dimension table)|数据仓库中的一个表，其中的项描述事实数据表中的数据。|  
|直接连接 (direct connect)|连接到后端数据库的状态，因此在保存数据库关系图或其中的所选项时，对数据库关系图所做的任何更改会自动更新数据库。|  
|直接响应模式 (direct response mode)|SQL Server 统计信息的收集与 SQL Server 统计信息显示分开的默认模式。|  
|脏页 (dirty page)|包含尚未写入磁盘的修改的缓冲区页。|  
|脏读 (dirty read)|包含未提交数据的一种读取。|  
|已禁用的索引 (disabled index)|标记为已禁用的任何索引。 已禁用的索引不可由数据库引擎使用。 已禁用的索引的索引定义保留在没有基础索引数据的系统目录中。|  
|离散信号 (discrete signal)|由数量序列构成的一种时序，此类时序是针对离散整数域的一种功能。|  
|离散化 (discretize)|将一组连续数据的值放入组中以便得到离散数目的可能状态。|  
|离散化列 (discretized column)|表示有限、计数数据的列|  
|非重复计数度量值 (distinct count measure)|通常用于确定对于某个维度的每个成员，另一维度有多少不同的最低级别成员共享事实数据表中的行的一种度量值。|  
|分布式分区视图 (distributed partitioned view)|以水平方式联接存在于多个服务器上的一组成员表中的分区数据的视图，使这些数据看起来如同在一个表中。|  
|分布式查询 (distributed query)|访问多个数据源的数据的单个查询。|  
|分布式事务 (distributed transaction)|涉及多个数据源的事务。|  
|distribution cleanup agent|在 SQL Server 代理下运行的一种计划的作业。 在所有订阅服务器都已接收了某一事务后，该代理将从分发数据库中删除该事务。 它还在与快照文件相对应的条目已从分发数据库中删除后将这些文件从文件系统中清除。|  
|分发数据库 (distribution database)|分发服务器上的一种数据库，此类数据库存储用于复制的数据，包括事务、快照作业、同步状态以及复制历史记录信息。|  
|分发保持期|事务复制中事务存储在分发数据库中的时间，|  
|distributor|充当与一个或多个发布服务器相关联的复制特定数据的存储区的数据库实例。|  
|DMF|返回 SQL Server 中有关值、对象和设置的服务器状态信息的一组内置函数中的一种。|  
|DML|用于检索和操作数据的 SQL 语句的子集。 DML 语句通常以 SELECT INSERT UPDATE 或 DELETE 开头。|  
|DML 触发器 (DML trigger)|当修改指定表中的数据时执行的存储过程。|  
|DMV|返回 SQL Server 中有关值、对象和设置的服务器状态信息的一组内置视图。|  
|DMX|在 Analysis Services 中，指的是以编程方式执行数据挖掘任务的语句。|  
|域|可为函数中的独立变量或为某一数据库属性指定的一组可能值。|  
|域|网络环境中共享共同的数据库、目录数据库或树的计算机的集合。 域作为具有公共规则和过程的一个单元进行管理，可包含安全策略，并且每个域都具有唯一的名称。|  
|域上下文 (domain context)|域服务的客户端表示形式。|  
|域完整性 (domain integrity)|数据特定列的项的有效性|  
|域操作 (domain operation)|对客户端应用程序公开的针对域服务的一种方法。 它使客户端应用程序能够对实体执行操作，例如查询、更新、插入或删除记录。|  
|域服务 (domain service)|封装应用程序的业务逻辑的一种服务。 它在服务层中公开一组相关的域操作。|  
|休眠的会话 (dormant session)|处于预登录状态的会话。 可以启动或结束会话来修改它们的状态，但它们通常保留为“睡眠/空闲”状态（如会话已启动且在服务器上处于打开状态以供客户端使用时）或“休眠”状态（如会话已结束且当前在服务器上无法用于客户端时）。|  
|双字节字符集 (double byte character set)|可使用多个字节来表示单个字符的字符集。 DBCS 包括某些由 1 个字节构成的字符以及某些由 2 个字节构成的字符。 中文、日语和韩语等语言使用 DBCS。|  
|双字节字符集 (double-byte character set)|可使用多个字节来表示单个字符的字符集。 DBCS 包括某些由 1 个字节构成的字符以及某些由 2 个字节构成的字符。 中文、日语和韩语等语言使用 DBCS。|  
|闭|表示计算机、打印机、网络上的通信线路和其他此类硬件未工作。|  
|仅下载类项目 (download-only article)|合并发布中只能在发布服务器或使用服务器订阅的订阅服务器上更新的项目。|  
|DPM 客户端 (DPM Client)|此 Data Protection Manager (DPM) 客户端使用户能够按照其备份管理员配置的公司保护策略保护和还原其数据。|  
|DPM 引擎 (DPM engine)|DPM 用于保护和还原数据的策略驱动的引擎。|  
|DPM Management Shell|基于 Windows PowerShell (Powershell.exe) 的一种命令 Shell，它可用于在 Data Protection Manager 中执行功能的 cmdlet。|  
|DPM Online|作为联机远程备份提供的一种功能，它既用于在现场外安全地存储数据以便长期使用，又用于灾难恢复 (DR)。|  
|DPM Online 帐户 (DPM Online account)|DPM 用来启动 DPM Online 服务的一种用户帐户。|  
|DPM Online 缓存 (DPM Online cache)|DPM Online 所要求的一种缓存卷，DPM 服务器将在其中存储信息以便更快备份和从 DPM Online 恢复。|  
|DPM Online 保护 (DPM Online protection)|使用 DPM Online 通过创建和维护联机数据的副本和恢复点以防数据丢失或损坏的过程。|  
|DPM Online 保护组 (DPM Online protection group)|共享相同的 DPM Online 保护配置的数据源的集合。|  
|DPM Online 恢复 (DPM Online recovery)|管理员从连接 Internet 的 DPM 服务器上的联机恢复点恢复以前版本的受保护数据的过程。|  
|DPM Online 恢复点 (DPM Online recovery point)|可从 DPM Online 提供的数据源的前一版本的日期和时间。|  
|DPM Online 副本 (DPM Online replica)|DPM Online 上联机保护的数据源的完整副本。 DPM 服务器上联机保护组的每个成员都与某一 DPM Online 副本相关联。|  
|DPM 角色 (DPM role)|DPM 管理员用于管理最终用户使用的 DPM 功能的用户、对象和权限的分组。|  
|DPM 自助式恢复配置工具 (DPM Self-Service Recovery Configuration Tool)|一种工具，DPM 可以利用该工具通过创建和管理 DPM 角色（用户、对象和权限的分组）授权最终用户执行数据的自助式恢复。|  
|DPM 自助式恢复工具 (DPM Self-Service Recovery Tool)|一种工具，最终用户可以使用该工具恢复来自 DPM 的备份，而无需 DPM 管理员执行任何操作。|  
|用于 SQL Server 的 DPM 自助式工具 (DPM Self-Service Tool for SQL Server)|用于 SQL Server 的一种工具，它使备份管理员能够授权最终用户从 DPM 恢复 SQL Server 数据库的备份，而无需备份管理员进一步执行操作。|  
|DPM SRT|随 DPM 提供的软件，用于简化针对 DPM 服务器以及 DPM 保护的计算机的 Windows Server 2003 裸机恢复。|  
|用于 SQL Server 的 DPM SST (DPM SST for SQL Server)|用于 SQL Server 的一种工具，它使备份管理员能够授权最终用户从 DPM 恢复 SQL Server 数据库的备份，而无需备份管理员进一步执行操作。|  
|DPM 系统恢复工具 (DPM System Recovery Tool)|随 DPM 提供的软件，用于简化针对 DPM 服务器以及 DPM 保护的计算机的 Windows Server 2003 裸机恢复。|  
|DQS|一种基于知识的数据质量系统，它使用户能够执行知识发现和管理、数据清除、数据匹配、与引用数据服务集成以及集成的事件探查。|  
|DQS 知识库 (DQS knowledge base)|Data Quality Services 用于提高数据质量的元数据存储库。 此元数据可由用户以交互方式创建，也可由 Data Quality Services 平台在自动的知识发现过程中创建。|  
|钻取 (drillthrough)|在 Analysis Services 中，是指检索用来汇总多维数据集单元数据的详细数据的一种方法。|  
|钻取报表 (drill-through report)|在用户单击报表中的某一项时显示的辅助报表。 详细数据将显示在相同的报表中。|  
|下拉列表 (drop-down list)|可以打开以便显示针对某一给定字段的所有选择的列表。|  
|DSN|用于将应用程序连接到特定 ODBC 数据库的信息的集合。|  
|无 DSN 连接 (DSN-less connection)|一种数据连接，它根据数据源名称 (DSN) 中的信息建立，但作为项目或应用程序的一部分进行存储。|  
|dump|出于存档目的或为了确保文件的安全而对程序、磁盘或数据进行的复制。|  
|转储设备 (dump device)|包含备份介质的磁带机或磁盘驱动器。|  
|动态游标 (dynamic cursor)|一种打开时可以反映对基础数据所做的数据修改的游标。|  
|动态筛选器 (dynamic filter)|可以在合并复制中使用的行筛选器，通过它可以基于系统函数或用户定义的函数（例如 SUSER_SNAME()）限制复制到订阅服务器的数据。|  
|动态锁定 (dynamic locking)|SQL Server 用来确定要在任一时刻使用的最具成本效益的锁的过程。|  
|动态管理函数 (dynamic management function)|返回 SQL Server 中有关值、对象和设置的服务器状态信息的一组内置函数中的一种。|  
|动态管理视图 (dynamic management view)|返回 SQL Server 中有关值、对象和设置的服务器状态信息的一组内置视图。|  
|动态恢复 (dynamic recovery)|检测和/或尝试更正关系数据库管理系统 (RDBMS) 内的软件故障或数据完整性损失的过程。|  
|动态路由 (dynamic routing)|自动调整为网络的当前状况的路由。 动态路由通常使用若干动态路由协议之一，例如路由信息协议 (RIP) 和边界网关协议 (BGP)。 请与静态路由进行比较。|  
|动态快照 (dynamic snapshot)|在合并复制中，仅包含单个分区中的数据的快照。|  
|预先加载 (eager loading)|一种加载模式，在其中，一组特定的相关对象将与已在查询中显式请求的对象一起加载。|  
|边缘事件 (edge event)|其事件负载在给定时间间隔内有效的一种事件；但在到达 CEP 服务器时只知道开始时间。 事件的有效结束时间稍后在单独的边缘事件中提供。|  
|有效策略 (effective policy)|为一个目标启用的一组策略。|  
|电子邮件|文本消息和计算机文件通过通信网络（例如局域网或 Internet）进行的交换。|  
|加密|将可读取数据（明文）转换为代码形式（加密文本）以防其被未授权方读取的过程。|  
|加密密钥 (encryption key)|与加密算法一起使用以便对数据进行加密和解密的位字符串。|  
|端帽 (end cap)|表示包含未连接端（例如线条、笔画的末端）的路径。 您可以通过应用四个端帽样式之一，更改每个笔画末端的外形：平端帽、圆端帽、方形端帽和三角形端帽。|  
|endpoint|同步提供程序及其关联的副本。|  
|端点映射程序 (endpoint mapper)|远程过程调用 (RPC) 服务器上的一种服务，它维护一个动态端点的数据库并且允许客户端将接口/对象 UUID 对映射到本地动态端点。|  
|排队 (enqueue)|将某一项置于队列中。|  
|enroll|将 SQL Server 的某一实例添加到实用工具控制点管理的 SQL Server 实例组中。|  
|注册 (enrollment)|请求、接收和安装证书的过程。|  
|注册代理 (Enrollment Agent)|用于代表其他用户帐户请求智能卡证书的用户帐户。 一个特定的证书模板将应用于注册代理。|  
|企业许可证 (enterprise license)|授权保护单台计算机上的文件和应用程序资源的许可证。|  
|实体|在 Reporting Services 中，是指模型项的逻辑集合，包括源字段、角色、文件夹和表达式，它们都是以熟悉的业务术语表示的。|  
|实体完整性 (entity integrity)|一种状态，在该状态下，每个表的每一行都能唯一标识。|  
|包络线公式 (envelopes formula)|通过将指定百分比用作移位，计算在移动平均线之上和之下的“包络线”的财务公式。 包络线指标用于创建买卖信号。 可以指定公式用于计算包络线的百分比。|  
|同等联接 (equijoin)|一种联接，它比较所联接的列中的值是否相等并将所有列都包括在结果中。|  
|Equirectangular 投影 (equirectangular projection)|地图报表项中一种非常简单的等距柱面投影，其中，水平坐标是经度，垂直坐标是纬度。|  
|错误处理|处理程序运行过程中发生的错误（或异常）的过程。 某些编程语言（例如 C++、Ada 和 Eiffel）具有用于协助进行错误处理的功能。|  
|错误列表|显示 T-SQL 语法或依赖关系错误的窗格的名称。|  
|错误日志 (error log)|列出在操作过程中遇到的错误的文件。|  
|错误状态号 (error state number)|与 SQL Server 消息关联的编号，用来帮助 Microsoft 支持工程师查找发出消息的特定代码位置。|  
|ETL|从不同源提取数据、将数据转换为一致的类型并加载转换后的数据以供应用程序使用的行为。|  
|基于 ETW 的日志接收器 (ETW-based log sink)|使用 Windows 内的 Windows 事件跟踪 (ETW) 框架捕获缓存客户端或缓存主机上的跟踪事件的方法。|  
|event|StreamInsight 服务器处理的基本数据单位。 每个事件都包含一个标题，该标题定义事件的类型和事件的临时属性。 事件（CTI 事件除外）通常包含事件负载，事件负载是一种 .NET 数据结构，其中包含与事件关联的数据。|  
|event|系统或应用程序中发生的任何需要通知用户或向日志中添加项的重要事情。|  
|事件类别 (event category)|在 SQL 跟踪中，指的是一组类似且逻辑上相关的事件类。|  
|事件历史记录 (event chronicle)|存储事件状态信息的表。|  
|事件历史记录规则 (event chronicle rule)|管理事件历史记录中的数据的一条或多条 Transact-SQL 语句。|  
|event 类|在 SQL 跟踪中，是指定义事件的属性集合。|  
|事件分类 (event classification)|区分在缓存客户端和缓存主机上发生的事件类型的一种方法。 Windows Server AppFabric 日志接收器将遵循使用 System.Diagnostics.TraceLevel 枚举建立的分类。|  
|事件收集存储过程 (event collection stored procedures)|系统生成的存储过程，应用程序可以调用此存储过程将事件提交至应用程序数据库中的事件表。|  
|事件处理程序 (event handler)|为了响应某个事件而执行的软件例程。|  
|事件标头 (event header)|事件中用来定义事件的临时属性和事件类型的部分。 临时属性包括与事件关联的有效开始时间和结束时间。|  
|事件类型 (event kind)|定义事件类型的事件元数据。|  
|事件模型 (event model)|定义事件的临时特性（形状）的事件元数据。|  
|事件通知 (event notification)|一种将有关数据库事件的信息发送到 Service Broker 的特殊触发器。|  
|事件负载 (event payload)|事件的数据部分，其中的数据字段定义为 CLR（公共语言运行时）类型。 事件负载是一种特型结构。|  
|事件提供程序 (event provider)|一种提供程序，它监视事件的来源，并且当事件发生时通知事件表。|  
|事件源 (event source)|事件的发源点。|  
|事件表 (event table)|应用程序数据库中存储事件数据的表。|  
|用于基于 Windows (ETW) 的日志接收器的事件跟踪 (Event Tracing for Windows (ETW)-based log sink)|使用 Windows 内的 Windows 事件跟踪 (ETW) 框架捕获缓存客户端或缓存主机上的跟踪事件的方法。|  
|所有人|一种用户帐户类型。|  
|逐出 (eviction)|从缓存主机或存储缓存对象的主机的内存中物理删除缓存对象的过程。 执行此过程通常是为了检查缓存主机服务的内存使用率。|  
|排他锁 (exclusive lock)|一种锁，用来防止在事务结束时释放资源的原始锁之前，任何其他事务获取该资源的锁。|  
|执行 (execute)|执行某一指令。|  
|执行计划窗格 (Execution Plan pane)|一种选项卡，承载 SQL Server 使用的估计或实际执行计划的输出。|  
|执行树 (execution tree)|SQL Server 2005 Integration Services 包数据流中的数据通过转换从源到达目标的路径。|  
|退出模块 (exit module)|在颁发证书后执行后处理（例如将已颁发的证书发布到 Active Directory）的一种证书服务组件。|  
|expiration|对象超过缓存超时值的那一时间点。 在某一对象到期时，该对象将被逐出。|  
|显式顶端 (explicit cap)|用作派生层次结构顶层的显式层次结构。|  
|显式层次结构 (explicit hierarchy)|在 Master Data Services 中，指的是使用合并成员对其他合并成员和叶成员进行分组的层次结构。|  
|显式加载 (Explicit Loading)|一种加载模式。在该模式下，对导航属性使用 Load 方法显式请求相关对象才加载这些对象。|  
|显式事务 (explicit transaction)|包含在事务分隔符（用于定义事务的开始和结束）内的一组 SQL 语句。|  
|分离型饼图 (exploded pie)|显示各个值在总计值中所占的比例并重点强调各个值（通过将饼的每一片显示为“抽离的”或独立于整体的）的一种饼图。|  
|分离型饼图 (exploded pie chart)|显示各个值在总计值中所占的比例并重点强调各个值（通过将饼的每一片显示为“抽离的”或独立于整体的）的一种饼图。|  
|指数移动平均线 (exponential moving average)|移动平均线公式对一段时间内的最新数据赋予较大权重，较旧数据赋予较小权重。 该公式应用按指数规律减小的加权系数。 每个较旧数据点的权重按指数规律减小，这为最近观察结果提供高得多的权重，但仍不会完全放弃较旧的观察结果。|  
|导出格式 (export format)|用于订阅和 HTML 查看器的用户界面文本。 与呈现扩展插件相对应。|  
|表达式|运算符、常量、文本值、函数以及计算结果为单个值的字段（列）、控件和属性的名称的任意组合。|  
|表达式宿主程序集 (expression host assembly)|在一个报表中找到的所有表达式都被编译成一个程序集。 表达式宿主程序集作为已编译报表的一部分进行存储。|  
|扩展权限 (extended permission)|特定于添加到标准 Active Directory 对象架构的一种权限。  与新对象相关联的权限扩展了现有的默认权限集。|  
|扩展属性|特对于数据库或数据库对象的用户定义文本（说明性或指导性文本，包括输入掩码和格式设置规则）。 此文本作为数据库或对象的属性存储在数据库中。|  
|身份验证的扩展保护|帮助避免中间人 (MITM) 攻击的一种安全功能。|  
|扩展存储过程 (extended stored procedure)|动态链接库 (DLL) 中的一种函数，它使用 SQL Server 扩展存储过程 API 进行编码。 然后，可以使用执行 Transact-SQL 存储过程所用的相同语句，从 Transact-SQL 中调用这种函数。|  
|可扩展样式表语言 (Extensible Stylesheet Language)|一个 XML 词汇表，用来通过定义呈现规则的样式表将 XML 数据转换为其他形式（如 HTML）。|  
|可扩展样式表语言转换 (Extensible Stylesheet Language Transformation)|一种基于 XML 的声明语言，用于显示或转换 XML 数据。|  
|可扩展样式表语言转换 (Extensible Stylesheet Language Transformations)|一种基于 XML 的声明语言，用于显示或转换 XML 数据。|  
|区 (extent)|磁盘或其他直接访问存储设备上操作系统为特定文件或程序保留的一个连续的存储空间块。|  
|外部传递系统 (external delivery system)|将格式化通知传递到目标设备的系统（如 Microsoft Exchange Server）。|  
|extract|生成一个 DAC 包文件，其中包含现有数据库中所有对象的定义以及与数据库相关联的实例对象。|  
|提取、转换和加载 (extraction, transformation, and loading)|从不同源提取数据、将数据转换为一致的类型并加载转换后的数据以供应用程序使用的行为。|  
|facet|一组逻辑的预定义属性，它们在基于策略的管理中模拟某些类型的托管目标（例如数据库、表、登录名、视图等）的行为或特性。|  
|方面|一组逻辑的预定义属性，它们在基于策略的管理中模拟某些类型的托管目标（例如数据库、表、登录名、视图等）的行为或特性。|  
|方面属性 (facet property)|应用于基于策略的管理中的特定方面的预定义属性。|  
|事实 (fact)|数据仓库的事实数据表中的行。 事实数据包含定义数据事件（如销售事务）的值。|  
|事实维度 (fact dimension)|维度与度量值组之间的关系，在这种关系中，维度主表与度量值组表相同。|  
|事实数据表 (fact table)|数据仓库架构中的中央表，它包含将事实数据与维度表关联的数字度量值和键。|  
|工厂方法 (factory method)|通常定义为静态的一种方法，其用途是返回某个类的实例。|  
|故障转移 (fail over)|将处理从失败的组件切换到其备份组件。|  
|失败的事务 (failed transaction)|因为遇到错误而不能完成的事务。|  
|故障转移群集 (failover cluster)|位于一个位置中的一组服务器，它们联网在一起以便在其中一台服务器发生故障时提供实时备份。|  
|故障转移群集|一个高可用性进程，在其中，在一台计算机上运行的应用程序或服务的实例可以在第一台计算机发生故障时故障转移到故障转移群集中的另一台计算机。|  
|故障转移伙伴 (failover partner)|在与伙伴服务器的连接失败时使用的服务器。|  
|防故障操作员 (fail-safe operator)|在无法联系到指定的操作员时接收警报的用户。|  
|失败通知 (failure notification)|在缓存客户端缺少一个或多个缓存通知时触发的一种缓存通知类型。|  
|严重错误 (fatal error)|导致系统或程序突然失败并且没有希望恢复的一种错误。 灾难性错误的一个例子是无法处理的未捕获的异常。|  
|联合数据库服务器 (federated database servers)|通过承载分布式分区视图的不同部分来分担数据处理负荷的一组相连服务器。|  
|馈送使用方 (feed consumer)|一种软件组件，它通过使用同步提供程序从 FeedSync 馈送提取项并将其应用于目标副本。|  
|纤程 (fiber)|一种在单个 OS 线程内计划的 Windows NT 轻型线程。|  
|纤程模式 (fiber mode)|SQL Server 实例为每个 SQL 计划程序分配一个 Windows 线程，然后为每个工作线程分配一个纤程（工作线程数不能超过 max worker threads 选项中设置的值）的一种情况。|  
|field|窗口或记录中存储单个数据值的区域。|  
|字段长度|在大容量复制中，表示大容量复制字符格式数据文件中的数据项所需的最大字符数。|  
|字段封送处理程序 (field marshaller)|处理字段封送的一种 SQL Server 功能。|  
|字段终止符 (field terminator)|在大容量复制中，是指标记字段或行结尾的一个或多个字符，用来将数据文件中的一个字段或行与下一个字段或行分隔开。|  
|文件备份 (file backup)|一个或多个文件或文件组中所有数据的备份。|  
|文件差异备份 (file differential backup)|只包含自最新文件备份以来对每个文件所做更改的一个或多个文件的备份。 文件差异备份需要以完整文件备份为基础。|  
|文件 DSN (file DSN)|文件数据源名称。 在安装了相同驱动程序的所有用户之间共享的、基于文件的数据源。 这些数据源不是专属于一个用户，也不是仅供一台计算机使用。|  
|文件映射 (file mapping)|文件的内容与某个进程的部分虚拟地址空间的关联。|  
|文件还原 (file restore)|还原数据库的一个或多个文件的操作。|  
|文件滚动 (file rollover)|程序基于某一事件关闭某个文件并创建一个新文件的过程。|  
|filegroup|一个或多个数据文件的命名集合，构成单个数据分配单元或用于数据库管理的单个单元。|  
|文件映射对象 (file-mapping object)|用来维护文件内容与某个进程的部分虚拟地址空间的关联的对象。|  
|文件流 (filestream)|用来保存文件数据的字节序列。|  
|填充因子 (fill factor)|索引的属性，用来定义 SQL Server 数据库引擎确定每页索引填充的程度。|  
|筛选器遗忘知识 (filter forgotten knowledge)|用作筛选器跟踪起点的知识。 筛选器跟踪副本可以通过删除虚影并提前了解筛选器遗忘知识，以包含已被删除的虚影的最高版本，从而节省存储空间。|  
|筛选键 (filter key)|在筛选键映射中映射为筛选器的 4 字节的值。|  
|筛选副本 (filtered replica)|只为筛选器中的项存储项数据的副本，如介质存储副本，它只存储评价为三星或更高级别的歌曲。|  
|筛选器跟踪副本 (filter-tracking replica)|可以标识筛选器中有哪些项以及最近哪些项移入或移出了筛选器的副本。|  
|细粒度锁 (fine-grained lock)|适用于少量代码或数据的锁。|  
|适合 (fit)|用于评估数据挖掘算法是否成功的条件之一。 适合通常表示为 0 和 1 之间的值，并且通过取评估的事例的预测值和实际值之间的协方差并且除以相同预测值和实际值的标准方差进行计算。|  
|固定数据库角色 (fixed database role)|每个数据库中都存在的预定义角色。 该角色的作用域仅限于在其中定义该角色的数据库。|  
|固定服务器角色 (fixed server role)|存在于服务器级别的预定义角色。 该角色的作用域仅限于在其中定义该角色的 SQL Server 实例。|  
|FK|某一数据库表中来自另一个表（也称作“被引用表”）的键，并且其值匹配该被引用表中的主键 (PK) 或唯一键。|  
|平面文件 (flat file)|由一种记录类型的记录组成的文件，其中没有用来控制记录之间的关系的嵌入的结构信息。|  
|平展 (flatten)|将嵌套的结构转换为平面结构。|  
|平展界面 (flattened interface)|创建用来组合多个界面的成员的界面。|  
|平展行集 (flattened rowset)|表现为二维行集的多维数据集，其中多个维度的元素的唯一组合在一个轴上进行组合。|  
|可变 ID (flexible ID)|分配给各种同步实体（如副本）的标识符。 标识符的长度可以是固定的，也可以是可变的。|  
|可变标识符 (flexible identifier)|分配给各种同步实体（如副本）的标识符。 标识符的长度可以是固定的，也可以是可变的。|  
|折叠计数 (fold count)|表示将在原始数据集中创建的分区数的值。|  
|文件夹层次结构 (folder hierarchy)|绑定的命名空间，用来唯一标识在报表服务器上存储并由其管理的所有报表、文件夹、共享数据源项和资源。|  
|强制服务 (forced service)|在数据库镜像会话中，是指在负责将服务传输到镜像数据库（但它处于未知状态）的主体服务器出现故障时数据库所有者启动的故障转移。 数据可能丢失。|  
|外键 (foreign key)|某一数据库表中来自另一个表（也称作“被引用表”）的键，并且其值匹配该被引用表中的主键 (PK) 或唯一键。|  
|外键关联 (foreign key association)|实体之间的关联，通过外键属性进行管理。|  
|外表 (foreign table)|包含外键的表。|  
|格式化文件 (format file)|包含元信息（例如数据类型和列大小）的文件，用于在从数据文件中读取数据或者向其中写入数据时解释数据。|  
|只进游标 (forward-only cursor)|不能滚动的游标；只能按照从第一行到最后一行的顺序读取行。|  
|自由格式语言 (free-form language)|其语法不受到行上字符位置的约束的一种语言。 C 和 Pascal 是自由格式语言，FORTRAN 则不是。|  
|完整备份 (full backup)|整个数据库的备份。|  
|完整差异备份 (full differential backup)|数据库中所有文件的备份，只包含自最新完整备份以来对数据库所做的更改。 完整差异备份需要以完整备份为基础。|  
|完全外部联接 (full outer join)|一种外部联接，这种联接中包括所有联接表中的所有行，无论它们是否匹配。 例如，书名和出版商之间的完全外部联接显示所有书名和所有出版商，甚至包括那些没有匹配值的行。|  
|完整恢复模式|一种数据库恢复模式，其中完整记录所有事务，并保留所有日志记录直至对它们进行备份。 如果在失败后备份了日志尾部，则数据库可恢复到失败点。 支持所有形式的恢复。|  
|全文目录 (full-text catalog)|全文索引组件以及在特定的目录结构中组织并且包含执行查询所需数据的其他文件的集合。|  
|全文启用 (full-text enabling)|允许在当前数据库上发生全文查询的过程。|  
|全文查询 (full-text query)|一种 SELECT 语句，在基于字符的列（数据类型为 char、varchar、text、ntext、nchar 或 nvarchar）中搜索词、短语、或者词或短语的多种形式的查询。 这种 SELECT 语句返回满足搜索条件的行。|  
|全文搜索|根据所有实际的文本数据，而不是根据包含一组有限关键字的索引来搜索一个或多个文档、记录或字符串。|  
|全文服务 (Full-Text service)|执行全文查询的 SQL Server 组件。|  
|全角字符 (full-width character)|在双字节字符集中，由 2 个字节表示并且通常具有半角差异的字符。|  
|function|作为单个逻辑单元运行的代码块。 函数通过名称来调用，接受可选输入参数，并返回状态和可选输出参数。 许多编程语言都支持函数。|  
|模糊分组 (fuzzy grouping)|Integration Services 中的一种数据清除方法，该方法检查数据集中的值，并确定相关数据行组和作为组的规范表示形式的一个数据行。|  
|模糊匹配 (fuzzy matching)|Integration Services 中的一种查找方法，它使用近似匹配算法来找到引用表中相似的数据值。|  
|GAC|计算机范围内的代码缓存，用于存储专为由计算机上的许多应用程序共享而安装的程序集。|  
|间隙深度 (gap depth)|指定沿着不同行显示的数据序列之间的距离作为分簇结果的一种度量方法。|  
|垃圾收集 (garbage collection)|自动恢复堆内存的过程。 将释放已分配但不再使用的内存块，并且可移动仍在使用中的内存块以便将可用内存合并到更大的块中。|  
|垃圾收集器 (garbage collector)|操作系统中执行垃圾收集的部分。|  
|门链接 (gated link)|两个或多个对象之间受保护的链接。 在执行期间，一旦已建立对象关系，则不跨越该对象关系检查权限，并且不必多次检查凭据。 如果向很多依赖性对象授权是不合适或不可管理的，则需要使用此类型的链接。|  
|聚集-写入操作 (gather-write operation)|数据库引擎将多个修改的数据页收集到单个写入操作中的一种性能优化。|  
|GC|自动恢复堆内存的过程。 将释放已分配但不再使用的内存块，并且可移动仍在使用中的内存块以便将可用内存合并到更大的块中。|  
|生成的代码 (generated code)|在 RIA 服务链接在服务器和客户端项目之间存在时，基于在中间层公开的操作和实体为客户端项目自动生成的代码。|  
|生成器 (generator)|将事件与订阅进行匹配并生成通知的 Notification Services 的组件。|  
|地理数据 (geographic data)|存储诸如 GPS 纬度和经度坐标之类的椭球体（圆形地球）数据的一种空间数据类型。|  
|几何图形数据 (geometric data)|支持平面或欧几里得（平面球）数据的一种空间数据类型。|  
|虚影 (ghost)|筛选副本中原先位于筛选器中但已移出的项或变更单位。|  
|虚影记录 (ghost record)|叶级索引中已标记为要删除但尚未由数据库引擎删除的行。|  
|虚影行 (ghost row)|叶级索引中已标记为要删除但尚未由数据库引擎删除的行。|  
|全局程序集缓存 (global assembly cache)|计算机范围内的代码缓存，用于存储专为由计算机上的许多应用程序共享而安装的程序集。|  
|全局默认值 (global default)|为特定数据库定义并由不同表的列共享的默认值。|  
|全局 ID (global ID)|分配给数据项的唯一标识符。 该标识符在所有客户端上必须是唯一的。 全局标识符是可变标识符，因此它可以使用任何格式，但全局标识符通常是 GUID 和 8 字节前缀。|  
|全局标识符 (global identifier)|分配给数据项的唯一标识符。 该标识符在所有客户端上必须是唯一的。 全局标识符是可变标识符，因此它可以使用任何格式，但全局标识符通常是 GUID 和 8 字节前缀。|  
|全局规则 (global rule)|为特定数据库定义并由不同表的列共享的规则。|  
|全局订阅 (global subscription)|一种对合并发布的订阅，它具有分配的优先级值，用来检测和解决冲突。|  
|全球化 (Globalization)|设计和开发软件产品以便在多个区域设置中运行的过程。 全球化涉及识别必须得到支持的区域设置，设计支持这些区域设置的功能，以及编写在任何受支持的区域设置中都同样很好地运行的代码。|  
|粒度|按其处理的单元大小（像素、数据集或时间段）对计算机活动或功能（例如屏幕分辨率、搜索和排序或者时间段分配）的描述，范围是从“粗糙”到“精细”。 片断越大，粒度越粗。|  
|粒度属性|用于指定给定维度相对于给定度量值组的粒度级别的单个属性。|  
|图形查询设计器 (graphical query designer)|Reporting Services 提供的一种查询设计器，用户可以使用它以交互方式生成查询并查看数据源类型 SQL Server、Oracle、OLE DB 和 ODBC 的结果。|  
|图形基元 (graphics primitive)|图形适配器可作为离散实体操作的一种基本形状（点、线条、圆形、曲线或多边形）。|  
|group|用作安全性或电子邮件通讯集合的用户、计算机、联系人和其他组的集合。 通讯组仅用于电子邮件。 安全组既用于授予对资源的访问权限，也用作电子邮件通讯列表。|  
|分组|报表中组合在一起的一组数据。|  
|半角字符 (half-width character)|在双字节字符集中，由一个字节表示并且通常具有全角差异的字符。|  
|硬盘 (hard disk)|一种并不灵活的盘片，其表面覆盖有可使用读/写头以磁性方式记录数据的材料。|  
|硬分页呈现器 (hard page-break renderer)|一种呈现扩展插件，它维护报表布局和格式，以便为一致的打印体验优化最终生成的文件，或者以书籍格式查看报表大纲。|  
|硬编码 (hard-coding)|将字符串或字符文本放在代码正文中（而不是放在外部资源文件中）的过程。|  
|硬编码 (hard-coding)|将数字常量基于假定的字符串长度；与语言或特定于区域性的事项有关的在代码中固定的假设 - 例如，字符串长度、日期格式等。|  
|硬件安全模块 (hardware security module)|一种提供加密功能的安全设备，通常通过提供在公钥加密中使用的私钥。|  
|硬件令牌 (hardware token)|一种提供加密功能的安全设备，通常通过提供在公钥加密中使用的私钥。|  
|哈希分区 (hash partitioning)|一种对表或索引进行分区的方法，它允许 SQL Server 应用内部哈希算法以便基于指定的分区数目以及一个或多个分区列的值将行分布到多个分区。|  
|热度地图 (heat map)|一种地图展示类型，其中，每个多边形的颜色强度对应于相关的分析数据。 例如，范围中较低的值显示为蓝色（冷色），较高的值显示为红色（暖色）。|  
|技术支持咨询 (helpdesk)|为组织的网络、硬件设备和软件提供技术协助的支持专业人员个体或团队。|  
|异类数据 (heterogeneous data)|以多种格式存储的数据。|  
|层次结构树 (hierarchy tree)|其中的元素在层次结构上彼此相关的一种结构。|  
|高可用性|一种 Windows Server AppFabric 功能，它通过将缓存数据的副本存储于多个缓存主机上，支持缓存数据的持续可用性。|  
|高可用性|系统或设备在需要时可用的一种能力。 如果用百分比的形式表示，则高可用性是实际服务时间除以所需服务时间。 尽管高可用性不会确保系统将不停机，但如果实现 99.999% 的网络正常运行时间，则网络通常被视作具备高可用性。|  
|高水印 (high watermark)|针对每个缓存主机的内存使用量阈值，它指定何时将对象从内存中逐出，直至内存使用量下降回低水印，而与对象是否到期无关。|  
|高须线 (high whisker)|盒须图上不属于离群值的最高值。|  
|提示 (hint)|指定的强制选项或策略，由 SQL Server 查询处理器针对 SELECT、INSERT、UPDATE 或 DELETE 语句执行。 提示将覆盖查询优化器可能为查询选择的任何执行计划。|  
|history|某一程序内用户操作的列表，例如在操作系统 shell 中输入的命令、通过使用 Gopher 传递的菜单或者使用 Web 浏览器访问的链接。|  
|可保持性 (holdability)|表示保持已处理并且通常在此后关闭的结果集打开（“暂挂”）的可能性。 例如：“SQL Server 仅在连接级别支持可保持性。”|  
|维持|保留用于度量数据挖掘模型结构准确性的定型数据的百分比。|  
|维持数据 (holdout data)|保留用于度量数据挖掘模型结构准确性的定型数据的百分比。|  
|维持存储区 (holdout store)|用于缓存维持数据的数据挖掘结构。 它包含对维持数据的引用。|  
|主页|报表服务器文件夹命名空间中的根文件夹。|  
|主页|充当超文本系统中的起始点的文档。 在万维网上，指的是网站中一组网页和其他文件的入口页。 在访问者使用 Web 浏览器导航到该站点时，将默认显示该主页。|  
|同类数据 (homogeneous data)|来自全由同一软件管理的多个数据源的数据。|  
|跃点 (hop)|在数据通信领域中，指分散在不同地理位置的网络中各路由器之间的路径的一段。|  
|跳跃窗口 (hopping window)|一种窗口，其中连续窗口是按固定时段在时间中向前“跳跃”的窗口。 窗口通过两个时间范围定义：周期 P 和窗口长度 L。对于每个 P 时间单位，都会创建一个大小为 L 的新窗口。|  
|水平分区|根据选定行将一个表分成多个表。|  
|水平拆分 (horizontal split)|CIDER Shell 的水平方向。|  
|热备用 (hot standby)|支持在已提交事务不丢失数据的情况下进行快速故障转移的备用服务器。|  
|热备用服务器 (hot standby server)|支持在已提交事务不丢失数据的情况下进行快速故障转移的备用服务器。|  
|HSM|一种提供加密功能的安全设备，通常通过提供在公钥加密中使用的私钥。|  
|HTML|标准通用标记语言的一种应用，它使用标记来对文档中的元素（例如文本和图形）进行标记，以便指示 Web 浏览器应该如何向用户显示这些元素以及如何响应用户操作。|  
|HTML 查看器 (HTML Viewer)|一种 UI 元素，包含一个报表工具栏和其他用于处理报表的导航元素。|  
|混合 OLAP|使用多维数据结构和关系数据库表的组合来存储多维数据的存储模式。|  
|超文本标记语言 (Hypertext Markup Language)|标准通用标记语言的一种应用，它使用标记来对文档中的元素（例如文本和图形）进行标记，以便指示 Web 浏览器应该如何向用户显示这些元素以及如何响应用户操作。|  
|标识字段 (identifying field)|将实体标识为唯一对象的字段或字段组。|  
|识别关系 (identifying relationship)|一种关系，其中主体实体的主键是依赖实体的主键的一部分。 在这种关系中，没有主体实体，依赖实体就不能存在。|  
|标识列 (identity column)|表中已分配了标识属性的列。|  
|标识属性 (identity property)|生成唯一标识表中每行的值的属性。|  
|象形文字 (ideograph)|亚洲书写体制中的一种字符，它代表一个概念或想法，而不是特定的词语或发音。|  
|象形字符 (ideographic character)|亚洲书写体制中的一种字符，它代表一个概念或想法，而不是特定的词语或发音。|  
|IEC|负责开发国际数据通信标准的两个国际标准组织之一。 国际电工委员会 (IEC) 与国际标准化组织 (ISO) 密切合作来定义计算标准。 它们共同发布了 SQL 的 ISO/IEC SQL-92 标准。|  
|立即更新订阅 (immediate updating subscription)|事务发布的订阅，用户可以在订阅服务器上对其进行数据修改。 然后，使用两阶段提交协议 (2PC) 将数据修改立即传播到发布服务器。|  
|隐式游标转换 (implicit cursor conversion)|返回一种不同于用户所声明的游标类型的游标。|  
|隐式事务 (implicit transaction)|一种连接选项，由连接执行的每个 SQL 语句都视为单独的事务。|  
|隐式权限 (implied permission)|用于执行特定于角色的活动的权限。|  
|非活动数据源 (inactive data source)|已在 DPM 服务器上备份但不再被主动保护的数据源。|  
|包含列的索引 (included column index)|同时包含键列和非键列的非聚集索引。|  
|传入消息 (incoming message)|已跨一个或多个消息传送系统发送的消息。 此类消息可能仅发送给您，也可能发送给其他许多收件人。 传入消息放置于指定为存放特定类别的消息的接收文件夹中。 您可为处理的每个消息类别设置不同的接收文件夹，或者使用一个文件夹用于所有类别。|  
|增量更新 (incremental update)|向现有多维数据集或维度添加新成员或向分区添加新数据的一组操作。|  
|独立关联 (independent association)|实体之间的关联，由独立对象表示和跟踪。|  
|索引分配映射 (Index Allocation Map)|用于映射分配单元使用的数据库文件中 4 GB 部分中的区的页。|  
|索引页 (index page)|包含索引行的数据库页。|  
|索引视图 (indexed view)|应用了唯一聚集索引的视图，可提高某些类型查询的性能。|  
|推理攻击 (inference attack)|一种安全威胁：恶意用户不用真正访问数据即可得出数据的值，例如，通过监视查询的响应时间。|  
|信息模型 (information model)|一种面向对象的架构，定义用于指定应用程序、进程、组件或软件项目的结构和行为的元数据构造。|  
|信息技术 (information technology)|公司数据处理部门的正式名称。|  
|初始快照 (initial snapshot)|包括复制所需的架构和数据、约束、扩展属性、索引、触发器以及系统表的文件。|  
|初始同步 (initial synchronization)|订阅的首次同步。在此过程中会将复制所需的系统表和其他对象以及每个项目的架构和数据复制到订阅服务器。|  
|起始磁带 (initial tape)|使用磁带备份设备的介质集中，介质簇中的第一个磁带。|  
|内部联接|通过比较源表间共享的列的值，从多个源表检索行的操作。 内部联接排除在其他源表中没有匹配行的源表中的行。|  
|亲身身份验证 (in-person authentication)|用于完成证书请求事务的物理身份验证。 例如，请求解锁其个人标识号 (PIN) 的最终用户将亲自拜访其证书管理员，并且提供含有标识（例如员工徽章或驱动程序许可证）的亲身身份验证。|  
|InProc|一种情况，其中，COM 对象的代码从 DLL 文件加载并且位于与客户端相同的进程中。|  
|输入适配器 (input adapter)|从外部源（如数据库、文件、股票资讯、网络端口、制造设备等）接受传入事件流的一种适配器。|  
|输入成员 (input member)|其值直接从数据源加载而不是从其他数据计算得到的成员。|  
|输入集 (input set)|提供给多维表达式 (MDX) 值表达式的数据集，表达式使用这些数据进行运算。|  
|输入源 (input source)|用作查询的信息源的任何表、视图或架构关系图。|  
|输入流 (input stream)|在程序中用作与特定任务或目标相关联的字节序列的一种信息流。 输入流包括从键盘到内存读取的字符序列以及从磁盘文件读取的数据块。|  
|不感知游标 (insensitive cursor)|一种打开时不反映其他用户对基础数据所做的数据修改的游标。|  
|插入事件 (insert event)|用于表示事件到达流中的事件类型。 插入事件类型由定义事件有效生命周期的元数据和事件的负载（数据）字段构成。|  
|插入查询 (Insert Into query)|将来自一个表的特定列和行复制到另一个表或同一个表中的查询。|  
|插入值查询|创建新行并将值插入到指定列中的一种查询（SQL 语句）。|  
|instance|计算机上运行的 SQL Server 副本。|  
|实例控制提供程序 (instance control provider)|一种提供程序，可用于针对实例存储区中的工作流实例发出控制命令。 例如，您可以使用 SQL 控制提供程序挂起、恢复或终止在 SQL Server 数据库中存储的实例。 在您执行控制实例存储区中的工作流实例的某一 cmdlet 时，该 cmdlet 在内部将该控制提供程序用于该实例存储区，以便向该实例发送命令。|  
|实例查询提供程序 (instance query provider)|一种提供程序，可用于针对实例存储区发出查询。 例如，SQL 查询提供程序允许针对 SQL Server 数据库中存储的工作流实例进行的查询。 在您执行针对实例存储区查询实例的某一 cmdlet 时，该 cmdlet 在内部使用查询提供程序从该存储区中检索实例。|  
|实例存储区 (instance store)|存储工作流实例状态和工作流实例元数据的一组数据库表。|  
|实例存储区提供程序 (instance store provider)|在 Windows AppFabric 中，指的是可用于创建实例存储区对象的一种提供程序。 例如，SQL 存储区提供程序允许客户端创建 SQL 工作流实例存储区对象，而后者又允许客户端将工作流实例保存到持久性存储区中以及从持久性存储区中检索工作流实例。|  
|集成|在计算中，指的是将不同的活动、程序或硬件组件组合到一个功能单元中。|  
|完整性 (integrity)|数据的精确性并且其符合其预期值，特别是在传输或处理后。|  
|完整性约束 (integrity constraint)|为表定义的属性，防止可能创建无效数据的数据修改。|  
|意向锁 (intent lock)|放置在资源层次结构的某个级别上的锁，以保护较低级别资源上的共享锁或排他锁。|  
|意向共享 (intent share)|放置在资源层次结构的某个级别上的锁，以保护较低级别资源上的共享锁或排他锁。|  
|交互式结构化查询语言 (interactive structured query language)|SQL Server 提供的交互式命令提示实用工具，使用户可以从服务器或工作站运行 Transact-SQL 语句或批处理并查看返回的结果。|  
|interface|一组定义的属性、方法和集合，构成行为和数据的逻辑分组。|  
|接口隐含 (interface implication)|如果一个接口隐含另一个接口，则实现第一个接口的任何类还必须实现第二个接口。 接口隐含用于信息模型中来获得多重继承的某些效果。|  
|中间语言 (Intermediate Language)|用作原始源语言（通常是高级语言）和目标语言（通常是机器代码）之间的中间步骤的一种计算机语言。 某些高级编译器使用汇编语言作为中间语言。|  
|国际电工委员会 (International Electrotechnical Commission)|负责开发国际数据通信标准的两个国际标准组织之一。 国际电工委员会 (IEC) 与国际标准化组织 (ISO) 密切合作来定义计算标准。 它们共同发布了 SQL 的 ISO/IEC SQL-92 标准。|  
|Internet 协议安全 (Internet Protocol security)|一组符合行业标准、基于加密的服务和协议，可帮助保护网络上数据的安全。|  
|进程间通信 (interprocess communication)|一个任务或进程与多任务操作系统中的其他任务或进程进行通信的功能。 常见的方法包括管道、信号量、共享内存、队列、信号和邮箱。|  
|间隔事件 (interval event)|其负载在给定的时间段内有效的事件。 间隔事件的元数据要求在事件元数据中同时提供间隔的开始时间和结束时间。 间隔事件只在此特定间隔内有效。|  
|间隔事件模型 (interval event model)|间隔事件的事件模型。|  
|调用操作 (invoke operation)|在无跟踪或延迟执行的情况下执行的一种域操作。|  
|IP 地址|出于通过传输数据包进行通信目的唯一标识连接到 Internet 的主机（计算机）与其他 Internet 主机的二进制编号。|  
|IPC|一个任务或进程与多任务操作系统中的其他任务或进程进行通信的功能。 常见的方法包括管道、信号量、共享内存、队列、信号和邮箱。|  
|IPsec|一组符合行业标准、基于加密的服务和协议，可帮助保护网络上数据的安全。|  
|隔离级别 (isolation level)|事务的属性，用于控制隔离数据以供一个进程使用并防止其他进程干扰的程度。|  
|ISQL|SQL Server 提供的交互式命令提示实用工具，使用户可以从服务器或工作站运行 Transact-SQL 语句或批处理并查看返回的结果。|  
|item|正在同步的数据或元数据的单位。 数据的一般项可能是文件或记录，元数据的一般项则可能为知识项。|  
|项级角色分配 (item-level role assignment)|一种应用于报表服务器文件夹命名空间中的项目的安全策略。|  
|项级角色定义 (item-level role definition)|一种安全模板，定义用来控制对报表服务器文件夹命名空间中的项的访问或与该项进行的交互的角色。|  
|迭代 (iterate)|反复执行一个或多个语句或指令。 这样执行的语句或指令被视为处于某一循环中。|  
|作业 (job)|程序为完成某一操作而连续执行的一系列指定操作（称为步骤）。|  
|作业历史记录 (job history)|保存作业的历史记录的日志。|  
|join|组合两个或更多个表的内容，生成合并每个表中的行和列的结果集。 通常使用这些表中的公共数据来联接表。|  
|联接列 (join column)|联接条件中引用的列。|  
|联接条件 (join condition)|指定表如何通过其联接列联系起来的比较子句。|  
|联接筛选器 (join filter)|合并复制中使用的一种筛选器，它将一个表中的行筛选器扩展到相关的表。|  
|join 运算符|联接条件中的一种比较运算符，它确定如何对条件两侧进行计算以及返回哪些行。|  
|联接路径 (join path)|指示两个表如何联系起来的一系列联接。|  
|联接表 (junction table)|在其他表之间建立关系的表。|  
|卡吉图 (Kagi chart)|用于跟踪价格波动和作出股票购买决策的一种图表，大多数情况下独立于时间。|  
|键|标识缓存中的对象的字符串。 该字符串在区域中必须唯一。 在添加对象时对象与某个键相关联，然后使用相同键检索对象。|  
|键|在加密、身份验证和数字签名中，指的是用于与某个算法一起使用以便对信息进行加密或解密的值。|  
|键|在数组中，按其对存储的数据进行组织和访问的字段。|  
|键|唯一地标识行（主键）、定义两个表之间的关系（外键）或用于生成索引的一个列或一组列。|  
|键属性 (key attribute)|用于将维度中的非键属性链接到相关度量的维度属性。|  
|键列|其内容唯一标识表中的每一行的列。|  
|密钥生成器 (key generator)|用于生成加密密钥材料的硬件或软件组件。|  
|关键绩效指标 (key performance indicator)|用于跟踪战略目标、目标、计划、行动或业务流程的绩效的预定义的度量。 KPI 是针对目标进行评估的。 这是直接获取自数据源的显式和可度量的值。 关键绩效指标 (KPI) 用于度量特定领域（例如每个客户的收入）中的绩效。|  
|键范围锁 (key range lock)|用于锁定表中记录之间范围的锁，以防止对一组记录进行虚拟添加或虚拟删除。 它确保可序列化事务。|  
|密钥恢复 (key recovery)|恢复用户的私钥的过程。|  
|密钥恢复代理 (Key Recovery Agent)|与证书管理员合作来恢复用户的私钥的指定用户。 一个特定的证书模板将应用于密钥恢复代理。|  
|由键集驱动的游标 (keyset-driven cursor)|一种打开时显示其他用户对其成员行所做的更新效果（但不显示插入或删除效果）的游标。|  
|知识 (knowledge)|与每个参与者看到和维护的所有变更有关的元数据。|  
|KPI|用于跟踪战略目标、目标、计划、行动或业务流程的绩效的预定义的度量。 KPI 是针对目标进行评估的。 这是直接获取自数据源的显式和可度量的值。 关键绩效指标 (KPI) 用于度量特定领域（例如每个客户的收入）中的绩效。|  
|KRA|与证书管理员合作来恢复用户的私钥的指定用户。 一个特定的证书模板将应用于密钥恢复代理。|  
|非 Unicode 程序的语言 (Language for non-Unicode programs)|一个“区域和语言选项”设置，为特定计算机指定默认代码页和关联的位图字体文件，此设置影响特定计算机的所有用户。 通过指定默认代码页和字体，为一种操作系统语言版本编写的非 Unicode 应用程序可以直接在其他操作系统语言版本上正确运行。|  
|语言服务分析器 (language service parser)|用于描述源代码中标记的功能和范围的组件。|  
|语言服务扫描器 (language service scanner)|用于标识源代码中标记的类型的组件。 此信息用于语法突出显示和快速标识可触发其他操作（例如括号匹配）的标记类型。|  
|闩锁 (latch)|一种短期的同步对象保护操作，此类操作无需为事务的整个生命周期锁定。 闩锁主要用于保护存储引擎主动从基表或索引传输到关系引擎的行。|  
|latency|在处理或传递数据时发生的延迟。|  
|延迟加载 (lazy loading)|一种数据加载模式。在该模式下，访问导航属性时才加载相关对象。|  
|惰性架构验证|一个选项，它将对远程架构进行检查以便根据查询验证其元数据的过程延迟到执行，以便提高性能。|  
|前导字节 (lead byte)|双字节字符中前面一半的字节值。|  
|前导主机 (lead host)|一种缓存主机，它设计为与其他前导主机一起工作以便使群集在任何时候均保持运行状态。|  
|叶 (leaf)|在树中表示的没有子对象的节点。|  
|叶级别 (leaf level)|聚集索引或非聚集索引的底层，或者层次结构的底层。|  
|叶成员 (leaf member)|没有后代的成员。|  
|叶节点 (leaf node)|在树中表示的没有子对象的节点。|  
|已知知识 (learned knowledge)|有关特定一组变更的源副本的当前知识以及记录的该副本的冲突信息。|  
|最早使用的 (least recently used)|缓存群集使用的逐出类型，其中，先逐出最近最少使用的对象，然后逐出最近常使用的对象。|  
|左外部联接 (left outer join)|一种外部联接，其中包括 JOIN 子句中最左侧表中的所有行。 在左表中的行与右表中的行不匹配时，来自右表的所有结果集中的列将被赋予值 NULL。|  
|级别|维度层次结构中成员集的名称，该集的所有成员与层次结构的根元素的距离相同。 例如，时间层次结构可以包含年、月和日级别。|  
|提升图|在 Analysis Services 中，是指对比较集中的每个数据挖掘模型的预测准确性进行比较的图表。|  
|轻型池|一个选项，该选项通过执行上下文切换内联化，减少有时在对称多处理 (SMP) 环境下遇到的、与过多的上下文切换有关的系统开销，从而降低用户/内核环的转换频率。|  
|线条层 (line layer)|地图报表中的一种层，它将空间数据显示为线条（例如，指示路径或路线的线条）。|  
|链接维度 (linked dimension)|某个多维数据集中对其他多维数据集（即，具有在相同或不同 Analysis Services 数据库中存在的不同数据源视图的多维数据集）中的维度的引用。 链接维度只能与源多维数据集中的度量值组相关，并且只能在源数据库中进行编辑。|  
|链接度量值组 (linked measure group)|某个多维数据集中对其他多维数据集（即，具有在相同或不同 Analysis Services 数据库中存在的不同数据源视图的多维数据集）中的度量值组的引用。  链接度量值组只能在源数据库中进行编辑。|  
|链接服务器 (linked server)|SQL Server 分布式查询所使用的 OLE DB 数据源的定义。 链接服务器定义指定访问数据所需的 OLE DB 访问接口，并包括足够的寻址信息供 OLE DB 访问接口连接数据。|  
|被链接表 (linked table)|由已定义为链接服务器的 OLE DB 数据源提供以供在 SQL Server 分布式查询中使用的 OLE DB 行集。|  
|链接表 (linking table)|与另两个表相关联并间接用作这两个表之间的关联的表。|  
|LINQ|用于定义一组查询运算符的查询语法，通过这些运算符，可以在任何基于 .NET 的编程语言中以直接的声明性方式表示遍历、筛选和投影操作。|  
|little endian|表示一种处理器内存体系结构，此体系结构存储数字以便首先放置最不重要的字节。|  
|本地缓存 (local cache)|一种功能，可使缓存对象的反序列化副本保存在运行支持缓存的应用程序的相同进程的内存中。|  
|本地分发服务器 (local Distributor)|同时配置为 SQL Server 复制的发布服务器和分发服务器的服务器。|  
|本地分区视图 (local partitioned view)|以水平方式联接存在于一台服务器上的一组成员表中的分区数据的视图，使这些数据看起来如同在一个表中。|  
|本地订阅 (local subscription)|合并发布的一种订阅，使用发布服务器的优先级值来检测冲突和解决冲突。|  
|区域设置|特定于语言和地域的规则和数据的集合。 区域设置包括有关排序规则、日期和时间格式设置、数字和货币约定，以及字符分类的信息。|  
|本地化 (localization)|改编产品和/或内容（包括文本和非文本元素）以便满足语言、区域性、政治期望和/或特定当地市场（区域性）的要求的过程。|  
|锁 (lock)|多用户环境中对资源的访问限制。|  
|锁升级|将许多细粒度的锁转换为较少粗粒度（从而降低系统开销）的锁的过程。|  
|日志备份 (log backup)|包括以前日志备份中未备份的所有日志记录的事务日志备份。 在完整恢复模式或大容量日志恢复模式下需要进行日志备份，但在简单恢复模式下不可用。|  
|日志链 (log chain)|数据库的一组连续的事务日志。 新日志链以创建数据库后生成的第一个日志备份开始，或者从数据库从简单模式切换到完整模式或大容量日志恢复模式时生成的第一个日志备份开始。 日志链在恢复之后的某一还原后分叉，并且创建新的恢复分支。|  
|日志提供程序|一种在运行时记录包信息的提供程序。 Integration Services 包括多种日志提供程序，可实现在包执行过程中捕获事件。 日志可以多种格式创建和存储，例如 XML、文本、数据库或 Windows 事件日志。|  
|日志读取器代理|复制中使用的可执行文件，用来监视为事务复制配置的每个数据库的事务，并将已为复制标记的事务从事务复制到分发数据库中。|  
|日志序列号 (log sequence number)|分配给事务日志中的每个项的唯一编号。  系统将根据创建实体的顺序依次分配 LSN。|  
|日志传送|以设定间隔将日志备份从读/写数据库（主数据库）复制到一个或多个远程服务器实例（辅助服务器）。 每个辅助服务器都具有通过还原主数据库的完整备份（而不恢复）而创建的称作辅助数据库的只读数据库。 辅助服务器将每个复制的日志备份还原到辅助数据库。 辅助服务器是用于主服务器的热备用服务器。|  
|日志传送配置 (log shipping configuration)|单个主服务器、一个或多个辅助服务器（每个服务器均有一个辅助数据库）和一个监视服务器。|  
|日志传送操作 (log shipping job)|执行下列日志传送操作之一的作业：备份主服务器上主数据库的事务日志（备份作业）、将事务日志文件复制到辅助服务器（复制作业）或将日志备份还原到辅助服务器上的辅助数据库（还原作业）。 备份作业驻留在主服务器上，复制和还原作业驻留各辅助服务器上。 另请参阅：主数据库、主服务器、辅助数据库、辅助服务器。|  
|日志接收器 (log sink)|缓存客户端和缓存主机的跟踪功能。 日志接收器从缓存客户端或缓存主机捕获跟踪事件，并且可以在控制台显示这些跟踪事件、将它们写入某一日志文件或者将它们报告给 Windows 中的 Windows 事件跟踪 (ETW) 框架。|  
|逻辑错误 (logic error)|诸如错误算法等此类错误，可导致程序生成不正确的结果，但不会阻止程序运行。 因此，逻辑错误通常很难发现。|  
|逻辑名称 (logical name)|SQL Server 用来标识文件的名称。|  
|逻辑记录 (logical record)|一项合并复制功能，您可以使用此功能来定义不同表中相关行之间的关系，以便将这些行作为一个单元来处理。|  
|登录 ID (login ID)|用于向操作系统、目录服务或分布式系统标识用户或实体的字符串。 例如，在 Windows® 集成身份验证中，登录名采用“DOMAIN\username”格式。|  
|登录安全模式 (login security mode)|决定 SQL Server 实例对登录请求所用验证方式的安全模式。|  
|长分析 (long parsing)|在 SQL 系统中，有两种类型的线程：一是短线程，即短期占用资源的进程；另一种是长线程，即长期占用资源的进程。 长分析就是对长期存在的线程进行分析。注：长/短的定义基于系统针对每个进程进行的计算/统计信息。|  
|低框 (Low Box)|盒须图上框的最低值。|  
|低水印 (low watermark)|每台缓存主机上的一个内存消耗量阈值，指定何时将到期的对象逐出内存。|  
|低须线 (low whisker)|盒须图上不属于离群值的最低值。|  
|LRU|缓存群集使用的逐出类型，其中，先逐出最近最少使用的对象，然后逐出最近常使用的对象。|  
|LSN|分配给事务日志中的每个项的唯一编号。  系统将根据创建实体的顺序依次分配 LSN。|  
|引诱攻击 (luring attack)|一种攻击，其中客户端被引诱而自主连接到攻击者。|  
|背景知识 (made-with knowledge)|在同步过程中，要在冲突检测中使用的源副本的当前知识。|  
|管理关系 (Manage Relationships)|一个用户界面元素，使用户能够在模型中查看、删除或创建新关系。|  
|托管代码 (managed code)|由公共语言运行时环境（而非由操作系统直接）执行的代码。 托管代码应用程序获得公共语言运行时服务，如自动垃圾收集、运行时类型检查和安全支持等。 这些服务帮助提供独立于平台和语言的、统一的托管代码应用程序行为。|  
|托管实例 (managed instance)|实用工具控制点监视的 SQL Server 实例。|  
|管理数据仓库|用来存储所收集数据的关系数据库。|  
|管理策略 (management policy)|用于管理 Certificate Lifecyle Manager (CLM) 配置文件模板中证书的工作流的定义。 管理策略定义谁执行工作流中的特定管理任务，并提供有关配置文件模板中证书的整个生存期的管理详细信息。|  
|Management Studio|Microsoft SQL Server 中随附的一套管理工具，用于配置和管理 Microsoft SQL Server 中的所有组件。|  
|手动故障转移 (manual failover)|在数据库镜像会话中，是指在负责将服务从主体数据库传输到镜像数据库（处于同步状态）的主体服务器仍在运行时数据库所有者启动的故障转移。|  
|多对多维度 (many-to-many dimension)|维度和度量值组之间的一种关系，在这种关系中，一个事实数据可与多个维度成员关联，而一个维度成员也可以与多个事实数据关联。 若要在维度与事实数据表之间定义这一关系，该维度应联接到中间事实数据表，反过来，此中间事实数据表应联接到已联接到此事实数据表的中间维度表。|  
|多对一关系 (many-to-one relationship)|这样的两个表之间的关系：一个表中的一个行可以与另一个表中的许多行相关。|  
|map|将数据与内存中的指定位置相关联。|  
|地图控件 (map control)|一个 JavaScript 控件，其中包含在您的网站上显示由 Bing Maps™ 支持的地图所需的对象、方法和事件。|  
|地图库 (map gallery)|一个地图库，其中所包含的地图来自位于面向报表创作环境的地图库文件夹中的报表。|  
|地图层 (map layer)|地图的子元素，每个地图层包括其地图成员和地图成员属性的元素。|  
|地图分辨率 (map resolution)|对于给定的地图比例尺，可以绘制地图功能的位置和形状的精度。 在大比例尺地图（如地图比例尺为 1:1）中，所显示的功能数比在小比例尺地图（如 1:1,000,000）上显示的功能数要多。|  
|地图图块 (map tile)|组合起来以形成一个 Bing 地图的许多 256 x 256 像素的图像之一。 地图图块包含地球在 Mercator 投影中的视图的一部分，并可能叠加了道路和文字，具体取决于 Bing 地图的样式。|  
|地图视区 (map viewport)|要在地图报表项中显示的地图区域。 例如，针对整个美国的地图可能嵌入在某一报表中，但只显示针对西北各州的区域。|  
|MAPI|一种消息传递体系结构，使多个应用程序可以跨各种硬件平台与多个消息传递系统进行交互。 MAPI 建立在组件对象模型 (COM) 基础之上。|  
|mapper|映射对象的组件。|  
|marker|标识数据点的可视指示器。 在地图报表中，标记是一个可视指示器，标识每个点在点层上的位置。|  
|标记地图 (marker map)|在每个位置（如城市）显示一个标记并且变化标记颜色、大小和类型的地图。|  
|市场篮分析|一种标准的数据挖掘算法，它分析一系列事务以预测用户最频繁地采购哪些商品。|  
|主数据 (master data)|关键的业务数据，如客户、产品、位置、员工和资产。 主数据通常分为四个组（人员、物、地点和概念）并可进一步分类。 例如，对于人员，可以进一步分类为客户、员工和销售人员。 对于事物，可进一步分为产品、部件、存储区和资产。 对于概念，可包括合同、担保和许可证。 最后，对于地点，可包括办公室地点和地理分区。|  
|主数据管理 (master data management)|为组织的主数据创建和维护一致和准确的列表所需的技术、工具和过程。|  
|主数据管理器|Master Data Services 应用程序中一个用于管理和访问主数据的组件。|  
|Master Data Services|一个主数据管理应用程序，可一致地定义和管理组织的关键数据实体。|  
|Master Data Services 配置管理器|一种用来创建和配置 Master Data Services 数据库、网站和 Web 应用程序的 SQL Server 配置管理器。|  
|master 数据库|记录 SQL Server 实例的所有系统级信息的系统数据库。|  
|主文件 (master file)|随早期的 SQL Server 版本一起安装的文件，用来存储 master、model 和 tempdb 系统数据库和事务日志以及 pubs 示例数据库和事务日志。|  
|主合并 (master merge)|将阴影索引与当前主索引结合起来以形成新的主索引的过程。|  
|主服务器 (master server)|分发作业并从多个服务器接收事件的服务器。|  
|具体化视图 (materialized view)|查询结果在其中缓存为具体表的视图，而具体表可以不时地从原始基表中进行更新。|  
|矩阵数据区域 (matrix data region)|报表布局中以可变分列格式显示数据的报表项。|  
|MBCS|混合宽度的字符集，其中某些字符包含 1 个以上的字节。 MBCS 用于日语、中文和韩语等语言，在这些语言中，256 个单字节字符集的可能值不足以表示所有可能的字符。|  
|MDS|一个主数据管理应用程序，可一致地定义和管理组织的关键数据实体。|  
|MDX|用来查询和操作多维对象（OLAP 多维数据集）中的数据的语言。|  
|度量值|多维数据集中的一组值，通常为数值并基于多维数据集的事实数据表中的某个列。 度量值是进行聚合和分析的中心值。|  
|度量值组 (measure group)|Analysis Services 多维数据集中一组相关的度量值。 这些度量值通常来自同一个事实数据表。|  
|介质簇 (media family)|备份操作写入到介质集所使用的备份设备的数据。 在只有一台备份设备的介质集中，只存在一个介质簇。 在条带介质集中，存在多个介质簇。 如果未镜像条带介质集，则每个设备对应于一个介质簇。 镜像介质集包含每个介质簇的两个到四个相同副本（称为镜像）。 将备份附加到介质集可扩展其介质簇。|  
|介质标头 (media header)|提供有关备份介质的信息的标签。|  
|介质集 (media set)|一个或多个备份操作使用恒定数量的备份设备写入的有序备份介质集合。|  
|中值 (median)|一组有序数值的中间值。 中值是通过选择最小值以使这组数值中至少有一半值不大于所选的值来确定的。 如果这组数值的个数为奇数，则中值对应于单个值。 如果这组数值的个数为偶数，则中值对应于两个中间值的和除以 2 所得的值。|  
|平均价公式 (median price formula)|计算最高价和最低价的平均值的公式。|  
|中值 (median value)|一组有序数值的中间值。 中值是通过选择最小值以使这组数值中至少有一半值不大于所选的值来确定的。 如果这组数值的个数为奇数，则中值对应于单个值。 如果这组数值的个数为偶数，则中值对应于两个中间值的和除以 2 所得的值。|  
|member|维度中的单个位置或项。 维度成员可以是用户定义的或预定义的，并且可具有与其相关联的属性。|  
|成员委托 (member delegation)|说明如何在接口之间映射接口成员的建模概念。|  
|成员表达式 (member expression)|返回成员的有效多维表达式 (MDX)。|  
|成员属性 (member property)|维度成员的特性。 维度成员属性可以是字母数字、布尔值或日期/时间数据类型，并且可以是用户定义的或预定义的。|  
|备注 (memo)|包含较长字符串的一种列，字符串长度通常大于 255 个字符。|  
|内存中介器 (memory broker)|在 SQL Server 中管理内存资源分配的软件组件。|  
|内存分配器 (memory clerk)|分配内存的内存管理组件。|  
|合并复制|一种允许站点对复制的数据进行自主更改，并在以后需要时合并更改并解决冲突的复制类型。|  
|合并逻辑删除 (merge tombstone)|通过合并冲突中的两个项来解决约束冲突时，会创建一个标记。|  
|消息号 (message number)|一个标识 SQL Server 错误消息的数字。|  
|消息队列|一种 Microsoft 技术，使在不同时间运行的应用程序能够跨异构网络和可能临时脱机的系统进行通信。|  
|消息类型 (message type)|Service Broker 消息的定义。 消息类型指定消息的名称，以及 Service Broker 对该类型的传入消息执行的验证类型。|  
|消息窗格 (Messages pane)|选项卡的一种，用来承载执行 TSQL 查询后从 SQL Server 返回的消息。|  
|消息处理应用程序编程接口 (Messaging Application Programming Interface)|一种消息传递体系结构，使多个应用程序可以跨各种硬件平台与多个消息传递系统进行交互。 MAPI 建立在组件对象模型 (COM) 基础之上。|  
|metadata|有关数据的属性或结构的信息（它们不是数据所包含的值的组成部分）。|  
|method|在面向对象的编程中，一个在调用时执行任务的命名代码块。|  
|Microsoft 消息队列 (Microsoft Message Queuing)|一种 Microsoft 技术，使在不同时间运行的应用程序能够跨异构网络和可能临时脱机的系统进行通信。|  
|Microsoft 顺序分析和聚类分析算法 (Microsoft Sequence Clustering algorithm)|综合了顺序分析和聚类分析的算法，它标识以相似方式排序的事件在一个序列中的聚类。 聚类可用于根据已知特性预测事件在一个序列中的可能排序方式。|  
|Microsoft SharePoint Foundation 使用情况数据导入|将使用情况日志导入日志数据库的 SharePoint Foundation 的默认计时器作业。|  
|Microsoft SharePoint Server|Microsoft 企业门户服务器的一个系列，它是在 Windows SharePoint Services 的基础上建立的，用于将 SharePoint 站点、信息和应用程序聚合到单个门户中。|  
|Microsoft SQL Server|Microsoft 关系数据库管理和分析系统的一个系列，用于实现电子商务、业务线和数据仓库解决方案。|  
|Microsoft SQL Server 2008 Express|Microsoft SQL Server 2008 的轻型可嵌入版本。|  
|Microsoft SQL Server 2008 Express with Advanced Services|Microsoft 关系数据库设计和管理系统，用于实现电子商务、业务线和数据仓库解决方案。|  
|Microsoft SQL Server 2008 Express with Tools|SQL Server Express 数据平台的一个免费、易于使用的版本，包括图形管理工具 SQL Server Management Studio (SMSS) Express。|  
|Microsoft SQL Server 联机丛书 (Microsoft SQL Server Books Online)|电子文档的集合，包括 Microsoft SQL Server 随附的完整文档。|  
|Microsoft SQL Server 商业智能 (Microsoft SQL Server Business Intelligence)|一种基于 Microsoft SQL Server 的数据基础结构和商业智能平台，由 Microsoft SQL Server Integration Services、关系引擎、Master Data Services、Reporting Services 和 Analysis Services 构成。|  
|Microsoft SQL Server Compact|Microsoft 关系数据库管理和分析系统，用于实现电子商务、业务线和数据仓库解决方案。|  
|Microsoft SQL Server Compact 3.5 for Devices|安装 SQL Server Compact 3.5 设备运行时组件的文件。|  
|Microsoft SQL Server Notification Services|一种 Microsoft SQL Server 外接程序，为构建和部署通知应用程序提供开发框架和宿主服务器。|  
|Microsoft SQL Server 播放捕获向导 (Microsoft SQL Server Playback Capture Wizard)|一种向导，它支持捕获与事件有关的信息以便以后分析。|  
|Microsoft SQL Server PowerPivot for Microsoft Excel|SQL Server 面向 Excel 的外接程序。|  
|Microsoft SQL Server PowerPivot for Microsoft SharePoint|一种 Microsoft SQL Server 技术，可针对发布到 SharePoint 的 PowerPivot 工作表提供查询处理和管理控制。|  
|Microsoft SQL Server Reporting Services|一种基于服务器的报表生成环境，它提供企业级的 Web 报表功能，从而使您可以创建从多个数据源提取数据的表，发布各种格式的表，以及集中管理安全性和订阅。|  
|Microsoft SQL Server Reporting Services 报表生成器 (Microsoft SQL Server Reporting Services Report Builder)|一种报表创作工具，它不但具备类似 Microsoft Office 的创作环境，并且还提供一些功能，例如新的迷你图、数据条和指示器数据可视化效果，能够将报表项保存为报表部件，用于创建地图的向导，聚合的聚合，以及对表达式的增强的支持。|  
|Microsoft SQL Server Service Broker|一种帮助开发人员生成安全的可缩放数据库应用程序的技术。|  
|Microsoft SQL Server System CLR Types|作为 SQL Server 2008 R2 功能包的一部分的一个独立包，包含用于在 SQL Server 中实现 geometry、geography 和 hierarchy ID 类型的组件。|  
|Microsoft 时序算法|使用线性回归决策树方法来分析与时间相关的数据（如每月销售数据或年利润）的算法。 它所发现的模式可用来预测将来步骤的值。|  
|中间件 (middleware)|介于两种或更多种软件之间并在这些软件之间翻译信息的软件。 中间件涵盖范围广泛的软件，通常介于应用程序与操作系统、网络操作系统或数据库管理系统之间。|  
|挖掘模型|包含数据挖掘进程定义和定型活动结果的对象。 例如，数据挖掘模型可以指定进程的输入、输出、算法以及其他属性，并保留在定型活动（如决策树）期间收集的信息。|  
|挖掘结构 (mining structure)|用于定义生成挖掘模型所基于的数据域的数据挖掘对象。|  
|次要刻度线 (minor tick mark)|与轴上的次要刻度单位对应的刻度线。|  
|镜像数据库 (mirror database)|在数据库镜像会话中，通常与主体数据库完全同步的数据库副本。|  
|镜像服务器 (mirror server)|在数据库镜像配置中，镜像数据库所在的服务器实例。 镜像服务器是镜像伙伴，该服务器的数据库副本当前是镜像数据库。 镜像服务器是热备用服务器。|  
|镜像介质集 (mirrored media set)|包含每个介质簇的两个到四个相同副本（镜像）的介质集。 还原操作对于每个介质簇只要求一个镜像，这使已损坏的介质卷能够被镜像中的对应卷替换。|  
|镜像 (mirroring)|将对读写数据库（主体数据库）所做的每次更新立即重新生成到驻留在单独的数据库引擎实例（镜像服务器）中的该数据库的只读镜像（镜像数据库）中。 在生产环境中，该镜像服务器位于其他的计算机上。 通过还原（但不恢复）主体数据库的完整备份可创建镜像数据库。|  
|model 数据库 (model database)|随 Microsoft SQL Server 一起安装的数据库，为新的用户数据库提供模板。 SQL Server 通过复制 model 数据库中的内容，然后将新数据库扩展未所需的大小，以创建数据库。|  
|模型依赖关系 (model dependency)|两个或更多个模型之间的一种关系，在这种关系中一个模型依赖于其他模型的信息。|  
|取模 (modulo)|其结果为除法运算的余数的算术运算。 例如，7 modulo 3 = 2，这是因为 17 除以 3，余数为 2。 取模运算在编程中使用。|  
|监视服务器 (monitor server)|在日志传送配置中，是指配置中的每个日志传送作业记录其历史记录和状态的服务器实例。 每个日志传送配置具有自己的专用监视服务器。|  
|msdb|存储计划的作业、警报以及备份/还原历史记录信息的数据库。|  
|MSMQ|一种 Microsoft 技术，使在不同时间运行的应用程序能够跨异构网络和可能临时脱机的系统进行通信。|  
|多基准差异备份 (multibase differential)|包含最后一次在非重复基准备份中备份的文件的差异备份。|  
|多字节字符集 (multibyte character set)|混合宽度的字符集，其中某些字符包含 1 个以上的字节。 MBCS 用于日语、中文和韩语等语言，在这些语言中，256 个单字节字符集的可能值不足以表示所有可能的字符。|  
|多播传递 (multicast delivery)|一种通知传递方法，它先对通知设置一次格式，然后将生成的消息发送给多个订阅服务器。|  
|多维表达式 (multidimensional expression)|用来查询和操作多维对象（OLAP 多维数据集）中的数据的语言。|  
|多维 OLAP|一种存储模式，使用专有多维结构存储分区的事实数据和聚合或维度。|  
|多维结构 (multidimensional structure)|一种数据库范例，将数据视为单元中包含维度和度量值的多维数据集。|  
|乘数 (multiplier)|在算术中，指示另一个数（被乘数）乘多少次的数字。|  
|多服务器管理|自动管理多个 SQL Server 实例的过程。|  
|多线程服务器应用程序 (multithreaded server application)|在单个进程内创建多个线程来同时服务多个用户请求的应用程序。|  
|多用户 (multiuser)|表示可以由多个用户使用的任何计算机系统。 尽管由多个用户共享的微型计算机可被视为多用户系统，但此术语通常保留用于可由多个用户通过通信工具或通过网络终端同时访问的计算机。|  
|互斥 (mutex)|一种编程方法，可确保一次只有一个程序或例程（通常通过使用信号量）能够访问某个资源（如内存分配、I/O 端口或文件）；信号量是在程序用来协调多个程序或例程的活动的标志。|  
|我的报表|一个个性化工作区。|  
|我的订阅 (My Subscriptions)|列出用户拥有的所有订阅的页面。|  
|命名缓存 (named cache)|内存中存储的可配置单元，具有与其关联的策略，可用于缓存群集中的所有缓存主机。|  
|命名实例 (named instance)|安装并给定了名称的 SQL Server，给定名称是为了与同一台计算机上的其他命名实例和默认实例区分开。|  
|命名管道 (named pipe)|内存的一部分，可被某个进程用来向另一个进程传递信息，因此一个进程的输出就是另一个进程的输入。 第二个进程可以是本地的（与第一个进程位于同一台计算机上），也可以是远程的（位于联网的计算机上）。|  
|命名更新 (named update)|一个自定义服务操作，所执行的操作与简单查询、更新、插入或删除操作不同。|  
|命名更新方法 (named update method)|一个自定义服务操作，所执行的操作与简单查询、更新、插入或删除操作不同。|  
|命名约定 (naming convention)|在给对象等命名时较为通用的标准。|  
|区域语言支持 API (national language support API)|32 位 Windows 中的一组系统函数，包含基于语言和文化习俗的信息。|  
|本机编译器 (native compiler)|为正在运行它的计算机生成机器码的编译器，与交叉编译器不同，后者为另一种类型的计算机生成代码。 大多数编译器为本机编译器。|  
|本机格式 (native format)|保持数据库的本机数据类型的本机格式。 当使用不包含任何扩展/双字节字符集 (DBCS) 字符的数据文件在多个 Microsoft SQL Server 实例之间大容量传输数据时，建议使用本机格式。|  
|自然层次结构 (natural hierarchy)|一种层次结构，其中每个级别的成员都与下一个级别的成员之间存在一对多的关系。|  
|针尖 (needle cap)|可应用于径向仪表的两个外观属性之一。|  
|嵌套查询 (nested query)|包含一个或多个子查询的 SELECT 语句。|  
|网络库 (Net-Library)|将 SQL Server 客户端软件和数据库引擎与网络 API 隔离的 SQL Server 通信组件。|  
|网络软件 (network software)|使各组计算机能够相互通信的软件，包括帮助连接到网络或参与网络的组件。|  
|换行符 (new line character)|一个控制字符，导致显示屏上的光标或打印机上的打印机构移到下一行的开头。|  
|nickname|与合并复制系统表一起使用时，是指已知具有指定级别的更新数据的另一台订阅服务器的名称。|  
|niladic 函数|没有任何输入参数的函数。|  
|NLS API|32 位 Windows 中的一组系统函数，包含基于语言和文化习俗的信息。|  
|节点|同步提供程序及其关联的副本。|  
|干扰词 (noise word)|诸如“的”或“此”的字词，它们对于搜索几乎没用，或者爬网程序在创建索引时应忽略它们。|  
|非聚集索引 (nonclustered index)|一种索引键值的逻辑顺序不同于表中相应行的物理顺序的基于 B 树的索引。 此索引包含指向表数据存储位置的行定位器。|  
|非包含数据库 (non-contained database)|一种 SQL Server 数据库，它在其中安装了数据库的 SQL Server 数据库引擎实例中存储数据库设置和元数据，并要求登录 master 数据库以进行身份验证。|  
|非键索引列 (Nonkey index column)|非聚集索引中不作为键列参与的列。 相反，该列存储在索引的叶级别，与键列一起使用来覆盖一个或多个查询。|  
|非叶成员 (nonleaf member)|具有一个或多个后代的成员。|  
|不可为 Null 的参数 (nonnullable parameter)|不能采用 NULL 值的参数。|  
|不可重复读 (nonrepeatable read)|当一个事务多次读取同一行并且另一事务在读取之间修改了该行时出现的不一致性。|  
|规范化规则 (normalization rule)|一个设计规则，可将数据冗余降至最低，并得到这样一个数据库：数据库引擎和应用程序软件可以在此数据库中轻松地强制实现完整性。|  
|通知|发送给系统的用户或管理员的消息或通知。 接收方可以是用户，也可以是自动消息管理器。|  
|Notification Services|一种 Microsoft SQL Server 外接程序，为构建和部署通知应用程序提供开发框架和宿主服务器。|  
|NSControl|一个命令提示实用工具，用于管理 Notification Services 实例和应用程序。|  
|NUL|一种由操作系统识别的“设备”，可像物理输出设备（如打印机）一样寻址，但放弃发送给它的任何信息。|  
|Null|一个指示缺少数据或数据未知的值。|  
|Null 键 (null key)|在键列中遇到的 Null 值。|  
|空指针 (null pointer)|一个不指向任何内容的指针：通常为标准化的内存地址（例如 0）。 空指针通常标记线性指针序列的最后一个指针，或指示数据搜索操作将返回空值。|  
|为 Null 性 (nullability)|列、参数或变量的属性，指定其是否允许 Null 数据值。|  
|可为 Null 的属性 (nullable property)|控制字段是否可以具有 NULL 值的属性。|  
|NUMA 节点 (NUMA node)|一组有自己的内存并可能有自己的 I/O 通道的处理器。|  
|数值数组 (numeric array)|由键的集合和值的集合构成的数组，其中的每个键都与一个值相关联。 值可以是任何类型，但键必须为数值。|  
|数值表达式 (numeric expression)|计算结果为数字的任何表达式。 该表达式可以是变量、常量、函数和运算符的任意组合。|  
|对象标识符 (object identifier)|唯一标识对象类或特性的数字。 对象标识符 (OID) 在行业范围的全局层次结构中进行组织。 对象标识符表示为带点的十进制字符串（如 1.2.3.4），每个圆点表示层次结构中的一个新分支。 国家/地区注册机构向个人或组织颁发根对象标识符，后者管理分组在其根对象标识符下的层次结构。|  
|对象生存期 (object lifetime)|缓存对象位于缓存中且可供缓存客户端检索的时间跨度。 当对象的生存期结束时，此对象将到期。 缓存客户端无法检索到期对象，但到期对象保留在缓存主机的内存中，直至被逐出。 指定为生存时间 (TTL)。|  
|对象变量 (object variable)|包含对象引用的变量。|  
|ODS 库 (ODS library)|使应用程序成为服务器的一组函数。 ODS 库调用响应来自客户端/服务器网络中的客户端的请求。 它还管理客户端与服务器之间的通信和数据。 ODS 库遵循表格格式数据流 (TDS) 协议。|  
|Office 文件验证 (Office File Validation)|一种安全功能，它线验证文件，然后允许应用程序加载文件，以防止出现文件格式漏洞。|  
|脱机还原 (offline restore)|当数据库处于脱机状态时执行的还原。|  
|OLAP|使用多维结构快速访问数据以便进行分析的技术。 OLAP 的源数据通常存储在关系数据库的数据仓库中。|  
|OLAP 多维数据集 (OLAP cube)|一个经过组织和汇总，形成由一组维度和度量值定义的多维结构的数据集。|  
|OLAP 数据库 (OLAP database)|一种关系数据库系统，可处理的查询比标准关系数据库所处理的查询更复杂，处理方式为：对数据进行多维度访问（按多个不同条件查看数据）、使用密集计算功能以及采用专用的索引编制方法。|  
|一次性密码 (one-time password)|由特殊的密码生成软件或硬件令牌生成的密码，只可使用一次。|  
|联机分析处理 (online analytical processing)|使用多维结构快速访问数据以便进行分析的技术。 OLAP 的源数据通常存储在关系数据库的数据仓库中。|  
|联机还原 (online restore)|一种可在数据库保持联机时还原一个或多个辅助文件组、属于辅助文件组的文件或页面的还原。 联机还原仅可用于 SQL Server 2005 Enterprise Edition（包括 Evaluation Edition 和 Developer Edition）中。|  
|开放式数据服务库 (Open Data Services library)|使应用程序成为服务器的一组函数。 ODS 库调用响应来自客户端/服务器网络中的客户端的请求。 它还管理客户端与服务器之间的通信和数据。 ODS 库遵循表格格式数据流 (TDS) 协议。|  
|操作代码 (operation code)|机器语言或汇编语言指令的一部分，它指定指令的类型以及要对其执行操作的数据结构。|  
|运算符后的表达式|StreamInsight 服务器在处理已应用查询的事件时计划使用的查询原子单元。 示例包括 SELECT、PROJECT、AGGREGATE、UNION、TOP K 和 JOIN。 运算符是完全可组合的，并且具有特定数量的输入和输出。 请参阅其他术语：查询 (query)、查询模板 (query template)、可组合 (composable)。|  
|运算符后的表达式|表达式中用于指定要执行的计算类型的符号， 其中包括数学、比较、逻辑和引用运算符。|  
|开放式并发 (optimistic concurrency)|一种通过使用缓存对象的版本信息管理并发的方法。 因为对对象的每个更新都更改其版本号，所以，使用版本信息将阻止更新覆盖其他人的更改。|  
|优化同步 (optimize synchronization)|合并复制中的选项，允许您在确定最近更改是否导致了某一行移入或移出发布到订阅服务器的分区时尽量降低网络流量。|  
|有序集 (ordered set)|以特定顺序返回的成员集。|  
|起始对象 (origin object)|存储库中作为方向关系起点的对象。|  
|OTP|由特殊的密码生成软件或硬件令牌生成的密码，只可使用一次。|  
|外部联接|一种联接，包括联接表中满足搜索条件的所有行，甚至包括在另一联接表中没有匹配行的一个表中的行。|  
|输出适配器 (output adapter)|一种适配器，它接收由服务器处理的事件，将事件转换为输出设备（数据库、文本文件、PDA 或其他设备）所需的格式并将数据发送到该设备。|  
|输出列 (output column)|在 SQL Server Integration Services 中，指的是源添加到数据流并且可用作数据流中下一数据流组件的输入列的列。|  
|输出流 (output stream)|离开计算机系统并且与特定任务或目标相关联的一种信息流。|  
|过度拟合 (overfitting)|在数据中的随机变体被错误划分为重要模式类别时数据挖掘中的问题。 在数据集太小以致无法表示真实情况时常常会发生过度拟合。|  
|所有权链 (ownership chain)|对象引用其他对象时，调用对象和被调用对象由同一个用户拥有。 SQL Server 使用所有权链来确定如何检查权限。|  
|包|作为一个单元运行的控件流和数据流元素的集合。|  
|数据包|从一台计算机或设备传输到网络上另一台计算机或设备的信息单位。|  
|填充索引 (Pad index)|指定中间级索引页的可用空间的选项。|  
|填充 (padding)|在数据存储中，将一个或多个位（通常是零）添加到数据块以便填充它、将实际数据位强制为某个位置或者禁止数据重复已具有既有含义（例如嵌入命令）的位模式的过程。|  
|页|用更小的数据子集返回查询结果，这使用户可通过查看数据“页”来在结果集中导航。|  
|页|在虚拟存储系统中，一个固定长度的连续虚拟地址块，在分页操作过程中它作为一个单元在内存和磁盘之间来回复制。|  
|页面错误 (page fault)|在软件尝试读取或写入标记为“不存在”的虚拟内存位置时发生的中断。|  
|页面还原 (page restore)|还原一个或多个数据页的操作。 页面还原用于修复隔离的损坏页。|  
|pager|一种口袋大小的无线电子设备，它使用无线信号记录传入的电话号码或短信。 某些寻呼机也允许用户发送消息。|  
|分页系统 (paging system)|一种允许用户在超出范围时发送和接收消息的系统。|  
|PAL|用来保护发布服务器的主要机制。 它包含已获得发布访问权限的登录名、帐户和组的一个列表。|  
|并行执行 (parallel execution)|两个或多个例程或程序看似同时发生的执行。 并行执行可在单个进程上实现，或者通过使用时间共享技术（例如将程序划分为不同任务或线程的执行）或通过使用多个处理器实现。|  
|并行处理 (parallel processing)|只能在包含两个或多个同时运行的处理器的计算机上运行的处理方法。 在将某一任务分发到可用处理器的方式上，并行处理不同于多处理。 在多处理中，一个进程可以划分为多个连续的块，一个处理器管理对数据库的访问，另一个处理器对数据进行分析，第三个处理器处理向屏幕上的图形输出。 使用执行并行处理的系统的程序员必须找到划分任务的方法，以便或多或少在可用处理器之间平均分配任务。|  
|参数化查询 (parameterized query)|通过参数接受输入值的查询。|  
|参数化报表 (parameterized report)|通过参数接受输入值的发布报表。|  
|参数化行筛选器 (parameterized row filter)|可以在合并复制中使用的行筛选器，通过它可以基于系统函数或用户定义的函数（例如 SUSER_SNAME()）限制复制到订阅服务器的数据。|  
|部分备份 (partial backup)|主文件组、每个读-写文件组和任意指定的可选文件中所有数据的备份。 只读数据库的部分备份仅包含主文件组。|  
|数据库部分还原 (partial database restore)|只还原数据库的一部分，包括它的主文件组，可能还包括一个或多个辅助文件组。 其他文件组保持永久脱机，尽管可以在以后还原它们。|  
|部分差异备份 (partial differential backup)|相对于上一次部分备份（基准备份）有差异的部分备份。 对于只读数据库，部分差异备份仅包含主文件组。|  
|参与者 (participant)|同步提供程序及其关联的副本。|  
|小品词|非常小的部分；不可分的对象。|  
|分区函数|一种函数，它定义如何根据某些列（称为分区依据列）的值将已分区表或索引的行分布到一组分区中。|  
|分区方案 (partition scheme)|将分区函数的分区映射到一组文件组的数据库对象。|  
|已分区索引 (partitioned index)|按分区方案生成的索引，其数据水平划分为多个单元，这些单元可以分布到数据库中的多个文件组中。|  
|分区快照 (partitioned snapshot)|在合并复制中，仅包含单个分区中的数据的快照。|  
|已分区表 (partitioned table)|按分区方案生成的表，其数据水平划分为多个单元，这些单元可以分布到数据库中的多个文件组中。|  
|分区表并行度 (partitioned table parallelism)|针对从已分区对象选择的查询的并行执行策略。 作为执行策略的一部分，查询处理器会确定查询所需的表分区，以及要分配给每个分区的线程比例。 在大多数情况下，查询处理器会为每个分区分配数量相等或几乎相等的线程，然后在这些分区中并行地执行查询。|  
|partitioning|使用多个较小的表替换某个表的过程。|  
|分区依据列 (partitioning column)|分区函数对表或索引进行分区时所使用的表或索引列。|  
|伙伴 (partner)|数据库镜像中的主体服务器或镜像服务器。|  
|传递顺序 (pass order)|针对多维数据集中的计算成员、自定义成员、自定义汇总公式和计算单元的评估（从最高到最低的计算传递数）和计算顺序（从最低到最高的计算传递数）。|  
|通行短语 (pass phrase)|用于获取对网络、程序或数据的访问权限的单词或其他文本的序列。 通常，通行短语越长，安全性就越高。|  
|传递查询 (pass-through query)|用于将命令直接发送到 ODBC 数据库服务器的特定于 SQL 的查询。|  
|传递语句 (pass-through statement)|没有修改或延迟而直接传递到源数据库的 SELECT 语句。|  
|密码策略 (password policy)|定义组策略对象 (GPO) 的密码要求的策略设置集合。|  
|密码提供程序 (password provider)|生成和验证一次性密码以对用户进行身份验证的组件。|  
|path|将一个数据流组件的输出连接到另一个数据流组件的输入的数据流元素。|  
|PBM|返回 SQL Server 中有关值、对象和设置的服务器状态信息的一组内置函数。 基于策略的管理允许数据库管理员声明系统的预期状态并且检查系统是否与该状态兼容。|  
|对等复制|一种事务复制。 与只读事务复制和具有更新订阅的事务复制相反，对等复制拓扑中节点之间的关系是对等关系而不是层级关系，每个节点均包含完全相同的架构和数据。|  
|性能工具 (performance tools)|可用于评估解决方案的性能的工具。 性能工具可具有不同的用途；某些工具设计为评估端到端性能，其他一些工具则着重于评估解决方案的某一特定方面的性能。|  
|持久化计算列 (persisted computed column)|物理存储的表的计算列，计算中涉及的任何其他列更改时，其值即更新。 在某一计算列是确定性的、但不精确时，将持久化属性应用于该列将允许对其创建索引。|  
|持久性数据库 (persistence database)|一种持久性存储区，它存储 SQL Server 数据库中的工作流实例状态和工作流实例元数据。|  
|透视 (perspective)|多维数据集的用户定义的子集，而视图是表的用户定义的子集和关系数据库中的列。|  
|保守式并发 (pessimistic concurrency)|一种管理并发的方法，它通过使用锁技术来阻止其他客户端同时更新相同的对象。|  
|虚拟 (phantom)|指的是在另一个任务（该任务尚未提交事务）先前读取的行范围中插入一个新行或删除现有行。|  
|PHP|一种开放源脚本语言，它可以嵌入在 HTML 文档中以便对 Web 服务器执行交互功能。 它通常用于 Web 开发。|  
|PHP:Hypertext 预处理器 (PHP:Hypertext Preprocessor)|一种开放源脚本语言，它可以嵌入在 HTML 文档中以便对 Web 服务器执行交互功能。 它通常用于 Web 开发。|  
|物理名称 (physical name)|文件或镜像文件所在的路径的名称。 默认值是 Master.dat 文件的路径，后随该文件的逻辑名称的前八个字符。|  
|物理存储 (physical storage)|系统中的 RAM 内存量，与虚拟内存相反。|  
|拾取文件夹 (Pickup folder)|从中拾取消息的目录。|  
|段落还原 (piecemeal restore)|分阶段还原数据库的组合还原，每个阶段对应于一个还原序列。 初始序列将主文件组中的文件以及其他文件（可选）还原到恢复模式支持的任何时间点并且使数据库处于联机状态。 后续还原序列使其余文件处于与数据库一致的时间点上并且使它们处于联机状态。|  
|PIN|一种唯一且保密的标识码，它类似于分配给某一授权用户的密码，并且用于通过电子设备访问个人信息或资产。|  
|PInvoke|公共语言运行时提供的功能，它使托管代码能够调用非托管本机 DLL 入口点。|  
|pivot|通过将表达式某一列中的唯一值转换为输出中的多个列来旋转表值表达式，并在必要时对最终输出中所需的任何其余列值执行聚合。|  
|先导货币 (pivot currency)|在比率度量值组中为其输入汇率的货币。|  
|数据透视表 (PivotTable)|Microsoft Excel 或 Access 中的一种交互技术，可显示来自某一列表或数据库的相同数据的动态视图。|  
|PL/SQL|Oracle 的数据操作语言，它允许 SQL 语句的按顺序或分组的执行，并且通常用于操作 Oracle 数据库中的数据。 该语法类似于 Ada 编程语言。|  
|占位符项 (placeholder item)|一种虚拟的地址、指令或计算机的其他数据馈送，仅用于满足规定的条件并且不影响用于解决问题的操作。|  
|明文|未加密或已解密形式的数据。|  
|计划指南 (plan guide)|一个 SQL Server 模块，可将查询提示附加到已部署应用程序中的查询，而无需直接修改查询。|  
|平面 (planar)|在计算机图形中，处于平面内。|  
|平台调用 (Platform Invoke)|公共语言运行时提供的功能，它使托管代码能够调用非托管本机 DLL 入口点。|  
|平台层 (platform layer)|包括支付服务层的物理服务器和服务的层。 平台层由许多 SQL Server 实例构成，每个实例都由 SQL Azure 结构进行管理。|  
|PMML|一种基于 XML 的语言，可在符合的供应商应用程序之间实现定义的预测模型的共享。|  
|点数图 (Point and Figure chart)|绘制日常价格变动而不考虑时间通道的一种图表。|  
|点深度 (point depth)|三维图表区域中显示的数据点的深度。|  
|点事件 (point event)|在单个时间点处发生的事件。 对于此类事件，只需要开始时间。 CEP 服务器通过向开始时间中添加时钟周期（基础时间数据类型的最小时间单位）来推断有效的结束时间，以设置事件的有效时间间隔。 点事件只对此单个瞬间有效。|  
|点事件模型 (point event model)|点事件的事件模型。|  
|点层 (point layer)|地图报表中的一种层，它将空间数据显示为点（例如，指示城市的点或相关点）。|  
|指针 (pointer)|指示在报表上按某个比例显示的单个值的针、标记或图条。|  
|时点恢复 (point-in-time recovery)|仅恢复日志备份中特定时间点之前提交的事务而不是恢复整个备份的过程。|  
|有害消息 (poison message)|含有应用程序无法成功处理的信息的消息。 有害的消息不是损坏的消息，而且可能是有效的请求。|  
|策略模块 (policy module)|一种证书服务组件，它确定某一证书请求是否应自动核准、拒绝或标记为待定。|  
|基于策略的管理 (policy-based management)|返回 SQL Server 中有关值、对象和设置的服务器状态信息的一组内置函数。 基于策略的管理允许数据库管理员声明系统的预期状态并且检查系统是否与该状态兼容。|  
|轮询器 (poller)|监视其他组件的状态的组件或接口。 它通过反复轮询其他组件以提供其当前状态，执行此功能。|  
|轮询|定期确定一组设备中每个设备的状态的过程，以便活动程序可以处理每个设备生成的事件，例如是否按下了某一鼠标按钮或者新数据是否是在某一串行端口上提供的。 这可能与事件驱动的处理相反，在后者中，操作系统通过中断或消息（而不是不得不依次检查各设备），针对发生的事件对程序或例程发出提醒。|  
|轮询查询 (polling query)|一种单独查询，Analysis Services 使用该查询的返回值来确定是否已对表或其他关系对象进行了更改。|  
|多边形层 (polygon layer)|地图报表中的层，它将空间数据显示为面积（例如，指示国家/地区之类的地理区域的面积）的层。|  
|填充 (population)|跨内容编译和维护某一索引的过程。|  
|定位更新 (positioned update)|对游标当前位置处的行执行的更新、插入或删除操作。|  
|PowerPivot|SQL Server 面向 Excel 的外接程序。|  
|PowerPivot 数据 (PowerPivot data)|通过 Microsoft SQL Server PowerPivot for Microsoft Excel 创建和嵌入的 SQL Server Analysis Services 多维数据集。|  
|PowerPivot for SharePoint|一种 Microsoft SQL Server 技术，可针对发布到 SharePoint 的 PowerPivot 工作表提供查询处理和管理控制。|  
|PowerPivot 服务|Analysis Services SharePoint 集成功能的中间层服务，可用于分配请求、监视服务器可用性和运行状况以及与场中的其他服务通信。|  
|PowerPivot 服务应用程序 (PowerPivot service application)|PowerPivot 服务的一种特定配置。|  
|PowerPivot Web 服务|一种 Web 服务，它执行请求重定向，以便处理定向到场外的 PowerPivot 引擎服务实例的请求。|  
|PowerPivot 工作簿 (PowerPivot workbook)|包含 PowerPivot 数据的 Excel 2010 工作簿。|  
|基于 PowerShell 的缓存管理工具 (PowerShell-based cache administration tool)|针对 Windows Server AppFabric 的专用管理工具。 通过超过 130 个标准命令行工具，这一新的以管理为中心的脚本语言帮助您实现更多的控制和更高的生产率。|  
|优先约束 (precedence constraint)|控件流元素，它将任务和容器连接到序列工作流中。|  
|预计算分区 (precomputed partition)|一种性能优化方法，可用于已筛选的合并发布。|  
|可预测列 (predictable column)|算法将基于输入列的值围绕这些列生成一个模型的数据挖掘列。 除了充当输出列之外，可预测列还可用作同一挖掘结构内其他可预测列的输入。|  
|prediction|一种数据挖掘方法，分析现有数据，并使用结果来预测新记录的属性值或现有记录中缺少的属性值。 例如，现有信用申请数据可用于预测新申请的信用风险。|  
|预测计算器|一种新报表，它基于逻辑回归分析并且与该算法计算出的分数一起显示各相关因素。 该报表既作为可帮助您输入数据和进行可能结果的计算的工作表提供，也作为执行同样任务的打印的报表提供。|  
|前缀字符|1 到 4 个字节的集合，用于为本机格式大容量复制数据文件中每个数据字段添加前缀。|  
|前缀长度|bcp 本机格式数据文件中每个非字符字段前的前缀字符数。|  
|必备知识 (prerequisite knowledge)|处理变更或变更批时目标提供程序必须具有的最少知识。|  
|演示模型 (presentation model)|一种数据模型，它聚合来自数据访问层中的多个实体的数据。 它用于避免直接向客户端项目公开实体。|  
|主数据库 (primary database)|包含一个应用程序处于活动状态的数据的读写数据库。|  
|主维度表 (primary dimension table)|在数据仓库中的雪花型架构中，直接与事实数据表相关并通常联接到事实数据表的维度表。|  
|主 DPM 服务器 (primary DPM server)|保护文件或应用程序数据源的一种 DPM 服务器。|  
|主键 (primary key)|唯一标识表中每个记录的一个或多个字段。 与许可证牌照号标识一辆汽车的方式相同，主键唯一标识一条记录。|  
|主要保护 (primary protection)|一种保护类型，其中，受保护服务器上的数据直接由主 DPM 服务器进行保护。|  
|主服务器 (primary server)|日志传送配置中主数据库所在的服务器实例。|  
|主表 (primary table)|一对多关系中的两个相关表中的一方。 主表应具有主键并且每个记录应该是唯一的。|  
|主体数据库 (principal database)|数据库镜像中的一种读-写数据库，其事务日志将持续不断地发送到镜像服务器，而镜像服务器将日志还原到镜像数据库。|  
|主体服务器 (principal server)|在数据库镜像中，是指当前作为主体数据库的数据库所属于的伙伴。|  
|优先级提升 (priority boost)|一种高级选项，它指定 Microsoft® SQL Server™ 是否应该以比同一计算机上其他进程更高的 Microsoft Windows NT® 计划优先级运行。|  
|私钥 (private key)|用于公钥算法的密钥对中机密的那一半。 私钥通常用于解密对称会话密钥、对数据进行数字签名或解密已经用相应的公钥加密的数据。|  
|主动缓存|多维数据集中管理数据过时的一种机制，通过这种机制，MOLAP 存储中的对象在缓存中自动更新和处理，查询则重定向到 ROLAP 存储。|  
|过程缓存 (procedure cache)|SQL Server 内存池的一部分，用于存储 Transact-SQL 批处理、存储过程和触发器的执行计划。|  
|配置文件模板 (profile template)|所有 Certificate Lifecycle Manager (CLM) 管理活动的核心。 配置文件模板提供单个管理单元，其中包括管理用户社区在证书的整个生命周期中可能需要的多个证书所需的所有信息。 配置文件模板还包含与这些证书的最终位置有关的信息，证书可以是基于软件的（即，存储于本地计算机上）或基于硬件的（存储于智能卡上）。 配置文件模板不能既包含基于软件的证书，又包含基于智能卡的证书。|  
|利润图|一种图形，显示与使用不同的数据模型相关联的理论上的利润增长。|  
|可编程 (programmable)|能够接受用于执行任务或操作的指令。 能够可编程是计算机的特征。|  
|属性页|在界面中显示对象的相关信息的对话框。|  
|property|用于定义对象的状态、外观或值的对象的属性或特征。|  
|属性映射 (property mapping)|包元素的变量和属性之间的映射。|  
|属性页 (property page)|表示为属性表的选项卡式页的一组属性。|  
|受保护的计算机 (protected computer)|包含是保护组成员的数据源的计算机。|  
|受保护的成员 (protected member)|保护组内的数据源。|  
|protocol|使计算机之间可以交换信息的一组标准的格式和过程。|  
|provider|提供数据库访问的进程内动态链接库 (DLL)。|  
|provider|允许副本与其他副本同步其数据的软件组件。|  
|提供程序对象 (provider object)|属于 Oracle Provider for SQL Server 之类的提供程序的对象。|  
|邻近搜索 (proximity search)|搜索那些指定的词彼此接近的情况的全文查询。|  
|代理帐户 (proxy account)|一种用于为没有执行某些操作的权限但需要执行这些操作的用户提供额外权限的帐户。|  
|公钥 (public key)|用于公钥算法的密钥对中非机密的那一半。 通常在对会话密钥进行加密、验证数字签名或加密可使用相应的私钥解密的数据时，使用公钥。|  
|publication|一个数据库中的一个或多个项目的集合。|  
|发布访问列表|用来保护发布服务器的主要机制。 它包含已获得发布访问权限的登录名、帐户和组的一个列表。|  
|发布数据库 (publication database)|发布服务器上的数据库，其中的数据和数据库对象标记为要复制并传播到订阅服务器。|  
|发布保持期 (publication retention period)|在合并复制中，订阅可以保持不同步状态的时间。|  
|已发布数据 (published data)|发布服务器上已复制的数据。|  
|Publisher|使数据可供复制到其他服务器的一种服务器。 发布服务器还检测更改的数据并且维护与站点上的所有发布有关的信息。|  
|publisher database|使数据可供复制到其他服务器的一种服务器。 发布服务器还检测更改的数据并且维护与站点上的所有发布有关的信息。|  
|发布服务器 (publishing server)|运行 Analysis Services 实例的服务器，用于存储一个或多个链接多维数据集的源多维数据集。|  
|发布表 (publishing table)|发布服务器上的表，其中的数据标记为要复制，是发布的一部分。|  
|pull|从网络服务器检索数据的过程。|  
|请求复制 (pull replication)|在目标调用的复制。|  
|请求订阅 (pull subscription)|在订阅服务器上创建和管理的订阅。 该订阅的分发代理或合并代理在订阅服务器上运行。|  
|纯日志备份 (pure log backup)|只包含某个时间段的事务日志，不包含任何批量更改的备份。|  
|push|将数据发送到网络服务器的过程。|  
|推送复制 (push replication)|在源调用的复制。|  
|推送订阅 (push subscription)|在发布服务器上创建和管理的订阅。|  
|限定的组件 (qualified component)|通过“组件类别 GUID，字符串限定符）对间接对 MSI 数据库中的组件进行标识（而非由组件标识符直接标识）的一种方法。|  
|限定符 (Qualifier)|包含描述类、实例、属性、方法或参数的信息的修饰符。 限定符由公共信息模型 (CIM)、CIM 对象管理器和开发人员定义。|  
|限定符特色信息 (qualifier flavor)|提供与限定符有关的附加信息的标志，例如派生类或实例能否重写限定符的原始值。|  
|量程 (quantum)|给定线程在多任务操作系统中执行时的一段短暂时间。 在它根据具有相同优先级的其他线程重新计划前，执行多任务。 以前称为“时间段”。|  
|query|连续运行在 StreamInsight 服务器中的查询模板的实例，该服务器处理自该查询绑定到的输入适配器实例接收的事件，并将处理过的事件发送到该查询绑定到的输出适配器实例。|  
|查询绑定器 (query binder)|将现有 StreamInsight 查询模板绑定到特定输入和输出适配器的一种对象。|  
|查询绑定 (query binding)|将输入适配器的实例和输出适配器的实例绑定到查询模板的实例的过程。|  
|查询设计器|一种工具，它帮助用户创建指定用户希望出现在报表数据集中的数据的查询命令。|  
|查询调控器 (query governor)|一个可用于使长时间运行的查询无法占用系统资源的配置选项。|  
|查询提示 (query hint)|一种提示，它指定应在整个查询中使用的指示的提示。 查询提示影响到语句中的所有运算符。|  
|查询优化器 (query optimizer)|负责为语句生成高效执行计划的数据库引擎组件。|  
|查询模板 (query template)|构成查询的基本单位。 查询模板定义连续分析和处理提交给 StreamInsight 服务器的事件以及从该服务器中发出的事件所需的业务逻辑。|  
|问题模板 (question template)|描述一组问题的结构，这些问题可以使用某种特定关系或一组关系来提出。|  
|队列读取器代理|一种可执行程序，它读取队列中来自订阅服务器的更改并且将这些更改传递到发布服务器。|  
|仲裁|在具有见证服务器的数据库镜像会话中，是指当前可彼此通信的服务器仲裁谁拥有主体服务器的角色的一种关系。|  
|quoted identifier|数据库中的一种对象，该对象由于名称不符合常规标识符的格式设置规则，因此必须使用特殊字符（分隔符）。|  
|RAD|一种构建计算机系统的方法，其中，系统按段进行编程和实施，而不是等到完成整个项目后进行实施。 由编程人员 James Martin 开发，RAD 使用如 CASE 和 Visual 编程等工具。|  
|不齐整层次结构 (ragged hierarchy)|一种层次结构，其中一个或多个分支中的一个或多个级别不包含成员。|  
|range|应用同一时钟向量的一组连续的项标识符。 范围用起点、终点以及应用于起点和终点之间的所有 ID 的时钟向量表示。|  
|范围分区 (range partition)|由数据的特定且可自定义的范围定义的一种表分区。|  
|按范围分区 (range partitioning)|对表或索引进行分区的方法，它通过指定分区来保存单个分区依据列中值在一定范围内的行。|  
|范围查询 (range query)|指定值的范围（例如，从 10 到 100 的所有行）作为搜索条件的一部分的查询。|  
|排名函数 (ranking function)|根据每一行在结果集的窗口（分区）中的位置返回有关该行在窗口中的排名信息的函数。|  
|快速应用程序开发 (rapid application development)|一种构建计算机系统的方法，其中，系统按段进行编程和实施，而不是等到完成整个项目后进行实施。 由编程人员 James Martin 开发，RAD 使用如 CASE 和 Visual 编程等工具。|  
|变动率 (rate of change)|相比于历史记录数据的价格变动率。 变动率是针对当前价格之前的一段日期进行计算的。 输出为百分比值。|  
|原始目标适配器 (raw destination adapter)|将原始数据写入文件的 SSIS 目标。|  
|原始文件 (raw file)|用于快速读取和写入数据的本机格式。|  
|原始文件目标|将原始数据写入文件的 SSIS 目标。|  
|原始文件源|从文件中读取原始数据的 SSIS 源。|  
|原始源适配器 (raw source adapter)|从文件中读取原始数据的 SSIS 源。|  
|RDA|一种服务，它为智能设备应用程序访问（请求）远程 SQL Server 数据库表和本地 SQL Server Mobile Edition 数据库表，以及向/从这些数据库表中发送（推送）数据提供了一种简单的方式。 还可以使用 RDA 在运行 SQL Server 的服务器上发出 SQL 命令。|  
|RDBMS|按关系模型指定的方式将数据组织为相关行和列的数据库系统。|  
|RDL|描述报表的布局和查询信息的一组指令。 RDL 由 XML 元素组成，这些元素符合为 Reporting Services 创建的 XML 语法。|  
|RDL 沙盒处理 (RDL Sandboxing)|通过这一功能，您可以在多个租户共享报表服务器的单个 Web 场的情况下检测到和限制单个用户使用的特定类型的资源。|  
|记录集 (record set)|由一组数据库记录组成的数据结构。 它可以从基表中生成，也可以从对表执行的查询中生成。|  
|recover|重新回到一种稳定的情况下。 计算机用户可以使用程序搜索和挽回存储设备中保留的任何信息，以恢复丢失或损坏的数据。 当出现的问题（如数据库管理程序异常终止）损坏数据库的完整性后，可以通过还原其完整性来恢复数据库。|  
|recovery|使数据库进入事务一致状态的数据库启动阶段。 恢复可能包括前滚日志记录中的所有事务（重做阶段）和回滚未提交的事务（撤消阶段），具体取决于关闭数据库的方式。|  
|恢复分支 (recovery branch)|共享同一个恢复分支 GUID 的一组 LSN。 创建数据库或用 RESTORE WITH RECOVERY 生成恢复分叉之后，会生成新的恢复分支。 此时可能出现多分支恢复路径，其中包括涵盖两个或多个恢复分叉点的 LSN 范围。|  
|恢复分叉点 (recovery fork point)|每次执行 RESTORE WITH RECOVERY 操作时开始一个新的恢复分支的点 (LSN,GUID)。 每个恢复分叉都确定了恢复分支之间的父子关系。 如果将数据库恢复到更早的时间点并从该点开始使用数据库，则恢复分叉点会开始一个新的恢复路径。|  
|恢复间隔|数据库引擎恢复数据库所需的最长时间。|  
|恢复模式|控制数据库备份和还原操作基本行为的数据库属性。 例如，恢复模式控制如何记录事务，事务日志是否需要备份，以及可以使用哪些类型的还原操作。|  
|恢复路径 (recovery path)|使数据库到达特定时间点（称为恢复点）的一组数据和日志备份。 恢复路径是一组特定的转换，这些转换随着时间的变化对数据库进行演变并保持数据库的一致性。 恢复路径描述从“起点”(LSN,GUID) 到“终点”(LSN,GUID) 的一组 LSN。 恢复路径中的 LSN 可以从起点到终点遍历一个或多个恢复分支。|  
|恢复点 (recovery point)|日志链中的点，恢复过程中前滚在该点停止。|  
|矩形 (rectangle)|一个报表项，可用作多个报表项的容器，也可用作报表上的一个图形元素。|  
|递归层次结构 (recursive hierarchy)|所有父子关系都以数据形式表示的数据层次结构。|  
|递归分区 (recursive partitioning)|数据挖掘算法提供程序用来将数据划分为组直至找不到更多有用组的迭代过程。|  
|重做 (redo)|恢复过程中的一个阶段，通过将记录的更改应用于数据库（前滚），使数据在时间上向前移动。|  
|重做阶段 (redo phase)|恢复过程中的一个阶段，通过将记录的更改应用于数据库（前滚），使数据在时间上向前移动。|  
|重做集 (redo set)|所还原的所有文件和页面的集合。|  
|引用数据 (reference data)|特性为共享读取操作且不频繁地发生变化的数据。 引用数据的示例包括航班计划表和产品目录。 Windows Server AppFabric 提供了本地缓存功能来存储此类数据。|  
|引用维度 (reference dimension)|维度与度量值组之间的关系，在这种关系中，维度通过另一维度与度量值组关联起来。|  
|引用表 (reference table)|要在模糊查找中使用的源表。|  
|被引用键 (referenced key)|外键引用的主键或唯一键。|  
|引用键 (referencing key)|某一数据库表中来自另一个表（也称作“被引用表”）的键，并且其值匹配该被引用表中的主键 (PK) 或唯一键。|  
|反身关系 (reflexive relationship)|从表中的列或列组合到同一个表中的其他列的关系。|  
|region|缓存内数据的容器，它将所有缓存对象一起放置于单个缓存主机中。 通过缓存区域，可使用称作标记的说明性字符串搜索该缓存区域中所有缓存的对象。|  
|region|一个文件中按逻辑顺序排列的 128 个叶级页的集合。 用来标识已分段文件中的区域。|  
|注册模型 (registration model)|一种已定义的用于提交和审批注册请求的方法。 企业通常选择一个注册模型，并相应地修改其管理策略。|  
|回归|基于数据集中的其他属性预测一个或多个连续变量（如利润或亏损）的统计过程。|  
|回归量 (regressor)|与输出变量具有线性关系的输入变量。|  
|关系数据库管理系统 (relational database management system)|按关系模型指定的方式将数据组织为相关行和列的数据库系统。|  
|关系引擎|处理存储引擎的 SQL Server 组件。 它负责解释 Transact-SQL 搜索查询并找出搜索由存储引擎提供的原始物理数据并将结果返回给用户的最高效方法。|  
|关系 OLAP|使用关系数据库中的表存储多维结构的存储模式。|  
|关系存储区 (relational store)|根据关系模型设置结构的数据存储库。|  
|关系对象 (relationship object)|表示担当彼此相关的角色的对象对的对象。|  
|相对日期 (relative date)|一个日期范围，通过比较运算符指定，并返回某个日期范围内的数据。|  
|远程数据 (remote data)|独立于当前 SQL Server 实例的 OLE DB 数据源中存储的数据。|  
|远程数据访问 (remote data access)|一种服务，它为智能设备应用程序访问（请求）远程 SQL Server 数据库表和本地 SQL Server Mobile Edition 数据库表，以及向/从这些数据库表中发送（推送）数据提供了一种简单的方式。 还可以使用 RDA 在运行 SQL Server 的服务器上发出 SQL 命令。|  
|远程分发服务器 (remote Distributor)|配置为分发服务器的服务器，独立于配置为发布服务器的服务器。|  
|远程登录标识 (remote login identification)|分配给用户以访问远程服务器上的远程过程的登录标识。|  
|远程分区 (remote partition)|一种分区，其数据存储在运行 Analysis Services 实例的服务器上，而不是用于存储分区元数据的服务器上。|  
|远程服务绑定 (remote service binding)|一种 Service Broker 对象，用来为远程服务指定本地安全凭据。|  
|远程存储过程 (remote stored procedure)|位于某个 SQL Server 实例上却由另一个 SQL Server 实例上的语句执行的存储过程。|  
|远程表 (remote table)|独立于当前 SQL Server 实例的 OLE DB 数据源中存储的表。|  
|呈现的输出 (rendered output)|来自呈现扩展插件的输出。|  
|呈现的报表 (rendered report)|包含数据和布局信息的完全处理报表，采用了适于查看的格式（例如，HTML）。|  
|呈现扩展插件 (rendering extension)|一个以特定格式呈现报表的插件（例如，Excel 呈现扩展插件）|  
|呈现对象模型 (rendering object model)|呈现扩展插件所使用的报表对象模型。|  
|副本 (replica)|位于 DPM 服务器上单个卷中的受保护数据的完整副本。 在将每个受保护的数据源添加到其保护组中后，将为其创建一个副本。 通过存储在一起，多个数据源可以在同一个副本卷上具有其副本。|  
|副本 (replica)|要同步的信息的特定存储库。|  
|副本 ID (replica ID)|用于唯一标识副本的值。|  
|副本键 (replica key)|在副本键映射中映射为副本 ID 的 4 字节的值。|  
|副本时钟周期 (replica tick count)|一个单调递增的数字，用于唯一标识对副本中某项所做的某次更改。|  
|复制|将内容和/或配置设置从一个位置（通常为服务器节点）复制到另一个位置的过程。 执行复制是为了确保同步或故障容错。|  
|复制管理对象|一个封装了 SQL Server 的复制功能的托管代码程序集。|  
|报表生成器|一种报表创作工具，它不但具备类似 Microsoft Office 的创作环境，并且还提供一些功能，例如新的迷你图、数据条和指示器数据可视化效果，能够将报表项保存为报表部件，用于创建地图的向导，聚合的聚合，以及对表达式的增强的支持。|  
|“报表数据”窗格 (report data pane)|一个数据窗格，用于显示表示用户报表中数据的项的层次结构视图。 顶级节点表示内置字段、参数、图像和数据源引用。|  
|报表定义 (report definition)|报表在处理或呈现之前的蓝图。 报表定义包含有关报表的查询和布局的信息。|  
|报表定义语言|描述报表的布局和查询信息的一组指令。 RDL 由 XML 元素组成，这些元素符合为 Reporting Services 创建的 XML 语法。|  
|报表设计器|承载在 Microsoft Visual Studio 环境中的一组设计图面和图形工具。|  
|报表执行快照 (report execution snapshot)|缓存的报表快照。 如果报表管理员希望从静态副本中运行报表，则将创建报表执行快照。|  
|报表历史记录|以前运行的报表副本的集合。|  
|报表历史记录快照 (report history snapshot)|包含在特定时间点捕获的数据的报表历史记录。|  
|报告中间格式 (report intermediate format)|报表的内部表示形式。|  
|报表项 (report item)|报表上的报表。|  
|报表布局模板 (report layout template)|报表生成器中预先设计的表、矩阵或图表报表模板。|  
|报表链接 (report link)|指向报表的 URL。|  
|报表管理器|基于 Web 的报表管理工具|  
|报表模型|用来创建特别报告的业务数据的元数据说明。|  
|报表部件 (report part)|已单独发布到报表服务器上并且可以在其他报表中重复使用的报表项。|  
|报表处理器组件 (Report Processor component)|从报表服务器数据库检索报表定义并将其与来自该报表的数据源中的数据相结合的组件。|  
|报表项目 (Report Project)|报表创作环境中的一个模板。|  
|报表项目向导|报表创作环境中用于创建报表的向导。|  
|报表呈现 (report rendering)|组合报表布局与数据源的数据以查看报表的操作。|  
|报表服务器|网络上用来启动报表生成器以及保存、管理和发布报表的位置。|  
|报表服务器管理员 (report server administrator)|具有提升特权的用户，能够访问报表服务器的所有设置和内容。 报表服务器管理员是被授予了内容管理员角色和/或系统管理员角色的用户。 所有本地管理员都将自动成为报表服务器管理员，但其他用户可以成为报表服务器命名空间总体或其中一部分的报表服务器管理员。|  
|报表服务器数据库|为报表服务器提供内部存储位置的数据库。|  
|报表服务器执行帐户 (report server execution account)|报表服务器 Web 服务和报表服务器 Windows 服务在运行时使用的帐户。|  
|报表服务器 Web 服务|一种承载、处理和传递报表的 Web 服务。|  
|报表快照 (report snapshot)|一种包含在特定时间点捕获的数据的静态报表。|  
|报表特定计划 (report-specific schedule)|根据报表定义的计划。 报表特定计划在特定的报表、订阅或报表执行操作的上下文中定义，用于确定缓存过期或快照更新的时间。|  
|repository|包含信息模型的数据库，这些模型与可执行软件一起管理该数据库。|  
|存储库引擎 (repository engine)|一种面向对象的软件，为存储库数据库提供管理支持并提供对存储库数据库的客户访问。|  
|存储库对象 (repository object)|表示存储库类型库中存储的数据结构的 COM 对象。|  
|存储库 SQL 架构 (Repository SQL schema)|存储库引擎用来管理所有存储库对象、关系和集合的一组标准表。|  
|存储库类型信息模型 (Repository Type Information Model)|一种表示 Metadata Services 的存储库类型定义的核心对象模型。|  
|重新发布服务器 (republisher)|发布从发布服务器接收的数据的订阅服务器。|  
|保留字符 (reserved character)|对程序而言具有特殊意义，因此，正常情况下无法用于为文件、文档和其他用户生成的工具（如宏）指定名称的键盘字符。 通常为特殊用途保留的字符包括星号（*）、正斜杠（/）、反斜杠（ \\ ）、问号（？）和竖线（&#124;）。|  
|解决策略 (resolution strategy)|存储库引擎在选择对象（存在多个版本，并且在调用程序中未指定版本信息）时按顺序评估的一组条件。|  
|resource|一个特殊变量，它保留着对数据库连接或语句的引用。|  
|resource|报表服务器数据库中除报表项、文件夹项和共享数据源项以外的任何项。|  
|资源数据 (resource data)|一种类型的数据，其特征为共享、同时读入和写入操作中以及供多个事务访问。 资源数据的示例包括用户帐户和拍卖项。|  
|资源调控器 (resource governor)|SQL Server 2008 中的一项新功能，使用户可以通过指定传入请求的资源消耗限制来控制 SQL Server 工作负荷和资源。|  
|还原|一种包括多个阶段的过程，用于将指定备份中的所有数据和日志页复制到指定数据库（数据复制阶段），然后前滚备份中记录的所有事务（重做阶段）。 此时，在默认情况下，还原将回滚任何不完整的事务（撤消阶段），这会完成数据库的恢复并使其可供用户使用。|  
|还原顺序 (restore sequence)|包含一个或多个还原命令的顺序，通常用于初始化要还原的数据库、文件和/或页的内容（数据复制阶段），前滚记录的事务（重做阶段）以及回滚未提交的事务（撤销阶段）。|  
|结果集 (result set)|通过运行查询或应用筛选器得到的记录集。|  
|results|通过运行查询或应用筛选器得到的记录集。|  
|结果窗格 (results pane)|一种窗格，显示与在用户界面的其他部分中选择的项有关的详细信息。 例如，在 Microsoft 管理控制台 (MMC) 中，详细信息窗格是位于右侧的窗格，显示控制台树中所选项的详细信息。|  
|retract 事件 (retract event)|一种内部事件类型，用于通过修改事件的结束时间来修改现有插入事件。|  
|可重用书签 (reusable bookmark)|可从给定表的行集使用并由同一表的另一行集用来对相应行进行定位的书签。|  
|撤消延迟 (revocation delay)|提出凭据撤消请求与实际撤消请求之间的时间段。|  
|RIA|提供用户界面的 Web 应用程序，与典型的网页相比，它更像桌面应用程序。 它不将整个网页发布到 Web 服务器，就能够处理用户操作。|  
|RIA 服务链接 (RIA Services link)|项目间链接引用，有助于从中间层节点生成演示层节点。|  
|丰富 Internet 应用程序 (rich Internet application)|提供用户界面的 Web 应用程序，与典型的网页相比，它更像桌面应用程序。 它不将整个网页发布到 Web 服务器，就能够处理用户操作。|  
|右外部联接 (right outer join)|一种外部联接，其中，查询的 SQL 语句中 RIGHT JOIN 操作右侧的所有记录都添加到查询结果中，即使在表中左侧的联接字段中没有任何匹配值也不例外。|  
|环索引 (ring index)|指示多边形实例中的环数的索引。|  
|RMO|一个封装了 SQL Server 的复制功能的托管代码程序集。|  
|角色分配 (role assignment)|分配特定的角色，此角色确定用户或组是否可以访问特定项和对其执行某个操作。|  
|角色定义 (role definition)|与角色关联的任何权限集合。|  
|角色切换|在数据库镜像会话中，由镜像数据库接管主体角色的过程。|  
|角色扮演维度 (role-playing dimension)|一个按不同的外键与事实数据表联接以生成多个多维数据集维度的数据库维度。|  
|回滚 (roll back)|撤消更改。|  
|前滚 (roll forward)|将所记录的更改应用于前滚集中的数据以使该数据在时间上向前移动。|  
|前滚集 (roll forward set)|按照某个还原顺序还原的所有数据的集合。 前滚集定义为还原一系列数据备份（一个或多个数据备份）。|  
|汇总 (roll up)|在一个位置收集来自多个位置的数据子集。|  
|滚动更新文件 (rollover file)|选择文件滚动更新选项后，在达到最大文件大小时，SQL Server 会关闭当前文件并创建一个新文件，此文件就是滚动更新文件。|  
|路由|一种 Service Broker 对象，用来为远程服务指定网络地址。|  
|路由客户端 (routing client)|一种缓存客户端，它包括由群集中的前导主机维护的路由表，并使客户端能够直接从缓存数据所在的缓存主机直接获得这些数据。|  
|路由表 (routing table)|路由客户端用来跟踪缓存群集中所有缓存主机的连接信息的数据结构。 它由群集中的前导主机进行维护。 它使路由客户端可以直接从缓存数据所在的缓存主机获得这些数据。|  
|行聚合函数 (row aggregate function)|生成汇总值的一种函数，其生成的汇总值在查询结果中显示为附加行。|  
|行锁 (row lock)|表中某一单个行的锁。|  
|行版本控制 (row versioning)|在联机索引操作中，一个使索引操作不受其他事务所做的修改的影响的功能。|  
|行溢出数据 (row-overflow data)|由于表中相应列的总宽度超过了每行 8,060 字节的限制而存储在表或索引的主数据页之外的 varchar、nvarchar、varbinary 或 sql_variant 数据。|  
|行集 (rowset)|每一行都拥有一个或多个数据列的一组行。|  
|rs 实用工具|报表脚本编写工具。|  
|rs.exe|报表脚本编写工具。|  
|rsconfig 配置工具|服务器连接管理工具。|  
|rsconfig.exe|服务器连接管理工具。|  
|规则触发 (rule firing)|运行应用程序定义文件中定义的某个应用程序规则（事件历史记录规则、订阅事件规则和订阅预定规则）的过程。|  
|失控查询 (runaway query)|运行时间过长而可能导致阻塞问题的查询。 失控查询通常不使用查询或锁定超时。|  
|运行时错误 (run-time error)|当执行程序时发生的、由编译器或其他监督程序检测到的软件错误。|  
|安全代码 (safe code)|由公共语言运行时环境（而非由操作系统直接）执行的代码。 托管代码应用程序获得公共语言运行时服务，如自动垃圾收集、运行时类型检查和安全支持等。 这些服务帮助提供独立于平台和语言的、统一的托管代码应用程序行为。|  
|取样 (sampling)|一种统计过程，它通过对相关的总体或数据集的一部分进行观测或分析，生成有关此总体或数据集的整体结论信息。|  
|保存过程 (save process)|向磁盘写入数据的过程。|  
|保存点|在按条件取消某个事务的一部分或当事务遇到错误，因而提供一种机制来回滚事务的一部分时，该事务可以返回的一个位置。|  
|SBCS|一种字符编码，其中每个字符由 1 个字节表示。 从数学上来说，单字节字符集限制为 256 个字符。|  
|标量 (scalar)|一个包含单个值的因子、系数或变量（与记录、数组或某种其他复杂数据结构相对）。|  
|标量值函数 (scalar-valued function)|一个函数，它返回单个值，如字符串、整数或位值。|  
|分隔线 (scale break line)|在图标区域种绘制的一条线，指示图标上高范围值与低范围值之间的重大差异。|  
|扩展部署 (scale-out deployment)|一种部署模型，其中，安装配置具有多个共享单个报表服务器数据库的报表服务器实例。|  
|计划和传递处理器|处理计划和传递的报表服务器引擎组件。 与 SQL 代理一起使用。|  
|架构行集 (schema rowset)|一个专门定义的行集，它返回 SQL Server 实例或 Analysis Services 实例上的对象或功能的元数据。  例如，OLE DB 架构行集 DBSCHEMA_COLUMNS 描述表中的列，而 Analysis Services 架构行集 MDSCHEMA_MEASURES 描述多维数据集中的度量值。|  
|架构快照 (schema snapshot)|一种快照，其中包括复制所需的已发布表和对象（触发器、元数据表等）的架构，但不包括用户数据。|  
|识别架构 (schema-aware)|与基于架构的处理方法有关，此架构用于定义将用来验证输入和输出文档的元素、属性和类型。|  
|scope|可以在程序中引用某个标识符（如对象或属性）的程度。 范围对于应用程序可以是全局的，对于活动文档可以是本地的。|  
|scope|正在同步的数据的集合。|  
|脚本内存 (script memory)|PHP 脚本使用的本地内存（客户端 RAM）。|  
|脚本窗格 (script pane)|表设计器的文本编辑器部分。|  
|编写脚本|指的是通过脚本在计算机上自动执行用户操作或配置标准状态。|  
|SDK|一组例程（通常在一个或多个库中），旨在使开发人员能够更轻松地为给定的计算机、操作系统或用户界面编写程序。|  
|search condition|WHERE 或 HAVING 子句中的谓词，用于指定源行要包含在 SQL 语句中必须满足的条件。|  
|搜索键 (search key)|要在文档或任何数据集合中搜索的值。|  
|辅助数据库 (secondary database)|主数据库的只读副本。|  
|辅助 DPM 服务器 (secondary DPM server)|保护一个或多个主 DPM 服务器以及文件和应用程序数据的 DPM 服务器。|  
|辅助保护 (secondary protection)|一种保护类型，其中，受保护服务器上的数据由主 DPM 服务器进行保护，而由辅助 DPM 服务器保护主 DPM 服务器上的副本。|  
|辅助服务器 (secondary server)|日志传送配置中辅助数据库所在的服务器实例。 辅助服务器定期从主数据库复制最新的日志备份并将日志还原到辅助数据库。 辅助服务器是热备用服务器。|  
|密钥提供程序 (secret provider)|生成和验证一次性密码以对用户进行身份验证的组件。|  
|安全对象 (securable)|可以通过权限得到保护的实体。 最主要的安全对象是服务器和数据库，但可以在更细化的级别设置各种权限。|  
|安全套接字层 (Secure Sockets Layer)|一种通过结合使用数据加密、数字证书和公钥密码系统提高数据通信安全性的协议。 SSL 支持在网络中进行身份验证并增强数据安全性和隐私。 SSL 不提供授权或不可否认性。|  
|安全扩展插件 (security extension)|Reporting Services 中的一个组件，用于对要访问报表服务器的用户或组进行身份验证。|  
|安全 ID (security ID)|在基于 Windows 的系统中，表示企业内的用户、组或计算机帐户的唯一值。 创建每个帐户时，都会为其颁发一个 SID。|  
|安全标识符 (security identifier)|在基于 Windows 的系统中，表示企业内的用户、组或计算机帐户的唯一值。 创建每个帐户时，都会为其颁发一个 SID。|  
|分段|一种数据挖掘方法，用于对数据进行分析以找出共享相似属性集的互斥记录集合。|  
|自联接 (self-join)|将某个表中的记录与同一表中的其他记录相结合（如果联接字段中具有匹配的值）的一种联接。 自联接可以是内部联接或外部联接。 在数据库关系图中，自联接称为反身关系。|  
|自助注册模型 (self-service registration model)|一种 Certificate Lifecycle Manager (CLM) 注册模型，其中，证书订阅方使用基于 Web 的界面直接执行或请求证书管理活动。|  
|自跟踪实体 (self-tracking entity)|从文本模板转换工具包 (T4) 模板中生成的一种实体，该实体可以将更改记录到标量属性、复杂属性以及导航属性中。|  
|语义模型定义语言 (Semantic Model Definition Language)|一组指令，用来描述在报表生成器中创建的报表的布局和查询信息。|  
|语义对象 (semantic object)|可以由数据库对象或其他实际对象表示的对象。|  
|语义验证 (semantic validation)|确认 XML 文件的元素在逻辑上有效的过程。|  
|半累加性度量值 (semiadditive measure)|可以根据多维数据集中的一个或多个（但不是全部）维度进行求和的一种度量值。|  
|敏感游标 (sensitive cursor)|打开时能够反映其他用户对基础数据所做的修改的一种游标。|  
|敏感数据 (sensitive data)|法律或政策以特殊方式保护的个人身份信息 (PII)。|  
|顺序集合 (sequenced collection)|顺序关系对象的目标对象的集合。|  
|顺序关系 (sequenced relationship)|存储库中的一种关系，它指定了每个目标对象在目标对象集合内的显式位置。|  
|序列号 (serial number)|分配给特定库存物料的编号，用于标识此物料并将其与其他具有相同物料编号的相似物料区分开来。|  
|序列化|将对象的状态信息转换为可以存储或传输的窗体的过程。 在序列化期间，对象将其当前状态写入到临时或持久性存储区。 以后，可以通过从存储区中读取或反序列化对象的状态，重新创建该对象。|  
|server|向网络用户提供共享资源（如文件或打印机）的计算机。|  
|服务器排序规则 (server collation)|SQL Server 实例的排序规则。|  
|服务器游标 (server cursor)|在服务器上实现的游标。|  
|服务器名称|用于唯一标识网络上的服务器计算机的名称。|  
|服务器订阅 (server subscription)|一种对合并发布的订阅，它具有分配的优先级值，用来检测和解决冲突。|  
|服务|执行特定的系统功能以支持其他程序的程序、例程或进程。|  
|Service Broker|一种帮助开发人员生成安全的可缩放数据库应用程序的技术。|  
|服务连接点 (service connection point)|一个 Active Directory 节点，在此节点上，系统管理员可以为用户和组定义 Certificate Lifecycle Manager (CLM) 管理权限。|  
|服务主体 (service principal)|与 Kerberos 对等通信内端点节点中的服务实体关联的全局唯一名称。|  
|服务主体名称 (service principal name)|客户端用于唯一标识服务实例的名称。 它通常从主机的 DNS 名称构建而来。 SPN 用于在客户端与托管特定服务的服务器之间相互进行身份验证的过程中。|  
|服务程序 (service program)|使用 Service Broker 功能的程序。  服务程序可以是 Transact-SQL 存储过程、SQLCLR 存储过程或外部程序。|  
|会话|连接处于活动状态并且可以发生通信的时间段。 为了在功能单元之间进行数据通信，会话还指在建立、维护和释放连接期间发生的所有活动。|  
|会话状态|在 ASP.NET 中，在服务器上为当前用户创建的变量存储区；每个用户在服务器上维护一个单独的会话状态。 会话状态通常用于存储回发之间用户特定的信息。|  
|set|数据源中维度成员或项的分组，它们被命名为单个单元且被视为单个单元，并可以多次引用或重复使用。|  
|安装程序初始化文件 (setup initialization file)|使用 Windows .ini 文件格式的一种文本文件，其中存储了配置信息，用于在没有用户来响应安装程序的提示的情况下安装 SQL Server。|  
|安装修复 (setup repair)|在安装程序的过程中，当出现问题时可能运行的一种错误报告过程。|  
|快照 (shadow copy)|一组数据的静态图像，如显示为查询结果的记录。|  
|形状文件 (shapefile)|一种用于在地理信息系统中互换空间数据的公共域格式。 形状文件的文件扩展名为 .shp。|  
|均摊 (sharding)|一种对大型数据集进行分区的方法，可提高性能和可伸缩性，并支持跨多个租户对数据进行分布式查询。|  
|共享的代码 (shared code)|服务器项目和客户端项目中专门指定的未经修改的代码。|  
|共享数据源项 (shared data source item)|封装在项中的数据源连接信息。 可以作为报表服务器文件夹命名空间中的项进行管理。|  
|共享维度 (shared dimension)|在数据库内创建的、可由该数据库内任意多维数据集使用的维度。|  
|共享锁 (shared lock)|通过非更新（读取）操作创建的锁。|  
|共享计划 (shared schedule)|可由多个项引用的计划信息。|  
|购物篮分析|一种标准的数据挖掘算法，它分析一系列事务以预测用户最频繁地采购哪些商品。|  
|显示计划 (Showplan)|显示 SQL 语句执行计划的一种报表。|  
|SID|在基于 Windows 的系统中，表示企业内的用户、组或计算机帐户的唯一值。 创建每个帐户时，都会为其颁发一个 SID。|  
|significance|FLOOR 函数的参数之一。|  
|Silverlight 业务应用程序 (Silverlight business application)|提供许多通用功能以便使用 Silverlight 客户端构建业务应用程序的模板。 它利用 WCF RIA 服务进行身份验证和注册服务。|  
|简单客户端 (simple client)|一种缓存客户端类型，它没有路由表，因此不需要与缓存群集中的所有缓存主机建立网络连接。 因为从群集传输到简单客户端的数据可能需要途径多个缓存主机，所以，简单客户端的执行速度可能比不上路由客户端。|  
|简单邮件传输协议 (Simple Mail Transfer Protocol)|TCP/IP 协议套件中的一个成员，管辖电子邮件在邮件传输代理之间的交换。|  
|简单恢复模式|一种数据库恢复模式，它记录的全部事务刚好足够在系统崩溃或还原数据备份后确保数据库一致性。 数据库最多只能恢复到其最新的数据备份，并且不支持还原单独页面。|  
|单字节字符集 (single-byte character set)|一种字符编码，其中每个字符由 1 个字节表示。 从数学上来说，单字节字符集限制为 256 个字符。|  
|单精度 (single-precision)|属于浮点数或与浮点数相关，在编程语言通常提供的两个或更多选项（如单精度与双精度）中具有最低精度。|  
|单用户模式|只有一个用户可以访问资源的一种状态。|  
|接收器|从其他设备接受内容的设备或设备的一部分。|  
|SKU|产品的唯一标识符（通常为字母）。 通过 SKU 可以跟踪产品来维护库存。 SKU 可以与可采购的任何物料关联。 例如，样式编号为 3726 和尺码为 8 的衬衣的 SKU 可能为 3726-8。|  
|sleep|暂停操作但不终止。|  
|切片|多维数据集中的一个数据子集，通过用维度成员限制一个或多个维度来指定。|  
|切片器|提供一次单击筛选控件的一种功能，通过这些控件，可以很轻松地缩小数据集的正查看部分的范围。|  
|滑动窗口 (sliding window)|固定长度 L 的窗口，该窗口根据流事件沿时间线移动。 对于时间线上的每个事件，都会创建一个新窗口，并在事件的开始时间开始。|  
|补充 (slipstream)|将更新、修补程序或 Service Pack 集成到原始软件的基本安装文件中，以便生成的文件允许单步安装更新的软件。|  
|补充安装 (slipstream installation)|一种安装类型，它将操作系统或程序的基本安装文件与其 Service Pack、更新或修补程序相集成，并通过一个步骤安装它们。|  
|智能卡 (smart card)|使用嵌入的微处理器和少量存储（带有访问代码）的塑料（信用卡大小或更小）设备，用于启用基于证书的身份验证。 智能卡可安全地存储证书、公钥和私钥、密码以及其他类型的个人信息。|  
|智能卡个性化控制 (Smart Card Personalization Control)|一种 ActiveX 控件，该控件可自动在客户端计算机上执行所有 Certificate Lifecycle Manager (CLM) 智能卡应用程序管理活动。|  
|智能卡配置文件 (smart card profile)|在使用配置文件模板（只包括基于智能卡的证书模板）执行请求时创建的 Lifecycle Manager (CLM) 配置文件。|  
|智能卡读卡器 (smart card reader)|计算机中安装的一种装置，支持使用智能卡实现增强的安全功能。|  
|Smart Card Self Service Control|客户端计算机上安装的软件，使最终用户和管理员能够通过提供从客户端计算机到智能卡的连接来管理智能卡。|  
|智能卡取消阻止 (smart card unblocking)|将智能卡与管理凭据绑定以便重置个人标识号（PIN）尝试计数器的操作。|  
|SMO|一种应用程序编程接口，支持将 SQL Server 管理整合到任何 COM 或 OLE 自动化应用程序中。|  
|SMTP|TCP/IP 协议套件中的一个成员，管辖电子邮件在邮件传输代理之间的交换。|  
|管理单元 (snap-in)|一种可以添加到由 Microsoft 管理控制台 (MMC) 支持的控制台的工具。 可以独自添加单独的管理单元；扩展管理单元只能添加用于扩展其他管理单元的功能。|  
|快照|一种包含在特定时间点捕获的数据的静态报表。|  
|快照隔离级别 (snapshot isolation level)|一种事务隔离级别，其中一个事务执行的每次读取操作都返回该事务开始时存在的所有数据。 因为快照事务不使用锁来防止读取操作，所以，它不阻止其他事务修改由快照事务读取的任何数据。|  
|快照复制|一种复制方式，其中，数据完全按照其在特定时刻的状态分发，不监视数据是否有更新。|  
|快照共享 (Snapshot Share)|可用于存储快照文件的共享。 快照文件包含已发布表的架构和数据。|  
|快照窗口 (snapshot window)|根据流中事件的开始和结束时间（而非时间线上的固定网格）定义的窗口。|  
|雪花型架构 (snowflake schema)|对星型架构的一种扩展，即，由多个表定义一个或多个维度。 在雪花型架构中，只有主维度表联接到事实数据表。 其他维度表联接到主维度表。|  
|软页 (soft page)|一种呈现的页面，可能稍大于使用报表的 InteractiveHeight 和 InteractiveWidth（HTML 和 WinForm 控件）属性指定的大小。|  
|软分页呈现器 (soft page-break renderer)|一种呈现扩展插件，它维护报表布局和格式，以便对生成的文件进行优化，从而实现基于屏幕（例如，在网页上或在 ReportViewer 控件中）进行查看和交付。|  
|软件开发包 (software development kit)|一组例程（通常在一个或多个库中），旨在使开发人员能够更轻松地为给定的计算机、操作系统或用户界面编写程序。|  
|软件配置文件 (software profile)|在使用配置文件模板（只包括基于软件的证书模板）执行请求时创建的 Lifecycle Manager (CLM) 配置文件。|  
|软件转换器 (software transformer)|一个软件模块或例程，它将事件（数据）修改为输出设备所需的格式，并将数据发送给该设备。|  
|解决方案资源管理器 (solution explorer)|Microsoft SQL Server Management Studio 的一个组件，用于在解决方案或项目中查看和管理项以及执行项管理任务。|  
|求解次序 (solve order)|在多维数据集的单次计算传递中，计算成员、自定义成员、自定义汇总公式和计算单元的求值次序（从最高求解次序到最低求解次序）和计算次序（从最低求解次序到最高求解次序）。|  
|排序顺序 (sort order)|一种根据值类型或数据类型对数据进行排列的方式。 可以按字母顺序、数字顺序或按日期对数据排序。 排序顺序使用升序（1 到 9、A 到 Z）或降序（9 到 1、Z 到 A）。|  
|source|从中获取或移动数据的磁盘、文件、文档或其他信息集合。|  
|source|SSIS 数据流组件，它使数据流中的其他组件可以访问来自不同外部数据源的数据。|  
|source|枚举任何更改并将其发送到目标提供程序的同步提供程序。|  
|源适配器 (source adapter)|用来从数据源中提取数据的数据流组件。|  
|源代码管理 (source code control)|一组功能，其中包括用于检查进出中心存储库的源代码的机制。 它还指版本控制系统，可以在整个开发生存期中管理文件，同时跟踪发生了哪些更改以及执行更改的用户、时间和原因。|  
|源代码管理 (source control)|一组功能，其中包括用于检查进出中心存储库的源代码的机制。 它还指版本控制系统，可以在整个开发生存期中管理文件，同时跟踪发生了哪些更改以及执行更改的用户、时间和原因。|  
|源多维数据集 (source cube)|链接多维数据集所基于的多维数据集。|  
|源数据库 (source database)|发布服务器上的一种数据库，其中的数据和数据库对象被标记为要进行复制，作为传播给订阅服务器的发布的一部分。 对于数据库视图，指创建视图所在的数据库。|  
|源对象 (source object)|某一特定集合中的所有对象通过关系（全部为同一关系类型）与其连接的单个对象。|  
|源分区 (source partition)|一种被合并到另一个分区并在合并过程结束后自动删除的 Analysis Services 分区。|  
|源提供程序 (source provider)|枚举任何更改并将其发送到目标提供程序的同步提供程序。|  
|迷你图 (sparkline)|可插入到文本或嵌入到工作表上的单元格中的小型图表，用于说明数据中的高、低值和趋势。|  
|稀疏列 (sparse column)|一种列，它可以减少 Null 值的存储空间需求，但代价是检索非 Null 值的开销增加。|  
|稀疏文件 (sparse file)|此文件的处理方式需要的磁盘空间要比其他方式少很多。 支持稀疏使得应用程序能够创建非常大的文件，而不需要调拨磁盘空间来容纳只包含零的那些文件区域。 例如，您可以通过稀疏支持来处理 42-GB 文件，其中，您只需向第一个 64 KB 写入数据（文件的剩余部分归零）。|  
|稀疏度 (sparsity)|不含数据的多维结构单元的相对百分比。|  
|空间数据 (spatial data)|数据由 2D 或 3D 图像表示。 空间数据可以进一步细分为几何图形数据（可以使用涉及欧几里得几何计算的数据）和地理数据（确定地球上的地理位置和边界的数据）。|  
|SPN|客户端用于唯一标识服务实例的名称。 它通常从主机的 DNS 名称构建而来。 SPN 用于在客户端与托管特定服务的服务器之间相互进行身份验证的过程中。|  
|SQL|一种数据库查询和编程语言，广泛用于访问、查询、更新和管理关系数据库系统中的数据。|  
|SQL 数据库|基于结构化查询语言 (SQL) 的数据库。|  
|SQL 表达式 (SQL expression)|运算符、常量、文本值、函数、表名和字段名的任意组合，其计算结果为单个值。|  
|SQL Native Client|同时用于 OLE DB 和 ODBC 的独立数据访问 API。|  
|SQL Server|Microsoft 关系数据库管理和分析系统的一个系列，用于实现电子商务、业务线和数据仓库解决方案。|  
|SQL Server 2005 Express Edition|Microsoft 关系数据库设计和管理系统的一个版本，用于实现电子商务、业务线和数据仓库解决方案。|  
|SQL Server 2005 Mobile Edition|SQL Server 产品名称（版本）|  
|SQL Server 代理|一种 Microsoft Windows 服务，它执行称作“作业”的计划的管理任务，并且在 SQL Server 中存储信息。|  
|SQL Server Analysis Services|Microsoft SQL Server 的一个功能，为商业智能应用程序提供联机分析处理 (OLAP) 和数据挖掘支持。 Analysis Services 将来自数据仓库的数据组织到具有预先计算的聚合数据的多维数据集中，从而快速响应复杂的分析查询。|  
|SQL Server Browser|可侦听对 Microsoft SQL Server 资源的传入请求并为客户端提供有关计算机中安装的 SQL Server 实例的信息的 Windows 服务。|  
|SQL Server Compact|Microsoft 关系数据库管理和分析系统，用于实现电子商务、业务线和数据仓库解决方案。|  
|SQL Server 组件 (SQL Server component)|SQL Server 程序模块，用于执行一组特定任务 - 例如，数据转换、数据分析和报告。|  
|SQL Server 配置管理器|一种工具，用于管理与 SQL Server 相关联的服务、配置 SQL Server 使用的网络协议以及从 SQL Server 客户端计算机管理网络连接配置。|  
|SQL Server 连接控制器 (SQL Server Configuration Manager)|一种连接技术，其中，基于不同数据访问技术的应用程序（.NET 或本机 Win32）可以共享相同的连接信息。 可为此类客户端应用程序集中管理连接信息。|  
|SQL Server 数据挖掘内容查看器 (SQL Server Data Mining Content Viewer)|一种查看器，显示在挖掘模型的内容架构行集中包含的内容。|  
|SQL Server 数据挖掘内容查看器控件 (SQL Server Data Mining Content Viewer Controls)|一组服务器端控件，可供用户在任何安装了 Microsoft Internet Explorer 的计算机上浏览复杂的挖掘模型。|  
|SQL Server Data Quality Services|一种基于知识的数据质量系统，它使用户能够执行知识发现和管理、数据清除、数据匹配、与引用数据服务集成以及集成的事件探查。|  
|SQL Server 数据层应用程序项目 (SQL Server data-tier application project)|数据库开发人员用于创建和开发 DAC 的 Visual Studio 项目。 在 Visual Studio 和 VSTS 源代码控制、版本控制和开发项目管理中完全支持 DAC 项目。|  
|SQL Server 最终用户恢复 (SQL Server End-User Recovery)|用于 SQL Server 的一种工具，它使备份管理员能够授权最终用户从 DPM 恢复 SQL Server 数据库的备份，而无需备份管理员进一步执行操作。|  
|SQL Server EUR|用于 SQL Server 的一种工具，它使备份管理员能够授权最终用户从 DPM 恢复 SQL Server 数据库的备份，而无需备份管理员进一步执行操作。|  
|SQL Server 执行包实用工具 (SQL Server Execute Package Utility)|用于运行 Integration Services 包的图形用户界面。|  
|SQL Server Express|Microsoft 关系数据库设计和管理系统的一个版本，用于实现电子商务、业务线和数据仓库解决方案。|  
|SQL Server 实例|计算机上运行的 SQL Server 副本。|  
|SQL Server 实例自动保护 (SQL Server instance auto-protection)|一种保护类型，使 DPM 可以自动确定和保护添加到配置为自动保护的 SQL Server 实例的数据库。|  
|SQL Server 登录名|存储在 SQL Server 中的帐户，用户可使用它连接到 SQL Server。|  
|SQL Server 管理对象|一种应用程序编程接口，支持将 SQL Server 管理整合到任何 COM 或 OLE 自动化应用程序中。|  
|SQL Server Management Studio|Microsoft SQL Server 中随附的一套管理工具，用于配置和管理 Microsoft SQL Server 中的所有组件。|  
|SQL Server Master Data Services|一个主数据管理应用程序，可一致地定义和管理组织的关键数据实体。|  
|SQL Server PowerPivot for Excel|SQL Server 面向 Excel 的外接程序。|  
|SQL Server Profiler|用于监视 SQL Server 数据库引擎实例或 Analysis Services 实例的图形用户界面。|  
|SQL Server Reporting Services|一种基于服务器的报表生成环境，它提供企业级的 Web 报表功能，从而使您可以创建从多个数据源提取数据的表，发布各种格式的表，以及集中管理安全性和订阅。|  
|SQL Server Service Broker|一种帮助开发人员生成安全的可缩放数据库应用程序的技术。|  
|SQL Server Store for Office Applications|一种 SQL Server 功能，支持将数据存储于 SQL Server 上的 Office 应用程序中。|  
|SQL Server 跟踪 (SQL Server Trace)|一组 Transact-SQL 系统存储过程，用于在 SQL Server 数据库引擎的实例上创建跟踪。|  
|SQL Server 实用工具|一种组织和监视 SQL Server 资源运行状况的方法。 它使管理员具有其环境的历史视图。|  
|SQL Server 实用工具面板 (SQL Server Utility dashboard)|一个面板，可提供托管的 SQL Server 实例和数据层应用程序的资源运行状况的快速摘要。 还可以指 SQL Server 实用工具详细视图或带有详细信息的列表视图。|  
|SQL Server 实用工具资源管理器 (SQL Server Utility Explorer)|一种显示 SQL Server 实用工具中的对象的层次结构树。|  
|SQL Server 实用工具视点 (SQL Server Utility viewpoints)|SQL Server 实用工具的一个功能，通过用作实用工具控制点 (UCP) 的 SQL Server 实例向管理员提供反映资源在一段时间中的运行状况的视图。|  
|SQL 语句|对数据执行某种操作的 SQL 或 Transact-SQL 命令，例如 SELECT 或 DELETE。|  
|SQL 跟踪|一组 Transact-SQL 系统存储过程，用于在 SQL Server 数据库引擎的实例上创建跟踪。|  
|SQL Writer|SQL Server 提供的符合 VSS 的编写器，用于处理 VSS 与 SQL Server 的交互。|  
|SQL 编写器服务|一种服务，允许 Windows 备份程序通过卷影复制服务框架在 SQL Server 正在运行时复制 SQL Server 数据文件。|  
|SQL-92|1992 年发布的 SQL 标准版。|  
|SSAS|Microsoft SQL Server 的一个功能，为商业智能应用程序提供联机分析处理 (OLAP) 和数据挖掘支持。 Analysis Services 将来自数据仓库的数据组织到具有预先计算的聚合数据的多维数据集中，从而快速响应复杂的分析查询。|  
|SSL|一种通过结合使用数据加密、数字证书和公钥密码系统提高数据通信安全性的协议。 SSL 支持在网络中进行身份验证并增强数据安全性和隐私。 SSL 不提供授权或不可否认性。|  
|SSRCT|一种工具，DPM 可以利用该工具通过创建和管理 DPM 角色（用户、对象和权限的分组）授权最终用户执行数据的自助式恢复。|  
|SSRS|一种基于服务器的报表生成环境，它提供企业级的 Web 报表功能，从而使您可以创建从多个数据源提取数据的表，发布各种格式的表，以及集中管理安全性和订阅。|  
|SSRT|一种工具，最终用户可以使用该工具恢复来自 DPM 的备份，而无需 DPM 管理员执行任何操作。|  
|临时数据 (staged data)|在 SQL Server Master Data Services 的临时过程中导入到临时表中的数据。|  
|staging|SQL Server Master Data Services 中用于将数据导入到临时表中，然后在将临时数据导入到 master 数据库之前将其作为批进行处理的过程。|  
|临时过程 (staging process)|SQL Server Master Data Services 中用于将数据导入到临时表中，然后在将临时数据导入到 master 数据库之前将其作为批进行处理的过程。|  
|临时队列 (staging queue)|SQL Server Master Data Services 中的批处理表，其中，临时记录排队为批处理以等待处理到 Master Data Services 数据库中。|  
|临时表 (staging table)|SQL Server Master Data Services 中在临时处理过程内用业务数据进行填充的表。|  
|独立服务器 (standalone server)|运行 Windows Server 但不参与域的计算机。 独立服务器只有其自己的最终用户数据库，它自行处理登录请求。 它不与任何其他计算机共享帐户信息，无法提供对域帐户的访问。|  
|备用文件 (standby file)|在还原操作中的撤消阶段，用来保存要修改页面的“写入时复制”预映像的文件。 通过备用文件可以还原撤消过程，以索回未提交的事务。|  
|备用服务器 (standby server)|包含数据库副本的服务器实例，如果源数据库不可用，可以使该数据库副本联机。  日志传送可用于维护“温”备用服务器（称为辅助服务器），其数据库副本定期自动从日志备份中进行更新。 在向温备用服务器执行故障转移之前，必须手动完全更新其数据库副本。 可以使用数据库镜像来维护热备用服务器（称为镜像服务器），其数据库副本将持续保持最新。 向镜像服务器上的数据库进行故障转移基本上是瞬间完成的。|  
|现有查询 (standing query)|在 StreamInsight 服务器内运行的针对传入事件执行连续计算的查询模板的实例化。|  
|星型联接 (star join)|一个事实数据表（通常为大型事实数据表）与至少两个维度表之间的联接。|  
|星型查询 (star query)|将一个事实数据表与多个维度表相联接的查询。|  
|星型架构 (star schema)|一种关系数据库结构，其中数据保存在架构中心的一个事实数据表中，而其他维度数据存储在维度表中。 每个维度表按键列直接与事实数据表相关并通常联接到事实数据表。|  
|开始角度 (start angle)|介于 0 至 360 之间的旋转角度，是刻度的起始位置。 位置零 (0) 位于仪表的底部，开始角度按顺时针方向旋转。 例如，如开始角度为 90 度，将使刻度从 9 点钟位置开始。|  
|起始线帽 (start cap)|线条的起点。|  
|语句|已编译的 T-SQL 查询。|  
|静态游标 (static cursor)|按照其打开时结果集所处的状态来显示结果集的一种游标。|  
|静态行筛选器 (static row filter)|一种可用于所有复制类型的筛选器，允许基于 WHERE 子句限制复制到订阅服务器上的数据。|  
|stemmer|在全文搜索中，对于某种给定的语言，词干分析器可基于该语言的规则生成某个特定词的变形形式。 词干分析器特定于语言。|  
|单步执行|若要执行当前语句并进入中断模式，只要出现对另一个过程的调用，就会逐语句执行下一个过程。|  
|管理门户 (stewardship portal)|MDS 的一项功能，它对包括成员和层次结构在内的主数据提供集中控制，并使数据模型管理员能够通过开发、审核、管理数据模型并跨域一致地落实这些模型来确保数据质量。|  
|单品 (stock keeping unit)|产品的唯一标识符（通常为字母）。 通过 SKU 可以跟踪产品来维护库存。 SKU 可以与可采购的任何物料关联。 例如，样式编号为 3726 和尺码为 8 的衬衣的 SKU 可能为 3726-8。|  
|偷取的页 (stolen page)|缓冲区高速缓存中被其他服务器请求占用的页|  
|非索引字表 (stoplist)|所谓的非索引字的特定集合，非索引字通常频繁出现在文档中但被认为并没有传达有用的信息。|  
|非索引字 (stopword)|通常频繁出现在文档中但并没有传达有用信息的字词。|  
|存储引擎 (storage engine)|SQL Server 的一个组件，负责管理数据库中的原始物理数据。  例如，向磁盘读取数据就是一个由存储引起处理的任务。|  
|存储位置|可以在其中找到特定项的位置：磁盘、磁带或类似介质上的寻址位置或唯一标识的位置。|  
|存储过程|SQL 语句和可选控制流语句的预编译集合，以一个名称存储并作为一个单元处理。 它们存储在 SQL 数据库中，并可以通过来自应用程序的一个调用而运行。|  
|存储过程冲突解决程序 (stored procedure resolver)|所调用的用于处理基于行更改的冲突的程序（这些冲突是在冲突解决程序所注册到的项目中遇到的）。|  
|流 (stream)|字节序列的抽象，例如文件、I/O 设备、进程中通信管道、TCP/IP 套接字或进行后台处理的打印作业。 复合文件中流与存储之间的关系类似于文件与文件夹之间的关系。|  
|流使用者 (stream consumer)|使用查询输出的结构或设备。 示例包括：输出适配器或另一个运行的查询。|  
|StreamInsight 事件流调试器 (StreamInsight Event Flow Debugger)|Microsoft StreamInsight 平台上用于提供事件流调试和分析功能的独立工具。|  
|StreamInsight 平台 (StreamInsight platform)|该平台由 StreamInsight 服务器、事件流调试工具、Visual Studio IDE 和其他组件构成，用于开发复杂事件处理应用程序。|  
|StreamInsight 服务器 (StreamInsight server)|Microsoft StreamInsight 的核心引擎和适配器框架组件。 StreamInsight 服务器可用于处理和分析与复杂事件处理应用程序关联的事件流。|  
|字符串|作为单个实体进行处理的一组字符或字符字节。 计算机程序使用字符串来存储和传送数据和命令。 大多数编程语言将字符串（如 2674:gstmn）视为与数值（如 470924）截然不同。|  
|条带线 (strip line)|按固定或自定义间隔设置图表背景模式的水平或垂直区域。 您可以使用条带线改进可读性以便查找图表上的各个值，突出显示定义发生的日期或突出显示特定的键范围。|  
|带状线 (stripe)|按固定或自定义间隔设置图表背景模式的水平或垂直区域。 您可以使用条带线改进可读性以便查找图表上的各个值，突出显示定义发生的日期或突出显示特定的键范围。|  
|条带介质集 (striped media set)|使用多个设备的一种介质集，将在这些设备之间分发每个备份。|  
|强一致性 (strong consistency)|支持高可用性并且缓存群集中有缓存对象的多个副本的方案。 该对象的所有副本保持完全相同。|  
|结构化查询语言 (Structured Query Language)|一种数据库查询和编程语言，广泛用于访问、查询、更新和管理关系数据库系统中的数据。|  
|子查询|包含一个或多个子查询的 SELECT 语句。|  
|子报表 (subreport)|包含在另一个报表中的报表。|  
|subscribe|从发布服务器请求数据。|  
|subscriber|在 Notification Services 中，向其传递通知的人或进程。|  
|subscriber|在复制中，接收复制数据的数据库实例。|  
|订阅服务器数据库 (subscriber database)|在复制中，接收复制数据的数据库实例。|  
|订阅服务器 (subscribing server)|一种运行 Analysis Services 实例的服务器，用来存储链接的多维数据集。|  
|订阅|请求将发布的副本发送给订阅服务器。|  
|订阅数据库 (subscription database)|订阅服务器上的一个数据库，接收发布服务器所发布的数据和数据库对象。|  
|订阅事件规则 (subscription event rule)|处理事件驱动订阅信息的规则。|  
|订阅预定规则 (subscription scheduled rule)|处理预定订阅的信息的一个或多个 Transact-SQL 语句。|  
|子集 (subset)|由多个表和这些表之间的关系行组成的一个选集，它是大型数据库关系图的一部分。|  
|减 (subtract)|执行从其他内容中减去某个内容的基本数学操作。|  
|支持计数|一个动态选项，显示决定列值决定依赖列的行数。|  
|支持百分比|一个动态选项，显示决定列决定依赖列的行数的百分比。|  
|外围应用 (surface area)|一个软件可以被攻击的多种方式。|  
|可疑磁带 (suspect tape)|具有冲突的标识信息（如条码或介质上的标识符）的磁带。|  
|SVF|一个函数，它返回单个值，如字符串、整数或位值。|  
|SVG|一种基于 XML 的语言，用于编写二维图像独立于设备的说明。 当打印或使用不同屏幕大小和分辨率进行查看时，SVG 图像保持其外观。 SVG 是万维网联盟 (W3C) 推荐采用的语言。|  
|扫描角度 (sweep angle)|刻度将在一个圆周中所跨的度数（介于 0 至 360 之间）。 扫描角度为 360 度将生成为一个完整圆的刻度。|  
|切入表 (switch in table)|用户要用于切入其数据的临时表。 需要先创建此临时表，然后才能使用管理分区向导切换分区。|  
|切出表 (switch out table)|用户要用于从当前源表切出的分区的临时表。|  
|对称密钥 (symmetric key)|在发布和使用期间，用于同时对受保护的内容进行加密和解密的密钥。|  
|同步管理器 (Sync Manager)|一种用于确保客户端计算机上的文件或目录与服务器上的相应文件或目录包含相同数据的工具。|  
|同步访问接口 (sync provider)|允许副本与其他副本同步其数据的软件组件。|  
|同步应用程序 (synchronization application)|一个软件组件（如个人信息管理器或音乐数据库），其中承载着同步会话并调用同步访问接口以同步不同的数据存储区。|  
|同步社区 (synchronization community)|使其数据相互保持同步的一组副本。|  
|同步管理器 (synchronization manager)|一种用于确保客户端计算机上的文件或目录与服务器上的相应文件或目录包含相同数据的工具。|  
|同步管理器 (synchronization manager)|一种用于确保客户端计算机上的文件或目录与服务器上的相应文件或目录包含相同数据的工具。|  
|同步业务流程 (synchronization orchestrator)|启动和控制同步会话的业务流程。|  
|同步提供程序 (synchronization provider)|允许副本与其他副本同步其数据的软件组件。|  
|同步会话 (synchronization session)|一个单向同步过程，其中，源提供程序枚举其更改，并将更改发送到目标提供程序，并由后者将更改应用到其存储区。|  
|联合格式 (syndication format)|一种用于在博客和网站上发布数据的格式。|  
|语法验证 (syntactic validation)|确认 XML 文件符合其架构的过程。|  
|系统配置检查器 (System Configuration Checker)|一个系统准备工具，通过在安装软件应用程序之前验证目标计算机来避免出现安装失败。|  
|系统数据库|所有 SQL Server 实例中都存在的五个数据库，用于存储系统信息。|  
|系统函数|一组内置函数，用于对 SQL Server 中的值、对象和设置执行操作，并返回有关它们的信息。|  
|系统区域设置 (system locale)|一个“区域和语言选项”设置，为特定计算机指定默认代码页和关联的位图字体文件，此设置影响特定计算机的所有用户。 通过指定默认代码页和字体，为一种操作系统语言版本编写的非 Unicode 应用程序可以直接在其他操作系统语言版本上正确运行。|  
|系统角色分配 (system role assignment)|作为一个整体应用于站点的角色分配。|  
|系统角色定义 (system role definition)|传达站点范围的授权的角色定义。|  
|系统存储过程 (system stored procedure)|一种存储过程，支持运行 SQL Server 系统所需的所有管理任务。|  
|系统存储过程|SQL Server 提供的一组存储过程，可以用于诸如从系统目录中检索信息或执行管理任务之类的操作。|  
|系统表 (system table)|存储用于定义服务器配置及其所有表的数据的表。|  
|系统表|构成 SQL Server 系统目录的内置表。|  
|系统变量 (system variable)|DTS 提供的变量。|  
|选项卡页 (tab page)|选项卡控件的一部分，由选项卡用户界面元素和显示区域组成，充当数据或其他控件（如文本框、组合框和命令按钮）的容器。|  
|表|在记录（行）和字段（列）中存储数据的数据库对象。 这些数据通常是关于特定事物类别（如员工或订单）的。|  
|表数据区域 (table data region)|报表布局中以分列格式显示数据的报表项。|  
|表设计器|一种可视的设计图面，用于创建和编辑 TSQL 表和表相关的对象。|  
|表锁 (table lock)|针对包括所有数据和索引的表的锁。|  
|表引用 (table reference)|解析为表的名称、表达式或字符串。|  
|tablespace|数据库存储单元，大致等同于 SQL Server 中的文件组。 表空间允许存储和管理各个组内的数据库对象。|  
|表值函数 (table-valued function)|返回表的用户定义函数。|  
|Tablix|可以用表、矩阵和列表格式呈现数据的数据区域。 其目的是提供数据区域对象的独特功能和用户组合数据格式的能力。|  
|Tablix 数据区域|可以用表、矩阵和列表格式呈现数据的数据区域。 其目的是提供数据区域对象的独特功能和用户组合数据格式的能力。|  
|表格格式数据流|SQL Server 内部客户端/服务器数据传输协议。 TDS 允许客户端产品和服务器产品独立于操作系统平台、服务器版本或网络传输来进行通信。|  
|表格查询 (tabular query)|诸如对表中数据进行搜索、排序、筛选或转换等的标准操作。|  
|结尾日志备份 (tail-log backup)|从可能已损坏的数据库中提取的日志备份，用来捕获尚未备份的日志。 失败后执行结尾日志备份，以防丢失所做的工作。|  
|磁带备份 (tape backup)|一种可以向操作系统支持的任何磁带设备写入数据的 SQL Server 备份操作。|  
|目标|对其执行操作的数据库。|  
|目标分区 (target partition)|一种 Analysis Services 分区，用来合并另一个分区，并且合并之后将包含这两个分区的数据。|  
|目标队列 (target queue)|在 Service Broker 中，与要向其发送消息的服务关联的队列。|  
|目标服务器 (target server)|从主服务器接收作业的服务器。|  
|目标类型 (target type)|目标的类型，它具有某些特征和行为。|  
|任务对象 (task object)|一个 Data Transformation Services (DTS) 对象，将要执行的各项工作定义为数据转换过程的一部分。 例如，某个任务可以执行一条 SQL 语句，或使用 DTS 数据抽取将 OLE DB 源中的异构数据移动和转换至 OLE DB 目标。|  
|TDS|SQL Server 内部客户端/服务器数据传输协议。 TDS 允许客户端产品和服务器产品独立于操作系统平台、服务器版本或网络传输来进行通信。|  
|临时智能卡 (temporary smart card)|向用户签发的用于取代丢失的智能卡或要求限时访问的非永久性智能卡。|  
|临时存储过程 (temporary stored procedure)|放置在临时数据库 tempdb 中的过程，会话结束时将被清除。|  
|临时表 (temporary table)|放置在临时数据库 tempdb 中的表，会话结束时将被清除。|  
|tenant|Web 服务通过应用程序的单个实例提供服务的客户端组织。 公司可以在一组服务器上安装软件的一个实例，并将向多个租户提供 Software as a Service（软件即服务）。|  
|影院视图 (theater view)|一种视图，通过此视图，预览可在 PowerPivot 库的 SharePoint 文档库中居中显示，并且您可以循环访问可用的工作表。 每个工作表的较小缩略图显示在页面任一侧的下方。|  
|theta 联接 (theta join)|基于对标量值进行比较的联接。|  
|千位分隔符 (thousand separator)|将在小数点分隔符左侧具有四位或更多位数的数字中的千位和百位分隔开。|  
|线程 (thread)|进程内一种运行程序指令的对象类型。 如果使用多个线程，则可以在进程中执行并发操作，并且一个进程可以在不同处理器上同时运行其程序的不同部分。 线程在其进程的地址空间中具有自己的一组寄存器、其自己的内核堆栈、一个线程环境块和一个用户堆栈。|  
|中止 (throttle)|一个 Microsoft SQL Server 工具，用于当同时处于活动状态的操作超过八个时限制数据库引擎实例的性能。|  
|时钟周期|时钟电路发出的快速重复发生的定期信号。|  
|时钟周期 (tick count)|一个单调递增的数字，用于唯一标识对副本中某项所做的某次更改。|  
|图块服务器 (tile server)|一个地图图像缓存引擎，用于缓存和提供预先生成的固定大小的地图图像图块。|  
|time|一种 SQL Server 系统数据类型，用于存储从 0:00 到 23:59:59.999999 的时间值。|  
|时间间隔 (time interval)|给定事件在其中有效的时间段。 有效的时间间隔包括有效的开始时间和构成时间段的所有瞬间，但不包括有效的结束时间。|  
|词汇切分 (tokenization)|在文本挖掘或全文搜索中，标识字符串内（在词边界、词素或词干处）有意义的单元以便可以对相关标记进行分组的过程。 例如，尽管“San Francisco”是两个词，但可以将其视为一个标记。|  
|逻辑删除 (tombstone)|用于表示和跟踪已删除项的标记，可防止将此项意外重新引入到同步社区中。|  
|工具 (tool)|协助完成一个或一组任务的实用工具或功能。|  
|拓扑|涉及同步的一组参与者以及参与者之间相互连接的方式。|  
|跟踪|数据库引擎返回的事件和数据的集合。|  
|跟踪文件 (trace file)|包含指定对象（如应用程序、操作系统或网络）的活动记录的文件。 跟踪文件包含对 API 进行的调用、API 的活动、通信链接和内部流的活动以及其他信息。|  
|跟踪令牌 (tracer token)|一种性能监视工具，可用于进行事务复制。 令牌（少量数据）通过复制系统进行发送，以测量事务到达分发服务器和订阅服务器所需的时间量。|  
|尾字节 (trail byte)|双字节字符中后面一半的字节值。|  
|定型 (train)|用数据填充模型，以便派生出可在预测或知识发现中使用的模式。|  
|定型数据集 (training data set)|一组已知的可预测数据，用于为数据挖掘模型定型。|  
|特征 (trait)|用于描述实体的一种属性。|  
|特征短语 (trait phrasing)|一种表示次要实体描述主要实体的关系的方法。|  
|事务隔离级别 (transaction isolation level)|事务的属性，用于控制隔离数据以供一个进程使用并防止其他进程干扰的程度。|  
|事务日志 (transaction log)|记录在数据库中发生的事务变化并提供用于更新主文件和建立审核跟踪的基础的文件。|  
|事务日志备份 (transaction log backup)|包括以前日志备份中未备份的所有日志记录的事务日志备份。 在完整恢复模式或大容量日志恢复模式下需要进行日志备份，但在简单恢复模式下不可用。|  
|事务保持期 (transaction retention period)|事务复制中事务存储在分发数据库中的时间，|  
|事务回滚 (transaction rollback)|将用户指定的事务回滚到事务内的上一个保存点或事务开头。|  
|事务数据 (transactional data)|与销售、交货、发票、故障标记、索赔以及其他货币相关和货币不相关交互关联的数据。|  
|事务复制|一种通常从发布数据库对象和数据的快照开始复制的复制类型。|  
|Transact-SQL|一种语言，包含用来管理 SQL Server 实例、在 SQL Server 实例中创建和管理所有对象，以及在 SQL Server 表中插入、检索、修改和删除所有数据的命令。 Transact-SQL 是对国际标准化组织 (ISO) 和美国国家标准学会 (ANSI) 发布的 SQL 标准中所定义的语言的一种扩展。|  
|转换|用于修改、汇总和清除数据的 SSIS 数据流组件。|  
|转换输入 (transformation input)|列中包含的数据，在联接或查找过程中用来修改或聚合它要联接的表中的数据。|  
|转换输出 (transformation output)|作为转换过程的结果返回的数据。|  
|趋势|一般趋势或走向，通常通过考察特殊属性随时间变化的规律来确定。|  
|可信连接|只能由已通过网络身份验证的用户打开的 Windows 网络连接。|  
|TSQL 窗格 (TSQL pane)|一种选项卡，用于承载编辑器控件以便允许 TSQL 代码编辑。|  
|翻转窗口 (tumbling window)|其跳跃大小等于窗口大小的跳跃窗口。|  
|tuple|根据多维数据集的每个属性层次结构中属性成员的组合唯一标识一个单元的有序成员集合。|  
|两阶段提交|确保应用于多个服务器的事务在所有服务器上都完成或都未完成的协议。 两阶段提交由事务管理器协调并且受到资源管理器的支持。|  
|类型检查 (type checking)|由编译器或解释器执行的过程，用于确保当使用某个变量时，该变量的数据类型与声明它时的数据类型相同。|  
|特型适配器 (typed adapter)|仅发出一个事件类型的适配器。|  
|特型事件 (typed event)|一种事件，对于此事件而言，源提供或接收器使用的事件负载的结构为已知的，并且将根据此特定事件结构设计输入或输出适配器。|  
|UCP|为 SQL Server 实用工具提供中心原因点的网络节点。 它使用 SQL Server Management Studio (SSMS) 中的实用工具资源管理器组织和监视 SQL Server 资源的运行状况。|  
|UDT|用户编写的对 SQL Server 中的标量类型系统的扩展。|  
|非均衡层次结构 (unbalanced hierarchy)|一种层次结构，其中一个或多个分支中的一个或多个级别不包含成员。|  
|未绑定流 (unbound stream)|包含事件模型或负载类型的定义但不定义数据源的事件流。|  
|不可提交的 (uncommittable)|所涉及的是保持打开状态但无法完成的事务。 无法提交的事务可被视为部分失败的事务的子类，其中事务遇到了阻止其完成的错误，但它仍保留其锁且必须由用户进行回滚。|  
|解压缩 (uncompress)|将压缩文件的内容还原为其原始格式。|  
|无法传递 (undeliverable)|无法传递给目标收件人。 如果无法传递电子邮件，则电子邮件将返回给发件人，并且邮件服务器将添加说明问题的信息；例如，电子邮件地址可能不正确，或者收件人的邮箱可能已满。|  
|基础表 (underlying table)|由视图、游标或存储过程引用的表。|  
|撤消 (undo)|数据库恢复过程中的一个阶段，在此阶段，将取消（回滚）在恢复的重做阶段完成时仍未提交的所有事务所做的更改。|  
|撤消文件 (undo file)|当未提交的回滚事务修改了数据库中页面的内容后，但在恢复操作将内容还原到其先前状态之前，保存这些内容的文件。 撤消文件可防止丢失由未提交的事务执行的更改。|  
|撤消阶段 (undo phase)|数据库恢复过程中的一个阶段，在此阶段，将取消（回滚）在恢复的重做阶段完成时仍未提交的所有事务所做的更改。|  
|非强制关系 (unenforced relationship)|表之间的一种联系，将一个表中的主键与另一个表中的外键关联起来，并且在 INSERT 和 UPDATE 事务执行期间不检查引用完整性。|  
|取消初始化 (uninitialize)|更改枚举器或数据源对象的状态，以便其无法用于访问数据。|  
|唯一索引 (unique index)|一种索引，采用这种索引时各行的索引值必须都不相同，因而可禁止出现索引或键值重复的情况。|  
|uniqueifier|一个占用 4 个字节的列，由 SQL Server 数据库引擎自动添加到行中，以使每个索引键保持唯一。|  
|通用协调时间 (Universal Time Coordinate)|世界上每个地方通用的标准时间，由国际计量局 (International Bureau of Weights and Measures) 进行协调。 通用协调时间用于同步 Internet 上的计算机。|  
|未知成员 (unknown member)|一种维度成员，在处理包含该维度的多维数据集的过程中，未找到其任何键。|  
|未知磁带 (unknown tape)|DPM 服务器尚未识别的磁带。|  
|非托管代码 (unmanaged code)|由操作系统在 .NET Framework 的公共语言运行时之外直接执行的代码。 非托管代码必须提供其自己的内存管理、类型检查和安全性支持，这一点与托管代码不同，后者从公共语言运行时接收这些服务。|  
|非托管实例 (unmanaged instance)|实用工具控制点不监视的 SQL Server 实例。|  
|逆透视 (unpivot)|将来自单个记录中多个列的值扩展为单个列中具有同样值的多个记录。|  
|不安全代码 (unsafe code)|由操作系统在 .NET Framework 的公共语言运行时之外直接执行的代码。 非托管代码必须提供其自己的内存管理、类型检查和安全性支持，这一点与托管代码不同，后者从公共语言运行时接收这些服务。|  
|泛型适配器 (untyped adapter)|接受或发出多个事件类型（其中的负载结构或负载中的字段类型并非事先已知）的适配器。 示例包括：来自 CSV 或文本文件、SQL 表或套接字的事件。|  
|更新锁 (update lock)|加在可更新的资源（例如行、页、表）上的锁。|  
|更新统计信息 (update statistics)|重新计算有关指定索引中的键值分布的信息的过程。|  
|updategram|这是一种模板，通过此模板，可以在 Microsoft SQL Server 中通过现有 XML 文档修改数据库。|  
|用户帐户 (user account)|在 Active Directory 中，一个包含用于定义域用户的所有信息的对象，这些信息包括用户名、密码以及该用户帐户在其中具有成员资格的组。 用户帐户可以存储在 Active Directory 中或本地计算机上。|  
|用户数据库 (user database)|SQL Server 用户创建的用于存储应用程序数据的数据库。|  
|用户实例 (user instance)|由父实例代表用户生成的 SQL Server Express 实例。|  
|用户定义聚合函数 (user-defined aggregate function)|通过引用 SQL Server 程序集创建的一种聚合函数，其实现是在 .NET Framework 公共语言运行时中所创建的某个程序集中定义的。|  
|用户定义类型 (user-defined type)|用户编写的对 SQL Server 中的标量类型系统的扩展。|  
|实用工具控制点|为 SQL Server 实用工具提供中心原因点的网络节点。 它使用 SQL Server Management Studio (SSMS) 中的实用工具资源管理器组织和监视 SQL Server 资源的运行状况。|  
|实用工具读取者 (Utility Reader)|允许用户帐户连接到 SQL Server Utility、在 SSMS 中的实用工具资源管理器中查看所有视点以及在 SSMS 中的实用工具资源管理器中查看“实用工具管理”节点的设置的权限。|  
|vacuumer|用于删除数据的工具。|  
|有效期 (validity period)|已定义的凭据被认为可信的时间段。|  
|值表达式 (value expression)|将返回值的多维表达式 (MDX)。 值表达式可以对集、元组、成员、级别、数字或字符串进行运算。|  
|版本|一个用于区分缓存中存储的使用相同键的对象的属性。 Windows Server AppFabric 使用 DataCacheItemVersion 类存储版本信息。 每次在缓存中添加或更新对象时，版本值都会更改。 版本控制用于维护数据一致性。 乐观并发是使用版本控制而非锁来实现的。|  
|版本|标识对副本中的某个项进行的更改的元数据。 它由该项的副本键和副本时钟周期数组成。|  
|垂直筛选 (vertical filtering)|筛选表中的列。 当在复制过程中使用筛选时，创建的表项目将只包含所发布表中的选定列。|  
|垂直分区 (vertical partitioning)|基于选定的列将单个表拆分为多个表的过程。 多个表中的每一个都具有相同的行数，但列数较少。|  
|垂直拆分 (vertical split)|CIDER Shell 的垂直方向。|  
|特大型数据库 (very large database)|一种变得非常大并造成管理难题，需要引起人员和流程额外关注的数据库。|  
|牺牲品 (victim)|当 tempdb 用完了空间且数据库引擎强制版本存储区收缩时，尚未生成行版本的运行时间最长的事务。 在错误日志中为每个作为牺牲品的事务生成消息 3967。 如果某个事务被标记为牺牲品，则该事务不能再读取版本存储区中的行版本。|  
|视图生成 (view generation)|一种存储库引擎功能，用来基于信息模型中的类、接口和关系创建关系视图。|  
|虚拟日志文件 (virtual log file)|SQL Server 数据库引擎根据某个物理日志文件得出的非物理文件。|  
|直观合计 (visual total)|某一维度成员显示的聚合单元值，它与该成员的显示子级显示的单元值一致。|  
|可视化程序 (visualizer)|一种在调试模式下直观表示数据的方式。|  
|VLDB|一种变得非常大并造成管理难题，需要引起人员和流程额外关注的数据库。|  
|VSS Writer|应用程序内的一个组件，它在备份期间与 VSS 平台基础结构交互，以确保应用程序数据准备就绪，可创建快照。|  
|实际时间 (wall-time)|计算机完成某项任务所需的总时间，这是 CPU 时间、I/O 时间和通信信道延迟的总和。|  
|热延迟 (warm latency)|在工作流类型已编译时用于创建新的工作流实例的时间。|  
|热备用状态 (warm standby)|一种冗余方法，其中辅助（也即备份）系统在主系统的后台运行。 数据定期镜像到辅助服务器，这意味着两台服务器有时并不包含完全相同的数据。|  
|温备用服务器 (warm standby server)|包含异步更新的数据库副本且能以相当快的速度使该副本联机的备用服务器。|  
|水印 (watermark)|用于管理每个缓存主机上的内存消耗量的阈值。 高水印和低水印指定何时将对象逐出内存。|  
|Web 应用程序|一种软件程序，它将超文本传输协议 (HTTP) 用作其核心通信协议，并通过超文本标记语言 (HTML) 将基于 Web 的信息传递给用户。|  
|Web 池 (Web pool)|工作进程提供的一个或多个 URL 的分组。|  
|Web 池代理 (Web Pool Agent)|Certificate Lifecyle Manager (CLM) Web 门户在其中运行的隔离进程。|  
|Web 项目 (Web project)|指定 Web 应用程序的元素的一组文件。|  
|网站|HTTP 服务器在万维网或 Intranet 上托管的一组相关网页。 网站中的网页通常涵盖一个或多个主题，并通过超链接相互连接。|  
|Web 同步|在合并复制中，是指允许使用 HTTPS 协议复制数据的一种功能。|  
|网站 (website)|HTTP 服务器在万维网或 Intranet 上托管的一组相关网页。 网站中的网页通常涵盖一个或多个主题，并通过超链接相互连接。|  
|加权收盘价公式 (weighted close formula)|计算高价、低价和收盘价的平均值的公司，同时给予收盘价额外的权重。|  
|宽字符 (wide character)|由两个字符组成的多语言字符代码。|  
|window|流中属于某个时间段的事件的子集；即：包含沿时间线的事件数据的窗口。|  
|Windows Management Instrumentation|Microsoft 对 Distributed Management Task Force (DMTF) Web-based Enterprise Management (WBEM) 计划的扩展。|  
|Windows NT 集成安全性 (Windows NT Integrated Security)|一种利用 Windows NT 身份验证进程的安全模式。|  
|见证服务器 (witness server)|在数据库镜像中，是指负责监视主体服务器和镜像服务器状态，并且默认情况下在主体服务器出现故障时可以启动自动故障转移的服务器实例。 数据库镜像会话只能有一个可选的见证服务器（或“见证”）。|  
|WMI|Microsoft 对 Distributed Management Task Force (DMTF) Web-based Enterprise Management (WBEM) 计划的扩展。|  
|WMI 查询语言 (WMI Query Language)|ANSI SQL 的一个子集，进行了适合 Windows Management Instrumentation (WMI) 的语义更改。|  
|工作簿|在电子表格程序中，指包含许多相关工作表的文件。|  
|工作负荷调控器 (workload governor)|一个 Microsoft SQL Server 工具，用于当同时处于活动状态的操作超过八个时限制数据库引擎实例的性能。|  
|工作负荷组|在资源调控器中，根据应用于每个请求的分类规则被认为是相似的会话请求的容器。 利用工作负荷组可对资源占用进行聚合监视并可将统一策略应用至组中的所有请求。|  
|工作站 (workstation)|连接到网络的微计算机或终端。|  
|WQL|ANSI SQL 的一个子集，进行了适合 Windows Management Instrumentation (WMI) 的语义更改。|  
|写回 (write back)|更新某个多维数据集的单元值、成员或成员属性值。|  
|预写日志 (write-ahead log)|一种事务日志记录方法，始终先写入日志再写入数据。|  
|x 轴 (x-axis)|网格、图表或图形上具有水平和垂直维度的水平参考线。|  
|XML for Analysis|一种规范，描述支持对驻留在万维网上的数据源进行数据访问的开放标准。|  
|XMLA|一种规范，描述支持对驻留在万维网上的数据源进行数据访问的开放标准。|  
|XQuery|一种函数查询语言，广泛适用于各种从 Quilt、XPath 和 XQL 派生的 XML 数据类型。 Ipedo 和 Software AG 分别针对 XQuery 语言实现了自己的 W3C 建议规范版本。 也称为 XML 查询和 XQL。|  
|XSL|一个 XML 词汇表，用来通过定义呈现规则的样式表将 XML 数据转换为其他形式（如 HTML）。|  
|XSL 转换 (XSL Transformation)|一种基于 XML 的声明语言，用于显示或转换 XML 数据。|  
|XSLT|一种基于 XML 的声明语言，用于显示或转换 XML 数据。|  
  
  
