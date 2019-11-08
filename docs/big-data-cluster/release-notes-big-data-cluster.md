---
title: SQL Server 大数据群集发行说明
titleSuffix: SQL Server big data clusters
description: 本文介绍 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]（预览版）的最新更新和已知问题。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e868d5db99c3f0be141d28a881d8d8bc6f9c241e
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/04/2019
ms.locfileid: "73531628"
---
# <a name="sql-server-big-data-clusters-release-notes"></a>SQL Server 大数据群集发行说明

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

利用 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]，你可以从所有数据中获得近乎实时的见解，该群集提供了一个完整的环境来处理包括机器学习和 AI 功能在内的大量数据。

本文列出了 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] (BDC) 最新版本的更新和已知问题。

## <a id="rtm"></a> SQL Server 2019

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 介绍 SQL Server 大数据群集。

使用 SQL Server 大数据群集可执行以下操作：

- [部署](../big-data-cluster/deploy-get-started.md) SQL Server、Spark 和在 Kubernetes 上运行的 HDFS 容器的可缩放群集。 
- 在 Transact-SQL 或 Spark 中读取、写入和处理大数据。
- 通过大容量大数据轻松合并和分析高价值关系数据。
- 查询外部数据源。
- 在由 SQL Server 管理的 HDFS 中存储大数据。
- 通过群集查询多个外部数据源的数据。
- 将数据用于 AI、机器学习和其他分析任务。
- 在 [!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)] 中[部署和运行应用程序](../big-data-cluster/concept-application-deployment.md)。
- 使用 [PolyBase](../relational-databases/polybase/polybase-guide.md) 虚拟化数据。 使用外部表从外部 SQL Server、Oracle、Teradata、MongoDB 和 ODBC 数据源查询数据。
- 使用 Always On 可用性组技术为 SQL Server 主实例和所有数据库提供高可用性。

## <a name="sql-server-version"></a>SQL Server 版本

SQL Server 的当前版本为 `15.0.2070.34`。

## <a name="image-tags"></a>映像标记

此版本的映像标记为 `2019-GDR1-ubuntu-16.04`。

[!INCLUDE [sql-server-servicing-updates-version-15](../includes/sql-server-servicing-updates-version-15.md)]

## <a name="supportability"></a>可支持性

本部分介绍 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] (BDC) 支持的平台。

### <a name="kubernetes-platforms"></a>Kubernetes 平台

|平台|支持的版本|
|---------|---------|
|Kubernetes|BDC 要求 Kubernetes 版本最低为 1.13。 请参阅 [Kubernetes 版本和版本倾斜支持策略](https://kubernetes.io/docs/setup/release/version-skew-policy/)，详细了解 Kubernetes 版本支持策略。|
|Azure Kubernetes 服务 (AKS)|BDC 要求 AKS 版本最低为 1.13。<br/>请参阅 [AKS 中支持的 Kubernetes 版本](/azure/aks/supported-kubernetes-versions)，详细了解版本支持策略。|

### <a name="host-os-for-kubernetes"></a>适用于 Kubernetes 的主机操作系统

|平台|支持的版本|
|---------|---------|
|Red Hat Enterprise Linux|版本 7.3、7.4、7.5、7.6|
|Ubuntu|16.04|

### <a name="tools"></a>工具

|平台|支持的版本|
|---------|---------|
|`azdata`|必须与服务器具有相同的次要版本（与 SQL Server 主实例相同）。<br/>运行 `azdata –-version` 以验证该版本。 目前，此版本为 `15.0.2070`。|
|Azure Data Studio|获取 [Azure Data Studio](https://aka.ms/getazuredatastudio) 的最新内部版本。|

### <a name="sql-server-editions"></a>SQL Server 版本

|版本|说明|
|---------|---------|
|Enterprise<br/>Standard<br/>开发人员| 大数据群集版本由 SQL Server 主实例的版本确定。 在部署时会默认部署开发人员版。 可在部署后更改版本。 请参阅[配置 SQL Server 主实例](../big-data-cluster/configure-sql-server-master-instance.md)。 |

## <a name="known-issues"></a>已知问题

### <a name="livy-job-submission-from-azure-data-studio-ads-or-curl-fail-with-500-error"></a>从 Azure Data Studio (ADS) 或 curl 提交 Livy 作业失败，出现 500 错误

**问题及其对客户的影响**：在 HA 配置中，Spark 共享资源 (sparkhead) 配置了多个副本。 在这种情况下，可能会遇到从 Azure Data Studio (ADS) 或 `curl` 提交 Livy 作业失败的问题。 若 `curl` 到任何 sparkhead pod 都会导致连接被拒绝，则可以验证该问题。 例如，`curl https://sparkhead-0:8998/` 或 `curl https://sparkhead-1:8998` 返回 500 错误。

在下列情况下会发生这种情况：

- 每个 Zookeeper 实例的 Zookeeper pod 或进程重启几次。
- 当 Sparkhead pod 和 Zookeeper pod 之间的网络连接不可靠时。

**解决方法**：重启两个 Livy 服务器。

```bash
kubectl -n <clustername> exec sparkhead-0 -c hadoop-livy-sparkhistory supervisorctl restart livy
```

```bash
kubectl -n <clustername> exec sparkhead-1 -c hadoop-livy-sparkhistory supervisorctl restart livy
```

### <a name="create-memory-optimized-table-when-master-instance-in-an-availability-group"></a>当主实例位于可用性组中时，创建内存优化表

- **问题及其对客户的影响**：不能使用为了连接到可用性组数据库（侦听器）而公开的主终结点来创建内存优化表。

- **解决方法**：若要在 SQL Server 主实例为可用性组配置时创建内存优化表，请[连接到 SQL Server 实例](deployment-high-availability.md#instance-connect)，公开一个终结点，连接到 SQL Server 数据库，并在使用新连接创建的会话中创建内存优化表。

### <a name="insert-to-external-tables-active-directory-authentication-mode"></a>在 Active Directory 身份验证模式下插入外部表

- **问题及其对客户的影响**：当 SQL Server 主实例处于 Active Directory 身份验证模式时，如果查询仅从外部表（至少有一个外部表在存储池中）中选择并插入到另一个外部表中，该查询返回：

   ```
   Msg 7320, Level 16, State 102, Line 1
   Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "SQLNCLI11". Only domain logins can be used to query Kerberized storage pool.
   ```

- **解决方法**：通过下列方式之一修改查询。 将存储池表联接到本地表，或者先插入到本地表，然后从本地表进行读取以插入到数据池。

## <a name="next-steps"></a>后续步骤

有关 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 的详细信息，请参阅[什么是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]？](big-data-cluster-overview.md)
