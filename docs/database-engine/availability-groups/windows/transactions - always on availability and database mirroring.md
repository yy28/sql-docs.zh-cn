---
title: "用于 AlwaysOn 可用性组和数据库镜像的跨数据库事务和分布式事务 (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "数据库镜像 [SQL Server], 互操作性"
  - "跨数据库事务 [SQL Server]"
  - "事务 [数据库镜像]"
  - "可用性组 [SQL Server], 互操作性"
  - "故障排除 [SQL Server], 跨数据库事务"
ms.assetid: 9f7ed895-ad65-43e3-ba08-00d7bff1456d
caps.latest.revision: 33
ms.author: "mikeray"
manager: "jhubbard"
---
# 用于 AlwaysOn 可用性组和数据库镜像的跨数据库事务和分布式事务 (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

本主题介绍了用于 AlwaysOn 可用性组和数据库镜像的跨数据库事务和分布式事务。  
  
## 对同一个 SQL Server 实例中的跨数据库事务的支持  
AlwaysOn 可用性组不支持同一个 SQL Server 实例中的跨数据库事务。 这意味着同一数据库中的两个跨数据库事务不可能由相同的 SQL Server 实例托管。 即使这些数据库属于同一个可用性组，也是如此。  
  
数据库镜像也不支持跨数据库事务。  
  
##  <a name="dtcsupport"></a> 对分布式事务的支持  
使用 AlwaysOn 可用性组时，支持分布式事务。 这适用于由两个不同的 SQL Server 实例托管的数据库之间的分布式事务。 它也适用于 SQL Server 和其他兼容 DTC 的服务器之间的分布式事务。  
 
Microsoft 分布式事务处理协调器（MSDTC 或 DTC）是一项 Windows 服务，用于为分布式系统提供事务基础结构。 MSDTC 允许客户端应用程序在一个事务中包含多个数据源，然后跨该事务包含的所有服务器提交该事务。 例如，可以使用 MSDTC 来协调跨不同服务器上多个数据库的事务。

SQL Server 2016 引入了使用分布式事务的功能，且该事务中的一个或多个数据库位于某个可用性组中。 在 SQL Server 2016 之前，可用性组中的数据库不支持分布式事务。 SQL Server 2016 可以为每个数据库注册一个资源管理器。 这项新功能正是分布式事务可以包含可用性组中的数据库的原因。

  
 必须满足以下要求：  
  
-   可用性组必须在 Windows Server 2016 或 Windows Server 2012 R2 上运行。 对于 Windows Server 2012 R2，必须安装 KB3090973 中的更新，网址：[https://support.microsoft.com/zh-cn/kb/3090973](https://support.microsoft.com/en-us/kb/3090973)。  
  
-   必须使用 **CREATE AVAILABILITY GROUP** 命令和 **WITH DTC_SUPPORT = PER_DB** 子句创建可用性组。 当前不可更改现有可用性组。  

- 将加入可用性组的所有 SQL Server 实例都必须为 SQL Server 2016 或更高版本。
  
 
 ## 不支持分布式事务
 不支持分布式事务的特定情况包括：
 
 -  事务包含的多个数据库位于同一个可用性组中。
 
 -  其中至少一个数据库处于某一可用性组中，另一个数据库则处于 SQL Server 的相同实例上。 
 
 -  其中未通过启用分布式事务创建可用性组。
 
 -  数据库镜像。
 
 ## 建议
 在生产环境中，应群集化 DTC 服务。 如果未群集化 DTC 服务，SQL Server 将使用本地 DTC 服务。 如果使用本地 DTC 服务，解决方案的整体可用性会降低。 群集化 DTC 之后，如果群集节点发生故障，可以恢复正在进行的事务。
 
 > [!IMPORTANT]
 > 确定 DTC 不能为你的环境解决的事务的适当默认结果。  有关如何配置默认结果的信息，请参阅 [in-doubt xact resolution 服务器配置选项](../../../database-engine/configure-windows/in-doubt-xact-resolution-server-configuration-option.md)。
  
## 使用数据库镜像的示例方案  
 以下数据库镜像示例说明了如何可能出现逻辑上的不一致。 在此示例中，应用程序使用跨数据库事务插入两行数据：将其中一行插入镜像数据库 A 中的表，将另一行插入另一个数据库 B 中的表。数据库 A 在具有自动故障转移功能的高安全性模式下进行镜像。 提交事务时，数据库 A 不可用，镜像会话将故障自动转移到数据库 A 的镜像数据库。  
  
 故障转移之后，跨数据库事务可能会在数据库 B 上成功提交，但不可能会在故障转移的数据库中成功提交。 如果在发生故障之前，数据库 A 的原始主体服务器未能将跨数据库事务的日志发送到镜像服务器，则可能会出现这种情况。 故障转移之后，该事务将不存在于新的主体服务器上。 数据库 A 和数据库 B 出现不一致，因为在数据库 B 中插入的数据保持完好无损，而在数据库 A 中插入的数据已经丢失。  
  
 使用 MS DTC 事务时可能会出现类似的情况。 例如，故障转移后，新主体将访问 MS DTC。 但是 MS DTC 不能识别新的主体服务器，因而会终止被认为已在其他数据库中提交了的、所有“准备提交”的事务。  
  
> [!NOTE]  
>  通过本主题未批准的方式配合 DTC 使用数据库镜像或配合 DTC 使用 AlwaysOn 可用性组不受支持。  这并不意味着不支持与 DTC 不相关的产品方面；而是不支持因错误使用分布式事务而引发的任何问题。  
  
## 另请参阅  
 [AlwaysOn 可用性组：互操作性 (SQL Server)](../../../database-engine/availability-groups/windows/always-on-availability-groups-interoperability-sql-server.md)  
  
  