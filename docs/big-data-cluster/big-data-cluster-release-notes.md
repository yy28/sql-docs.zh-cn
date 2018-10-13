---
title: SQL Server 2019 大数据群集的发行说明 |Microsoft Docs
description: 本文介绍了最新的更新以及 SQL Server 2019 （预览版） 大数据群集的已知的问题。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/04/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 13d5cfa95b9a37ecf26658ee255f93c8099faa8f
ms.sourcegitcommit: 0d6e4cafbb5d746e7d00fdacf8f3ce16f3023306
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/11/2018
ms.locfileid: "49085544"
---
# <a name="release-notes-for-sql-server-2019-big-data-clusters"></a>SQL Server 2019 大数据群集的发行说明

本文提供有关最新版本的 SQL Server 大数据群集的最新的更新和已知的问题。

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="ctp-20-october-2018"></a>CTP 2.0 (2018 年 10 月)

以下部分介绍的新功能和 SQL Server 2019 CTP 2.0 中的大数据群集的已知的问题。

### <a name="whats-in-the-ctp-20-release"></a>在 CTP 2.0 版中是什么？

- 使用 mssqlctl 管理工具的简单的部署体验
- 在 Azure Data Studio 的本机笔记本体验
- 查询通过存储 SQL Server 实例的 HDFS 文件
- 通过主服务器，以 SQL Server、 Oracle、 MongoDB 和 HDFS 的数据虚拟化
- 对于 SQL Server 和 Azure Data Studio 中的 Oracle 数据虚拟化向导
- 主机上的机器学习服务
- 群集管理门户，可用于监视和故障排除
- 在 Azure Data Studio 中提交 Spark 作业 
- 在群集管理门户中的 Spark UI
- 卷装载到存储类
- 通过从主服务器的数据池的查询
- 在 SSMS 中显示为分布式查询计划
- Pip 包为 mssqlctl 的管理工具的
- 通过控制器服务的内置部署引擎

### <a name="known-issues"></a>已知问题

以下各节提供在 CTP 2.0 中的 SQL Server 大数据群集的已知的问题。

#### <a name="deployment"></a>部署

- 如果使用 Azure Kubernetes 服务 (AKS)，建议的版本的 Kubernetes 是 1.10。 *，不支持磁盘重设大小。 您应确保相应地调整存储在部署时。 有关如何调整存储大小的详细信息，请参阅[数据暂留](concept-data-persistence.md)一文。 对于部署在 Vm 上的 Kubernetes，建议的版本是 1.11。

- 在部署后在 AKS 上，可能会看到从部署的以下两个警告事件。 这两个这些事件已知问题，但它们不会阻止您成功部署 AKS 上的大数据群集。

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- 如果大数据群集部署失败，则不会删除关联的命名空间。 这可能导致在群集上的孤立命名空间。 一种解决方法是在部署具有相同名称的群集之前手动删除该命名空间。

#### <a name="external-tables"></a>外部表

- 它是可以创建一个表，其中包含不支持的列类型的数据池外部表。 如果查询外部表，您会收到类似于以下内容一条消息：

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- 如果查询存储池外部表，可能会遇到错误，如果基础文件要在同一时间复制到 HDFS。

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

#### <a name="spark-and-notebooks"></a>Spark 和笔记本

- POD IP 地址可能会更改 Kubernetes 环境中，为 Pod 重新启动。 在 master pod 将重新启动的方案中，Spark 会话可能会因`NoRoteToHostException`。 这由于不使用新的 IP 获取刷新的 JVM 缓存的地址。

- 如果您有在 Windows 上的已安装的 Jupyter 和单独的 Python，Spark 笔记本可能会失败。 若要解决此问题，请升级到最新版本的 Jupyter。

- 在笔记本中，如果单击**添加文本**命令，在预览模式而非编辑模式中添加文本单元格。 您可以单击预览图标以切换到编辑模式和编辑该单元格。

#### <a name="hdfs"></a>HDFS

- 如果右键单击来预览它的 HDFS 中的某个文件时，可能会看到以下错误：

   `Error previewing file: File exceeds max size of 30MB`

   目前没有办法来预览文件大于 30 MB 的 Azure Data Studio。

- 不支持对 HDFS 涉及对 hdfs-site.xml 更改的配置更改。

#### <a name="security"></a>安全性

- SA_PASSWORD 是一部分的环境和可发现性 （例如在 cord 转储文件中）。 在部署后，必须重置 SA_PASSWORD 主实例上。 这不是一个 bug，但安全步骤。 有关如何更改 SA_PASSWORD Linux 容器中的详细信息，请参阅[更改 SA 密码](../linux/quickstart-install-connect-docker.md#sapassword)。

- AKS 日志可能包含用于大数据群集部署的 SA 密码。

## <a name="next-steps"></a>后续步骤

有关 SQL Server 大数据群集的详细信息，请参阅[什么是 SQL Server 2019 大数据群集？](big-data-cluster-overview.md)。
