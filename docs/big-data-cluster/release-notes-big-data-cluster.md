---
title: SQL Server 大数据群集发行说明
titleSuffix: SQL Server big data clusters
description: 本文介绍 SQL Server 大数据群集的最新更新和已知问题。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 03/31/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: cd004554ad45db40beae958bdf0a7142b1b74bab
ms.sourcegitcommit: 2426a5e1abf6ecf35b1e0c062dc1e1225494cbb0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/01/2020
ms.locfileid: "80517157"
---
# <a name="sql-server-2019-big-data-clusters-release-notes"></a>SQL Server 2019 大数据群集发行说明

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

以下发行说明适用于 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]。 本文按各版本分为不同的部分。 每个版本都有介绍 CU 更改的支持性文章的链接，还有 Linux 包下载的链接。 本文还列出了 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] (BDC) 最新版本的[已知问题](#known-issues)。

## <a name="supported-platforms"></a>支持的平台

本部分介绍 BDC 支持的平台。

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

### <a name="sql-server-editions"></a>SQL Server 版本

|版本|说明|
|---------|---------|
|Enterprise<br/>Standard<br/>开发人员| 大数据群集版本由 SQL Server 主实例的版本确定。 在部署时会默认部署开发人员版。 可在部署后更改版本。 请参阅[配置 SQL Server 主实例](../big-data-cluster/configure-sql-server-master-instance.md)。 |

## <a name="tools"></a>工具

|平台|支持的版本|
|---------|---------|
|`azdata`|必须与服务器具有相同的次要版本（与 SQL Server 主实例相同）。<br/><br/>运行 `azdata –-version` 以验证该版本。<br/><br/>请参阅[版本历史记录](#release-history)获取最新版本。|
|Azure Data Studio|获取 [Azure Data Studio](https://aka.ms/getazuredatastudio) 的最新内部版本。|

## <a name="release-history"></a>版本历史记录

下表列出了 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] 的版本历史记录。

| 发布               | 版本         | 发布日期 |
|-----------------------|-----------------|--------------|
| [CU4](#cu4)           | 15.0.4033.1     | 2020 年 3 月 31 日   |
| [CU3](#cu3)           | 15.0.4023.6     | 2020-03-12   |
| [CU2](#cu2)           | 15.0.4013.40    | 2020-02-13   |
| [CU1](#cu1)           | 15.0.4003.23    | 2020-01-07   |
| [GDR1](#rtm)          | 15.0.2070.34    | 2019-11-04   |

## <a name="how-to-install-updates"></a>如何安装更新

若要安装更新，请参阅[如何升级 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](deployment-upgrade.md)。

## <a name="cu4-april-2020"></a><a id="cu4"></a> CU4（2020 年 4 月）

SQL Server 2019 的累积更新 4 (CU4) 版本。 此次发布的 SQL Server 数据库引擎版本是 15.0.4033.1。

|包版本 | 映像标记 |
|-----|-----|
|15.0.4033.1 |[2019-CU4-ubuntu-16.04]

## <a name="cu3-march-2020"></a><a id="cu3"></a> CU3（2020 年 3 月）

SQL Server 2019 的累积更新 3 (CU3) 版本。 此次发布的 SQL Server 数据库引擎版本是 15.0.4023.6。

|包版本 | 映像标记 |
|-----|-----|
|15.0.4023.6 |[2019-CU3-ubuntu-16.04]

### <a name="resolved-issues"></a>已解决的问题

SQL Server 2019 CU3 解决了以前版本中的以下问题。

- [通过专用存储库进行部署](#deployment-with-private-repository)
- [升级可能因超时而失败](#upgrade-may-fail-due-to-timeout)

## <a name="cu2-february-2020"></a><a id="cu2"></a> CU2（2020 年 2 月）

SQL Server 2019 的累积更新 2 (CU2) 版本。 此次发布的 SQL Server 数据库引擎版本是 15.0.4013.40。

|包版本 | 映像标记 |
|-----|-----|
|15.0.4013.40 |[2019-CU2-ubuntu-16.04]

## <a name="cu1-january-2020"></a><a id="cu1"></a> CU1 （2020 年 1 月）

SQL Server 2019 的累积更新 1 (CU1) 版本。 此次发布的 SQL Server 数据库引擎版本是 15.0.4003.23。

|包版本 | 映像标记 |
|-----|-----|
|15.0.4003.23|[2019-CU1-ubuntu-16.04]

## <a name="gdr1-november-2019"></a><a id="rtm"></a> GDR1（2019 年 11 月）

SQL Server 2019 常规分发版本 1 (GDR1) - 介绍 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-nover.md)] 的公开发布。 此次发布的 SQL Server 数据库引擎版本是 15.0.2070.34。

|包版本 | 映像标记 |
|-----|-----|
|15.0.2070.34|[2019-GDR1-ubuntu-16.04]

[!INCLUDE [sql-server-servicing-updates-version-15](../includes/sql-server-servicing-updates-version-15.md)]

## <a name="known-issues"></a>已知问题

### <a name="deployment-with-private-repository"></a>通过专用存储库进行部署

- **受影响的版本**：GDR1、CU1、CU2。 CU3 已解决。

- **问题及其对客户的影响**：从专用存储库升级需要满足特定要求

- **解决方法**：如果使用专用存储库来预提取用于部署或升级 BDC 的映像，请确保当前版本映像和目标版本映像位于专用存储库中。 这样，在必要时可以成功回退。 此外，如果在原始部署后更改了专用存储库的凭据，请在升级之前更新 Kubernetes 中的相应机密。 `azdata` 不支持通过 `AZDATA_PASSWORD` 和 `AZDATA_USERNAME` 环境变量来更新凭据。 使用 [`kubectl edit secrets`](https://kubernetes.io/docs/concepts/configuration/secret/#editing-a-secret) 更新机密。 

不支持对当前版本和目标版本使用不同的存储库进行升级。

### <a name="upgrade-may-fail-due-to-timeout"></a>升级可能因超时而失败

- **受影响的版本**：GDR1、CU1、CU2。 CU3 已解决。

- **问题及其对客户的影响**：升级可能因超时而失败。

   下面的代码显示了提示失败的消息：

   ```
   >azdata.EXE bdc upgrade --name <mssql-cluster>
   Upgrading cluster to version 15.0.4003

   NOTE: Cluster upgrade can take a significant amount of time depending on
   configuration, network speed, and the number of nodes in the cluster.

   Upgrading Control Plane.
   Control plane upgrade failed. Failed to upgrade controller.
   ```

   在 Azure Kubernetes Service (AKS) 中升级 BDC 时，更有可能出现此错误。

- **解决方法**：增加升级的超时时间值。 

   若要增加升级的超时时间值，请编辑升级配置映射。 编辑升级配置映射：

   1. 运行以下命令：

      ```bash
      kubectl edit configmap controller-upgrade-configmap
      ```

   2. 编辑以下字段：

       **`controllerUpgradeTimeoutInMinutes`** 指定等待控制器或控制器 db 完成升级所需的分钟数。 默认值为 5。 至少更新为 20。

       **`totalUpgradeTimeoutInMinutes`** ：指定控制器和控制器 db 完成升级所需的总时间（控制器 + 控制器 db 升级）。默认值为 10。 至少更新为 40。

       **`componentUpgradeTimeoutInMinutes`** ：指定升级的每个后续阶段必须完成的时间量。  默认值为 30。 更新为 45。

   3. 保存并退出

   还有另一种方法可设置超时时间值，即使用下面的 python 脚本：

   ```python
   from kubernetes import client, config
   import json

   def set_upgrade_timeouts(namespace, controller_timeout=20, controller_total_timeout=40, component_timeout=45):
       """ Set the timeouts for upgrades

       The timeout settings are as follows

       controllerUpgradeTimeoutInMinutes: sets the max amount of time for the controller
           or controllerdb to finish upgrading

       totalUpgradeTimeoutInMinutes: sets the max amount of time to wait for both the
           controller and controllerdb to complete their upgrade

       componentUpgradeTimeoutInMinutes: sets the max amount of time allowed for
           subsequent phases of the upgrade to complete
       """
       config.load_kube_config()

       upgrade_config_map = client.CoreV1Api().read_namespaced_config_map("controller-upgrade-configmap", namespace)

       upgrade_config = json.loads(upgrade_config_map.data["controller-upgrade"])

       upgrade_config["controllerUpgradeTimeoutInMinutes"] = controller_timeout

       upgrade_config["totalUpgradeTimeoutInMinutes"] = controller_total_timeout

       upgrade_config["componentUpgradeTimeoutInMinutes"] = component_timeout

       upgrade_config_map.data["controller-upgrade"] = json.dumps(upgrade_config)

       client.CoreV1Api().patch_namespaced_config_map("controller-upgrade-configmap", namespace, upgrade_config_map)
   ```

### <a name="livy-job-submission-from-azure-data-studio-ads-or-curl-fail-with-500-error"></a>从 Azure Data Studio (ADS) 或 curl 提交 Livy 作业失败，出现 500 错误

- **问题及其对客户的影响**：在 HA 配置中，Spark 共享资源 `sparkhead` 配置有多个副本。 在这种情况下，可能会遇到从 Azure Data Studio (ADS) 或 `curl` 提交 Livy 作业失败的问题。 如果 `curl` 到任何 `sparkhead` Pod 都会导致连接被拒绝，则可以验证该问题。 例如，`curl https://sparkhead-0:8998/` 或 `curl https://sparkhead-1:8998` 返回 500 错误。

   在下列情况下会发生这种情况：

   - 每个 Zookeeper 实例的 Zookeeper Pod 或进程重启几次时。
   - 当 `sparkhead` Pod 和 Zookeeper Pod 之间的网络连接不可靠时。

- **解决方法**：重启两个 Livy 服务器。

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

### <a name="transparent-data-encryption-capabilities-can-not-be-used-with-databases-that-are-part-of-the-availability-group-in-the-sql-server-master-instance"></a>透明数据加密功能不能与 SQL Server 主实例中可用性组中的数据库一起使用

- **问题及其对客户的影响**：在 HA 配置中，由于每个副本上用于加密的主密钥不同，因此在故障转移后不能使用启用了加密的数据库。 

- **解决方法**：没有针对此问题的解决方法。 建议在准备好修复之前，不要在此配置中启用加密。

## <a name="next-steps"></a>后续步骤

有关 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 的详细信息，请参阅[什么是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]？](big-data-cluster-overview.md)
