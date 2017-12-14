---
title: "SQL Server 2012 SP4 发行说明 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: sql-non-specified
ms.technology: server-general
ms.custom: 
ms.date: 10/05/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 67cb8b3e-3d82-47f4-840d-0f12a3bff565
caps.latest.revision: "0"
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7aed12a3e687ab4c8b42b8f07c29d252e0d6acad
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2017
---
# <a name="sql-server-2012-sp4-release-notes"></a>SQL Server 2012 SP4 发行说明
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]本主题总结了 SQL Server 2012 SP4 中所包含的改进。 该主题还描述了安装 SP4 或对其安装进行故障排除之前需要查看的问题。 发行说明仅在线提供，不提供相关安装介质。 本主题会在发现问题时定期更新。 有关 SP4 中修补程序的详细列表，请参阅 [SQL Server 2012 SP4 版本信息](https://go.microsoft.com/fwlink/?linkid=846937)。  

> 服务包 4 包含所有 SQL Server 2012 SP3 累积更新。
  
##<a name="download-pages"></a>下载页面
以下项链接到了 SQL Server 2012 SP3 的主要下载包。 下载页包含系统要求和基本安装说明。
- [SQL Server 2012 SP4 修补程序安装](https://go.microsoft.com/fwlink/?linkid=846829)
- [SQL Server 2012 SP4 Express](https://go.microsoft.com/fwlink/?linkid=846905)
- [Microsoft SQL Server 2012 SP4 功能包](https://go.microsoft.com/fwlink/?linkid=846907)

##  <a name="sp4-performance-and-scale-improvements"></a>SP4 性能和缩放性方面的改进

- 改进了分发代理清除过程 - 过大的分发数据库会导致发生阻塞和死锁情况。 改进的清理过程旨在消除其中某些阻塞或死锁情况的发生。 
- 动态内存对象缩放 - 基于大量的节点和内核对内存对象进行动态分区，从而缩放现代硬件。 动态升级旨在防止潜在的瓶颈并对线程安全内存对象进行自动分区。 未分区的内存对象可进行动态升级，以便按节点分区。 分区数等于 NUMA 节点数。 可进一步提升按节点分区的内存对象，使其按 CPU 分区，其中分区数等于 CPU 数。
- 为缓冲池启用 8 TB 以上的内存 - 为缓冲池的使用启用了 128-TB 的虚拟地址空间
- **更改跟踪清除** - 改进了更改跟踪端表的更改跟踪清除性能和效率。 

## <a name="sp4-supportability-and-diagnostics-improvements"></a>SP4 可支持性和诊断改进

- 对复制代理的完全转储支持 - 如果复制代理现在遇到未经处理的异常，则会默认创建异常现象的微型转储。 此默认行为要求对未经处理的异常执行复杂的故障排除步骤。 SP4 引入了一个新的注册表项，支持为复制代理创建完全转储。
- 增强了 showplan XML 中的诊断 - Showplan XML 已得到增强，公开了以下相关信息：已启用的跟踪标志、用于优化的嵌套循环联接的内存部分、CPU 时间和运行时间。 
- 加强了 XE 和 DMV 诊断之间的相关性 - 仅 Query_hash 和 query_plan_hash 字段用于标识查询。 DMV 将二者定义为 varbinary(8)，而 XEvent 将其定义为 UINT64。 由于 SQL Server 不具有“unsigned bigint”，因此强制转换并非始终有效。 这一改进引入了等效于 query_hash 和 query_plan_hash 的新 XEvent 操作/筛选器列，除非二者定义为有助于关联 XE 和 DMV 之间的查询的 INT64。 
- 增强了内存授予/使用诊断 - 新的 query_memory_grant_usage XEvent（移植自 Server 2016 SP1）
- 将协议跟踪添加到 SSL 协商步骤 - 添加了成功/失败的协商的一些跟踪信息，包括协议等。在部署 TLS 1.2（以此为例）的情况下，对连接方案进行故障排除时很有用
- 为分发数据库设置正确的兼容性级别 - 安装服务包后，分发数据库兼容级别会更改为 90。 由于 sp_vupgrade_replication 存储过程中的问题，因此对级别进行了更改。 SP 现已改为设置分发数据库的正确兼容级别。 
- 用于克隆数据库的新的 DBCC 命令 - 克隆数据库是新添加的 DBCC 命令，允许 CSS 等强大的用户通过克隆架构和元数据（不克隆数据）对现有生产数据库进行故障排除。 该调用通过 DBCC clonedatabase (‘source_database_name’, ‘clone_database_name’) 执行。 克隆的数据库不应用于生产环境。 若要查看在克隆数据库的调用过程中是否已生成数据库，可以使用以下命令：select DATABASEPROPERTYEX('clonedb', 'isClone')。返回值 1 表示 true，0 表示 false。 
- SQL 错误日志中的 TempDB 文件和文件大小信息 - 如果在启动期间，TempDB 数据文件的大小和自动增长不同，则输出文件数并触发警告。
- IFI 支持 SQL Server 错误日志中的消息 - 在错误日志中指示数据库即时文件初始化处于启用/禁用状态
- 替换 DBCC INPUTBUFFER 的新 DMF - 已引入将 session_id 作为参数的新动态管理函数 sys.dm_input_buffer，用于替换 DBCC INPUTBUFFER
- 针对可用性组的读取路由问题的 Xevent 增强功能 - 当前，如果存在路由列表，但路由列表中的任何服务器都不可用于连接，则只会激发 read_only_rout_fail XEvent。 这一改进包括用于帮助进行故障排除的其他信息，还会在用于激发 XEvent 的码位中展开。 
- 通过可用性组故障转移，改进了 Service Broker 的处理 - 当前，如果在可用性组故障转移上启用了 Service Broker，则 AG 故障转移期间，主要副本发起的所有 Service Broker 连接均保持打开状态。 AG 故障转移期间，这一改进会关闭所有此类打开的连接。
- [自动 Soft NUMA 分区](https://msdn.microsoft.com/library/ms345357(SQL.120).aspx) - 在服务器级别启用了跟踪标志 8079 后，会借助 SQL 2014 SP2 引入自动“Soft NUMA”技术。 如果在启动期间启用了跟踪标志 8079，SQL Server 2014 SP2 会询问硬件布局，并在报告每个 NUMA 节点 8 个或多个 CPU 的系统上自动配置 Soft NUMA。 自动 Soft NUMA 行为是超线程（HT/逻辑处理器）感知。 通过提高侦听器数、缩放和网络与加密功能，其他节点的分区和创建会缩放后台处理。 建议首先测试自动 Soft NUMA 的工作负荷性能，然后再在生产中启用该技术。

## <a name="see-also"></a>另请参阅
- [安装 SQL Server 2012 服务更新](https://msdn.microsoft.com/library/hh479746(v=sql.110).aspx)
- [如何识别 SQL Server 的版本](https://support.microsoft.com/en-us/help/321185)

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
