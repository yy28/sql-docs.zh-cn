---
title: 发行说明
titleSuffix: SQL Server big data clusters
description: 本文介绍 SQL Server 2019 大数据群集 (预览版) 的最新更新和已知问题。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: c0dd96d4a3227fda76921764429b4566e3e5dd28
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419303"
---
# <a name="release-notes-for-big-data-clusters-on-sql-server"></a>SQL Server 上的大数据群集的发行说明

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文列出了 SQL Server 大数据群集的最新版本的更新和已知问题。

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a id="ctp32"></a>CTP 3.2 (7 月)

以下部分介绍 SQL Server 2019 CTP 3.2 中的大数据群集的新增功能和已知问题。

|新增功能或更新 | 详细信息 |
|:---|:---|
|公共预览版 |在 CTP 3.2 之前, SQL Server 大数据群集可用于注册的早期采用者。 此版本允许任何人体验 SQL Server 大数据群集的功能。 <br/><br/> 请参阅[SQL Server 大数据群集入门](deploy-get-started.md)。|
|`azdata` |CTP 3.2 引入`azdata`了一个使用 Python 编写的命令行实用程序, 群集管理员可以通过 REST api 启动和管理大数据群集。 `azdata`替换`mssqlctl`。 请[参阅`azdata`安装](deploy-install-azdata.md)。 |
|PolyBase |外部表列名现在用于查询 SQL Server、Oracle、Teradata、MongoDB 和 ODBC 数据源。 |
|HDFS 分层刷新 |介绍 HDFS 分层的刷新功能, 以便可以为远程数据的最新快照刷新现有装载。 请参阅[HDFS 分层](hdfs-tiering.md) |
|基于笔记本的故障排除 |CTP 3.2 引入了 Jupyter 笔记本, 以协助 SQL Server 大数据群集中的组件进行[部署](deploy-notebooks.md)和[发现、诊断和故障排除](manage-notebooks.md)。 |
| &nbsp; | &nbsp; |

## <a id="ctp31"></a>CTP 3.1 (六月)

以下部分介绍 SQL Server 2019 CTP 3.1 中的大数据群集的新增功能和已知问题。

|新增功能或更新 | 详细信息 |
|:---|:---|
|公共预览版 |在 CTP 3.2 之前, SQL Server 大数据群集可用于注册的早期采用者。 此版本允许任何人体验 SQL Server 大数据群集的功能。 <br/><br/> 请参阅[SQL Server 大数据群集入门](deploy-get-started.md)。|
|基于笔记本的故障排除。|CTP 3.2 介绍了 Jupyter 笔记本, 以协助 SQL Server 大数据群集中的组件进行[部署](deploy-notebooks.md)和[发现、诊断和故障排除](manage-notebooks.md)。 |
|`azdata` |CTP 3.2 引入`azdata`了一个使用 Python 编写的命令行实用程序, 群集管理员可以通过 REST api 启动和管理大数据群集。 `azdata`替换`mssqlctl`。 请[参阅`azdata`安装](deploy-install-azdata.md)。 |
|HDFS 分层刷新 |介绍 HDFS 分层的刷新功能, 以便可以为远程数据的最新快照刷新现有装载。 请参阅[HDFS 分层](hdfs-tiering.md) |
| &nbsp; | &nbsp; |

### <a name="whats-new"></a>新增功能

| 新增功能或更新 | 详细信息 |
|:---|:---|
| `mssqlctl` 命令更改 | `mssqlctl cluster` 命令已重命名为 `mssqlctl bdc`。 有关详细信息，请参阅 [`mssqlctl` 参考](reference-azdata.md)。 |
| 群集`mssqlctl`管理门户的新状态命令和删除。 | 在此版本中, 将删除群集管理门户。 添加了新的状态命令来`mssqlctl`补充现有监视命令。 |
| Spark 计算池 | 可以创建其他节点来增加 Spark 计算能力，而无需扩展存储。 此外，还可以启动不用于 Spark 的存储池节点。 Spark 和存储已分离。 有关详细信息，请参阅[配置无需 Spark 的存储](deployment-custom-configuration.md#sparkstorage)。 |
| MSSQL Spark 连接器 | 支持对数据池外部表执行读/写操作。 旧版本仅支持对 MASTER 实例表执行读/写操作。 有关详细信息，请参阅[如何使用 MSSQL Spark 连接器从 Spark 对 SQL Server 执行读写操作](spark-mssql-connector.md)。 |
| 使用 MLeap 的机器学习 | [可以在 Spark 中训练 MLeap 机器学习模型，并使用 Java 语言扩展在 SQL Server 中对它进行评分](spark-create-machine-learning-model.md)。 |

### <a name="known-issues"></a>已知问题

以下部分介绍此版本的已知问题和限制。

#### <a name="hdfs"></a>HDFS

- 如果右键单击 HDFS 中的文件进行预览, 可能会看到以下错误:

   `Error previewing file: File exceeds max size of 30MB`

   当前在 Azure Data Studio 中无法预览大于 30 MB 的文件。

- 对于包含对 hdfs-site.xml 的更改的 HDFS 的配置更改不受支持。

#### <a name="deployment"></a>部署

- 不支持从以前的版本升级大数据数据群集。

   > [!IMPORTANT]
   > 在部署最新版本之前, 必须备份数据, 然后删除现有的大数据群集 (使用以前版本的**azdata**)。 有关详细信息, 请参阅[升级到新版本](deployment-upgrade.md)。

- 在 AKS 上部署后, 你可能会看到来自部署的以下两个警告事件。 这两个事件均为已知问题, 但不会阻止你在 AKS 上成功部署大数据群集。

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- 如果大数据群集部署失败, 则不会删除关联的命名空间。 这可能导致群集上出现孤立命名空间。 解决方法是在部署同名群集之前手动删除该命名空间。

#### <a name="external-tables"></a>外部表

- 大数据群集部署不再创建**SqlDataPool**和**SqlStoragePool**外部数据源。 你可以手动创建这些数据源, 以支持将数据虚拟化到数据池和存储池。

   > [!NOTE]
   > 用于创建这些外部数据源的 URI 在 Ctp 之间有所不同。 请参阅下面的 Transact-sql 命令, 了解如何创建它们 

   ```sql
   -- Create default data sources for SQL Big Data Cluster
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
       CREATE EXTERNAL DATA SOURCE SqlDataPool
       WITH (LOCATION = 'sqldatapool://controller-svc/default');
 
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
       CREATE EXTERNAL DATA SOURCE SqlStoragePool
       WITH (LOCATION = 'sqlhdfs://controller-svc/default');
   ```

- 可以为具有不受支持列类型的表创建数据池外部表。 如果查询外部表, 会收到类似于以下内容的消息:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- 如果查询存储池外部表, 则在将基础文件同时复制到 HDFS 时, 可能会收到错误。

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- 如果要创建使用字符数据类型的外部表到 Oracle, 则 Azure Data Studio 虚拟化向导会在外部表定义中将这些列解释为 VARCHAR。 这将导致外部表 DDL 失败。 请修改 Oracle 架构以使用 NVARCHAR2 类型, 或手动创建外部表语句并指定 NVARCHAR, 而不是使用向导。

#### <a name="application-deployment"></a>应用程序部署

- 从 RESTful API 调用 R、Python 或 MLeap 应用程序时, 调用将在5分钟后超时。

#### <a name="spark-and-notebooks"></a>Spark 和笔记本

- POD 重新启动时, Kubernetes 环境中的 IP 地址可能会发生更改。 在主-pod 重启的方案中, Spark 会话可能会失败, `NoRoteToHostException`并出现错误。 这是由不使用新 IP 地址刷新的 JVM 缓存引起的。

- 如果已在 Windows 上安装 Jupyter 并在 Windows 上安装了单独的 Python, Spark 笔记本可能会失败。 若要解决此问题, 请将 Jupyter 升级到最新版本。

- 在笔记本中, 如果单击 "**添加文本**" 命令, 将以预览模式而不是编辑模式添加文本单元。 可以单击 "预览" 图标切换到编辑模式并编辑该单元。

#### <a name="security"></a>安全性

- SA_PASSWORD 是环境的一部分, 可发现 (例如在电缆转储文件中)。 部署之后, 必须在主实例上重置 SA_PASSWORD。 这不是一个 bug, 而是一个安全步骤。 有关如何更改 Linux 容器中的 SA_PASSWORD 的详细信息, 请参阅[更改 SA 密码](../linux/quickstart-install-connect-docker.md#sapassword)。

- AKS 日志可能包含用于大数据群集部署的 SA 密码。

#### <a name="kibana-logs-dashboards"></a>Kibana 日志仪表板

- 在 Aris CTP 3.0 与3.1 之间, Kibana 版本已从6.3.1 升级到7.0.1。  这使得 Edge 浏览器与 Kibana 不兼容。 在边缘加载 Kibana 仪表板的当前版本时, 用户将看到一个空白页。 请参阅[此处]( https://www.elastic.co/support/matrix#matrix_browse)了解适用于 Kibana.rs 的支持的浏览器 


## <a id="ctp30"></a>CTP 3.0 (可能为)

以下部分介绍 SQL Server 2019 CTP 3.0 中的大数据群集的新增功能和已知问题。

### <a name="whats-new"></a>新增功能

| 新增功能或更新 | 详细信息 |
|:---|:---|
| mssqlctl 更新 | 多个 mssqlctl [命令和参数更新](reference-azdata.md)。 这包括对“mssqlctl login”命令的更新，该命令现在以控制器用户名和终结点为目标。 |
| 存储增强功能 | 支持日志和数据的不同存储配置。 此外，减少了大数据群集的持久卷声明数。 |
| 多个计算池实例 | 支持多个计算池实例。 |
| 新池行为和功能 | 现在，默认情况下，计算池仅用于“ROUND_ROBIN”分发中的存储池和数据池操作。 数据池现在可以使用新的REPLICATED 分发类型，即同一数据位于所有数据池实例中。 |
| 外部表的改进 | HADOOP 数据源类型的外部表现在支持读取最大 1 MB 的行。 外部表（ODBC、存储池、数据池）现在支持与 SQL Server 表一样宽的行。 |

### <a name="known-issues"></a>已知问题

以下部分介绍此版本的已知问题和限制。

#### <a name="hdfs"></a>HDFS

- 尝试在 HDFS 中创建新文件夹时, Azure Data Studio 将返回错误。 若要启用此功能, 请安装 Azure Data Studio 的预览体验版本:
  
   - [Windows 用户安装程序-内部**版本**](https://azuredatastudio-update.azurewebsites.net/latest/win32-x64-user/insider)
   - [Windows 系统安装程序-内部**版本**](https://azuredatastudio-update.azurewebsites.net/latest/win32-x64/insider)
   - [Windows ZIP-**预览体验**](https://azuredatastudio-update.azurewebsites.net/latest/win32-x64-archive/insider)
   - [macOS-**内部版本**](https://azuredatastudio-update.azurewebsites.net/latest/darwin/insider)
   - [Linux TAR。GZ-内部**版本**](https://azuredatastudio-update.azurewebsites.net/latest/linux-x64/insider)

- 如果右键单击 HDFS 中的文件进行预览, 可能会看到以下错误:

   `Error previewing file: File exceeds max size of 30MB`

   当前在 Azure Data Studio 中无法预览大于 30 MB 的文件。

- 对于包含对 hdfs-site.xml 的更改的 HDFS 的配置更改不受支持。

#### <a name="deployment"></a>部署

- CTP 3.0 中不支持启用 GPU 的大数据群集的先前部署过程。 正在调查备用部署过程。 现在, 项目 "使用 GPU 支持和运行 TensorFlow 部署大数据群集" 已暂时取消发布, 以避免混淆。

- 不支持从以前的版本升级大数据数据群集。

   > [!IMPORTANT]
   > 在部署最新版本之前, 必须备份数据, 然后删除现有的大数据群集 (使用以前版本的**azdata**)。 有关详细信息, 请参阅[升级到新版本](deployment-upgrade.md)。

- 在 AKS 上部署后, 你可能会看到来自部署的以下两个警告事件。 这两个事件均为已知问题, 但不会阻止你在 AKS 上成功部署大数据群集。

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- 如果大数据群集部署失败, 则不会删除关联的命名空间。 这可能导致群集上出现孤立命名空间。 解决方法是在部署同名群集之前手动删除该命名空间。

#### <a name="external-tables"></a>外部表

- 大数据群集部署不再创建**SqlDataPool**和**SqlStoragePool**外部数据源。 你可以手动创建这些数据源, 以支持将数据虚拟化到数据池和存储池。

   > [!NOTE]
   > 用于创建这些外部数据源的 URI 在 Ctp 之间有所不同。 请参阅下面的 Transact-sql 命令, 了解如何创建它们 

   ```sql
   -- Create default data sources for SQL Big Data Cluster
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
       CREATE EXTERNAL DATA SOURCE SqlDataPool
       WITH (LOCATION = 'sqldatapool://controller-svc/default');
 
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
       CREATE EXTERNAL DATA SOURCE SqlStoragePool
       WITH (LOCATION = 'sqlhdfs://controller-svc/default');
   ```

- 可以为具有不受支持列类型的表创建数据池外部表。 如果查询外部表, 会收到类似于以下内容的消息:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- 如果查询存储池外部表, 则在将基础文件同时复制到 HDFS 时, 可能会收到错误。

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- 如果要创建使用字符数据类型的外部表到 Oracle, 则 Azure Data Studio 虚拟化向导会在外部表定义中将这些列解释为 VARCHAR。 这将导致外部表 DDL 失败。 请修改 Oracle 架构以使用 NVARCHAR2 类型, 或手动创建外部表语句并指定 NVARCHAR, 而不是使用向导。

#### <a name="application-deployment"></a>应用程序部署

- 从 RESTful API 调用 R、Python 或 MLeap 应用程序时, 调用将在5分钟后超时。

#### <a name="spark-and-notebooks"></a>Spark 和笔记本

- POD 重新启动时, Kubernetes 环境中的 IP 地址可能会发生更改。 在主-pod 重启的方案中, Spark 会话可能会失败, `NoRoteToHostException`并出现错误。 这是由不使用新 IP 地址刷新的 JVM 缓存引起的。

- 如果已在 Windows 上安装 Jupyter 并在 Windows 上安装了单独的 Python, Spark 笔记本可能会失败。 若要解决此问题, 请将 Jupyter 升级到最新版本。

- 在笔记本中, 如果单击 "**添加文本**" 命令, 将以预览模式而不是编辑模式添加文本单元。 可以单击 "预览" 图标切换到编辑模式并编辑该单元。

#### <a name="security"></a>安全性

- SA_PASSWORD 是环境的一部分, 可发现 (例如在电缆转储文件中)。 部署之后, 必须在主实例上重置 SA_PASSWORD。 这不是一个 bug, 而是一个安全步骤。 有关如何更改 Linux 容器中的 SA_PASSWORD 的详细信息, 请参阅[更改 SA 密码](../linux/quickstart-install-connect-docker.md#sapassword)。

- AKS 日志可能包含用于大数据群集部署的 SA 密码。

## <a id="ctp25"></a>CTP 2.5 (四月)

以下部分介绍 SQL Server 2019 CTP 2.5 中的大数据群集的新增功能和已知问题。

### <a name="whats-new"></a>新增功能

| 新增功能或更新 | 详细信息 |
|:---|:---|
| 部署配置文件 | 使用默认和自定义[部署配置 JSON 文件](deployment-guidance.md#configfile)进行大数据群集部署，而不是使用环境变量。 |
| 提示的部署 | `azdata cluster create` 现在会提示进行默认部署的任何必要设置。 |
| 服务终结点和 Pod 名称更改 | 以下外部终结点的名称已更改:<br/>&nbsp;&nbsp;&nbsp;- **endpoint-master-pool** => **master-svc-external**<br/>&nbsp;&nbsp;&nbsp;- **endpoint-controller** => **controller-svc-external**<br/>&nbsp;&nbsp;&nbsp;- **endpoint-service-proxy** => **mgmtproxy-svc-external**<br/>&nbsp;&nbsp;&nbsp;- **endpoint-security** => **gateway-svc-external**<br/>&nbsp;&nbsp;&nbsp;- **endpoint-app-service-proxy** => **appproxy-svc-external**|
| **azdata**改进 | 使用**azdata** [列出外部终结点](deployment-guidance.md#endpoints), 并使用`--version`参数检查**azdata**的版本。 |
| 脱机安装 | 脱机大数据群集部署的指南。 |
| HDFS 分层的改进 | S3 分层、装载缓存和 OAuth 对 ADLS Gen2 的支持。 |
| 新`mssql` Spark-SQL Server 连接器 | |

### <a name="known-issues"></a>已知问题

以下部分介绍此版本的已知问题和限制。

#### <a name="deployment"></a>部署

- 不支持从以前的版本升级大数据数据群集。

   > [!IMPORTANT]
   > 在部署最新版本之前, 必须备份数据, 然后删除现有的大数据群集 (使用以前版本的**azdata**)。 有关详细信息, 请参阅[升级到新版本](deployment-upgrade.md)。

- 在 AKS 上部署后, 你可能会看到来自部署的以下两个警告事件。 这两个事件均为已知问题, 但不会阻止你在 AKS 上成功部署大数据群集。

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- 如果大数据群集部署失败, 则不会删除关联的命名空间。 这可能导致群集上出现孤立命名空间。 解决方法是在部署同名群集之前手动删除该命名空间。

#### <a name="external-tables"></a>外部表

- 大数据群集部署不再创建**SqlDataPool**和**SqlStoragePool**外部数据源。 你可以手动创建这些数据源, 以支持将数据虚拟化到数据池和存储池。

   ```sql
   -- Create default data sources for SQL Big Data Cluster
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
       CREATE EXTERNAL DATA SOURCE SqlDataPool
       WITH (LOCATION = 'sqldatapool://service-mssql-controller:8080/datapools/default');
 
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
       CREATE EXTERNAL DATA SOURCE SqlStoragePool
       WITH (LOCATION = 'sqlhdfs://nmnode-0-svc:50070');
   ```

- 可以为具有不受支持列类型的表创建数据池外部表。 如果查询外部表, 会收到类似于以下内容的消息:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- 如果查询存储池外部表, 则在将基础文件同时复制到 HDFS 时, 可能会收到错误。

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- 如果要创建使用字符数据类型的外部表到 Oracle, 则 Azure Data Studio 虚拟化向导会在外部表定义中将这些列解释为 VARCHAR。 这将导致外部表 DDL 失败。 请修改 Oracle 架构以使用 NVARCHAR2 类型, 或手动创建外部表语句并指定 NVARCHAR, 而不是使用向导。

#### <a name="application-deployment"></a>应用程序部署

- 从 RESTful API 调用 R、Python 或 MLeap 应用程序时, 调用将在5分钟后超时。

#### <a name="spark-and-notebooks"></a>Spark 和笔记本

- POD 重新启动时, Kubernetes 环境中的 IP 地址可能会发生更改。 在主-pod 重启的方案中, Spark 会话可能会失败, `NoRoteToHostException`并出现错误。 这是由不使用新 IP 地址刷新的 JVM 缓存引起的。

- 如果已在 Windows 上安装 Jupyter 并在 Windows 上安装了单独的 Python, Spark 笔记本可能会失败。 若要解决此问题, 请将 Jupyter 升级到最新版本。

- 在笔记本中, 如果单击 "**添加文本**" 命令, 将以预览模式而不是编辑模式添加文本单元。 可以单击 "预览" 图标切换到编辑模式并编辑该单元。

#### <a name="hdfs"></a>HDFS

- 如果右键单击 HDFS 中的文件进行预览, 可能会看到以下错误:

   `Error previewing file: File exceeds max size of 30MB`

   当前在 Azure Data Studio 中无法预览大于 30 MB 的文件。

- 对于包含对 hdfs-site.xml 的更改的 HDFS 的配置更改不受支持。

#### <a name="security"></a>安全性

- SA_PASSWORD 是环境的一部分, 可发现 (例如在电缆转储文件中)。 部署之后, 必须在主实例上重置 SA_PASSWORD。 这不是一个 bug, 而是一个安全步骤。 有关如何更改 Linux 容器中的 SA_PASSWORD 的详细信息, 请参阅[更改 SA 密码](../linux/quickstart-install-connect-docker.md#sapassword)。

- AKS 日志可能包含用于大数据群集部署的 SA 密码。

## <a id="ctp24"></a>CTP 2.4 (三月)

以下部分介绍 SQL Server 2019 CTP 2.4 中的大数据群集的新增功能和已知问题。

### <a name="whats-new"></a>新增功能

| 新增功能或更新 | 详细信息 |
|:---|:---|
| 关于 GPU 支持在 Spark 中使用 TensorFlow 运行深度学习的指南。 | [部署具有 GPU 支持的大数据群集并运行 TensorFlow](spark-gpu-tensorflow.md)。 |
| 默认情况下，不再继续创建数据源 SqlDataPool 和 SqlStoragePool。 | 请根据需要手动创建它们。 查看[已知问题](#externaltablesctp24)。 |
| 数据池的 `INSERT INTO SELECT` 支持。 | 有关示例，请参阅[教程：使用 Transact-SQL 将数据引入 SQL Server 数据池](tutorial-data-pool-ingest-sql.md)。 |
| `FORCE SCALEOUTEXECUTION` 和 `DISABLE SCALEOUTEXECUTION` 选项。 | 强制或禁止使用计算池来查询外部表。 例如，`SELECT TOP(100) * FROM web_clickstreams_hdfs_book_clicks OPTION(FORCE SCALEOUTEXECUTION)` 。 |
| 更新的 AKS 部署建议。 | 当在 AKS 上评估大数据群集时，我们现在建议使用大小为 Standard_L8s 的单个节点。 |
| Spark 运行时升级到 Spark 2.4。 | |

### <a name="known-issues"></a>已知问题

以下部分介绍此版本的已知问题和限制。

#### <a name="deployment"></a>部署

- 不支持从以前的版本升级大数据数据群集。

   > [!IMPORTANT]
   > 在部署最新版本之前, 必须备份数据, 然后删除现有的大数据群集 (使用以前版本的**azdata**)。 有关详细信息, 请参阅[升级到新版本](deployment-upgrade.md)。

- 在 AKS 上部署后, 你可能会看到来自部署的以下两个警告事件。 这两个事件均为已知问题, 但不会阻止你在 AKS 上成功部署大数据群集。

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- 如果大数据群集部署失败, 则不会删除关联的命名空间。 这可能导致群集上出现孤立命名空间。 解决方法是在部署同名群集之前手动删除该命名空间。

#### <a name="kubeadm-deployments"></a>kubeadm 部署

如果使用 kubeadm 在多台计算机上部署 Kubernetes, 则群集管理门户不会正确显示连接到大数据群集所需的终结点。 如果遇到此问题, 请使用以下解决方法来发现服务终结点 IP 地址:

- 如果要从群集内进行连接, 请在 Kubernetes 中查询要连接到的终结点的服务 IP。 例如, 以下**kubectl**命令显示 SQL Server 主实例的 IP 地址:

   ```bash
   kubectl get service endpoint-master-pool -n <clusterName> -o=custom-columns="IP:.spec.clusterIP,PORT:.spec.ports[*].nodePort"
   ```

- 如果要从群集外部进行连接, 请使用以下步骤进行连接:

   1. 获取运行 SQL Server 主实例的节点的 IP 地址: `kubectl get pod mssql-master-pool-0 -o jsonpath="Name: {.metadata.name} Status: {.status.hostIP}" -n <clusterName>`。

   1. 使用此 IP 地址连接到 SQL Server 的主实例。

   1. 查询 master 数据库中的**cluster_endpoint_table**以获取其他外部终结点。

      如果此操作由于连接超时而失败, 则可能是防火墙处理了相应的节点。 在这种情况下, 你必须联系 Kubernetes 群集管理员, 并要求提供外部公开的节点 IP。 这可以是任何节点。 然后, 可以使用该 IP 和相应的端口连接到群集中运行的各种服务。 例如, 管理员可以通过运行以下内容找到此 IP:

      ```
      [root@m12hn01 config]# kubectl cluster-info
      Kubernetes master is running at https://172.50.253.99:6443
      KubeDNS is running at https://172.30.243.91:6443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
      ```

#### <a name="delete-cluster-fails"></a>删除群集失败

尝试删除具有**azdata**的群集时, 它会失败, 并出现以下错误:

```
2019-03-26 20:38:11.0614 UTC | INFO | Deleting cluster ...
Error processing command: "TypeError"
delete_namespaced_service() takes 3 positional arguments but 4 were given
Makefile:61: recipe for target 'delete-cluster' failed
make[2]: *** [delete-cluster] Error 1
Makefile:223: recipe for target 'deploy-clean' failed
make[1]: *** [deploy-clean] Error 2
Makefile:203: recipe for target 'deploy-clean' failed
make: *** [deploy-clean] Error 2
```

新的 Python Kubernetes client (版本 9.0.0) 更改了删除命名空间 API, 该 API 当前中断了**azdata**。 仅当安装了新的 Kubernetes python 客户端时, 才会发生这种情况。 若要解决此问题, 可以使用**kubectl** (`kubectl delete ns <ClusterName>`) 直接删除群集, 也可以使用`sudo pip install kubernetes==8.0.1`安装旧版本。

#### <a id="externaltablesctp24"></a>外部表

- 大数据群集部署不再创建**SqlDataPool**和**SqlStoragePool**外部数据源。 你可以手动创建这些数据源, 以支持将数据虚拟化到数据池和存储池。

   ```sql
   -- Create default data sources for SQL Big Data Cluster
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
       CREATE EXTERNAL DATA SOURCE SqlDataPool
       WITH (LOCATION = 'sqldatapool://service-mssql-controller:8080/datapools/default');
 
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
       CREATE EXTERNAL DATA SOURCE SqlStoragePool
       WITH (LOCATION = 'sqlhdfs://service-master-pool:50070');
   ```

- 可以为具有不受支持列类型的表创建数据池外部表。 如果查询外部表, 会收到类似于以下内容的消息:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- 如果查询存储池外部表, 则在将基础文件同时复制到 HDFS 时, 可能会收到错误。

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- 如果要创建使用字符数据类型的外部表到 Oracle, 则 Azure Data Studio 虚拟化向导会在外部表定义中将这些列解释为 VARCHAR。 这将导致外部表 DDL 失败。 请修改 Oracle 架构以使用 NVARCHAR2 类型, 或手动创建外部表语句并指定 NVARCHAR, 而不是使用向导。

#### <a name="application-deployment"></a>应用程序部署

- 从 RESTful API 调用 R、Python 或 MLeap 应用程序时, 调用将在5分钟后超时。

#### <a name="spark-and-notebooks"></a>Spark 和笔记本

- POD 重新启动时, Kubernetes 环境中的 IP 地址可能会发生更改。 在主-pod 重启的方案中, Spark 会话可能会失败, `NoRoteToHostException`并出现错误。 这是由不使用新 IP 地址刷新的 JVM 缓存引起的。

- 如果已在 Windows 上安装 Jupyter 并在 Windows 上安装了单独的 Python, Spark 笔记本可能会失败。 若要解决此问题, 请将 Jupyter 升级到最新版本。

- 在笔记本中, 如果单击 "**添加文本**" 命令, 将以预览模式而不是编辑模式添加文本单元。 可以单击 "预览" 图标切换到编辑模式并编辑该单元。

#### <a name="hdfs"></a>HDFS

- 如果右键单击 HDFS 中的文件进行预览, 可能会看到以下错误:

   `Error previewing file: File exceeds max size of 30MB`

   当前在 Azure Data Studio 中无法预览大于 30 MB 的文件。

- 对于包含对 hdfs-site.xml 的更改的 HDFS 的配置更改不受支持。

#### <a name="security"></a>安全性

- SA_PASSWORD 是环境的一部分, 可发现 (例如在电缆转储文件中)。 部署之后, 必须在主实例上重置 SA_PASSWORD。 这不是一个 bug, 而是一个安全步骤。 有关如何更改 Linux 容器中的 SA_PASSWORD 的详细信息, 请参阅[更改 SA 密码](../linux/quickstart-install-connect-docker.md#sapassword)。

- AKS 日志可能包含用于大数据群集部署的 SA 密码。

## <a id="ctp23"></a>CTP 2.3 (2 月)

以下部分介绍 SQL Server 2019 CTP 2.3 中的大数据群集的新增功能和已知问题。

### <a name="whats-new"></a>新增功能

| 新增功能或更新 | 详细信息 |
| :---------- | :------ |
| 在 IntelliJ 中的大数据群集上提交 Spark 作业。 | [在 IntelliJ 中的 SQL Server 大数据群集上提交 Spark 作业](spark-submit-job-intellij-tool-plugin.md) |
| 用于应用程序部署和群集管理的常见 CLI。 | [如何在 SQL Server 2019 大数据群集（预览版）上部署应用](big-data-cluster-create-apps.md) |
| 将应用程序部署到大数据群集的 VS Code 扩展。 | [如何使用 VS Code 将应用程序部署到 SQL Server 大数据群集](app-deployment-extension.md) |
| 更改**azdata**工具命令用法。 | 有关更多详细信息, 请参阅[azdata 的已知问题](#azdatactp23)。 |
| 在大数据群集中使用 Sparklyr | [在 SQL Server 2019 大数据群集中使用 Sparklyr](sparklyr-from-RStudio.md) |
| 通过 **HDFS 分层**将兼容 HDFS 的外部存储装入大数据群集。 | 请参阅 [HDFS 分层](hdfs-tiering.md)。 |
| SQL Server 主实例和 HDFS/Spark 网关的新的统一连接体验。 | 请参阅 [SQL Server 主实例和 HDFS/Spark 网关](connect-to-big-data-cluster.md)。 |
| 删除具有**azdata 群集删除**的群集后, 将仅删除命名空间中属于大数据群集一部分的对象。 | 不会删除命名空间。 但是，在早期版本中，此命令会删除整个命名空间。 |
| 安全性终结点名称已更改并合并。 | service-security-lb 和 service-security-nodeport 已合并到 endpoint-security 终结点中。 |
| 代理终结点名称已更改并合并。 | service-proxy-lb 和 service-proxy-nodeport 已合并到 endpoint-service-proxy 终结点中。 |
| 控制器终结点名称已更改并合并。 | service-mssql-controller-lb 和 service-mssql-controller-nodeport 已合并到 endpoint-controller 终结点中。 |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>已知问题

以下部分介绍此版本的已知问题和限制。

#### <a name="deployment"></a>部署

- 不支持从以前的版本升级大数据数据群集。

   > [!IMPORTANT]
   > 在部署最新版本之前, 必须备份数据, 然后删除现有的大数据群集 (使用以前版本的**azdata**)。 有关详细信息, 请参阅[升级到新版本](deployment-upgrade.md)。

- **ACCEPT_EULA**环境变量必须是 "是" 或 "是", 才能接受 EULA。 以前的版本允许使用 "y" 和 "Y", 但这些版本不再被接受, 导致部署失败。

- **CLUSTER_PLATFORM**环境变量的默认值与以前版本中的不同。

- 在 AKS 上部署后, 你可能会看到来自部署的以下两个警告事件。 这两个事件均为已知问题, 但不会阻止你在 AKS 上成功部署大数据群集。

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- 如果大数据群集部署失败, 则不会删除关联的命名空间。 这可能导致群集上出现孤立命名空间。 解决方法是在部署同名群集之前手动删除该命名空间。

#### <a name="kubeadm-deployments"></a>kubeadm 部署

如果使用 kubeadm 在多台计算机上部署 Kubernetes, 则群集管理门户不会正确显示连接到大数据群集所需的终结点。 如果遇到此问题, 请使用以下解决方法来发现服务终结点 IP 地址:

- 如果要从群集内进行连接, 请在 Kubernetes 中查询要连接到的终结点的服务 IP。 例如, 以下**kubectl**命令显示 SQL Server 主实例的 IP 地址:

   ```bash
   kubectl get service endpoint-master-pool -n <clusterName> -o=custom-columns="IP:.spec.clusterIP,PORT:.spec.ports[*].nodePort"
   ```

- 如果要从群集外部进行连接, 请使用以下步骤进行连接:

   1. 获取运行 SQL Server 主实例的节点的 IP 地址: `kubectl get pod mssql-master-pool-0 -o jsonpath="Name: {.metadata.name} Status: {.status.hostIP}" -n <clusterName>`。

   1. 使用此 IP 地址连接到 SQL Server 的主实例。

   1. 查询 master 数据库中的**cluster_endpoint_table**以获取其他外部终结点。

      如果此操作由于连接超时而失败, 则可能是防火墙处理了相应的节点。 在这种情况下, 你必须联系 Kubernetes 群集管理员, 并要求提供外部公开的节点 IP。 这可以是任何节点。 然后, 可以使用该 IP 和相应的端口连接到群集中运行的各种服务。 例如, 管理员可以通过运行以下内容找到此 IP:

      ```
      [root@m12hn01 config]# kubectl cluster-info
      Kubernetes master is running at https://172.50.253.99:6443
      KubeDNS is running at https://172.30.243.91:6443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
      ```

#### <a id="azdatactp23"></a>azdata

- **Azdata**工具从动词-名词命令的顺序改为名词谓词顺序。 例如, `azdata create cluster`现在`azdata cluster create`是。

- `--name` 使用`azdata cluster create`创建群集时, 此参数是必需的。

   ```bash
   azdata cluster create --name <cluster_name>
   ```

- 有关升级到大数据群集和**azdata**的最新版本的重要信息, 请参阅[升级到新版本](deployment-upgrade.md)。

#### <a name="external-tables"></a>外部表

- 可以为具有不受支持列类型的表创建数据池外部表。 如果查询外部表, 会收到类似于以下内容的消息:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- 如果查询存储池外部表, 则在将基础文件同时复制到 HDFS 时, 可能会收到错误。

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- 如果要创建使用字符数据类型的外部表到 Oracle, 则 Azure Data Studio 虚拟化向导会在外部表定义中将这些列解释为 VARCHAR。 这将导致外部表 DDL 失败。 请修改 Oracle 架构以使用 NVARCHAR2 类型, 或手动创建外部表语句并指定 NVARCHAR, 而不是使用向导。

#### <a name="application-deployment"></a>应用程序部署

- 从 RESTful API 调用 R、Python 或 MLeap 应用程序时, 调用将在5分钟后超时。

#### <a name="spark-and-notebooks"></a>Spark 和笔记本

- POD 重新启动时, Kubernetes 环境中的 IP 地址可能会发生更改。 在主-pod 重启的方案中, Spark 会话可能会失败, `NoRoteToHostException`并出现错误。 这是由不使用新 IP 地址刷新的 JVM 缓存引起的。

- 如果已在 Windows 上安装 Jupyter 并在 Windows 上安装了单独的 Python, Spark 笔记本可能会失败。 若要解决此问题, 请将 Jupyter 升级到最新版本。

- 在笔记本中, 如果单击 "**添加文本**" 命令, 将以预览模式而不是编辑模式添加文本单元。 可以单击 "预览" 图标切换到编辑模式并编辑该单元。

#### <a name="hdfs"></a>HDFS

- 如果右键单击 HDFS 中的文件进行预览, 可能会看到以下错误:

   `Error previewing file: File exceeds max size of 30MB`

   当前在 Azure Data Studio 中无法预览大于 30 MB 的文件。

- 对于包含对 hdfs-site.xml 的更改的 HDFS 的配置更改不受支持。

#### <a name="security"></a>安全性

- SA_PASSWORD 是环境的一部分, 可发现 (例如在电缆转储文件中)。 部署之后, 必须在主实例上重置 SA_PASSWORD。 这不是一个 bug, 而是一个安全步骤。 有关如何更改 Linux 容器中的 SA_PASSWORD 的详细信息, 请参阅[更改 SA 密码](../linux/quickstart-install-connect-docker.md#sapassword)。

- AKS 日志可能包含用于大数据群集部署的 SA 密码。

## <a id="ctp22"></a>CTP 2.2 (2018 年12月)

以下部分介绍 SQL Server 2019 CTP 2.2 中的大数据群集的新增功能和已知问题。

### <a name="new-features"></a>新增功能

- 通过 ( `/portal` **https://\<:30777/门户)访问的群集管理门户。\>**
- 主池服务名称从`service-master-pool-lb`和`service-master-pool-nodeport`更改为`endpoint-master-pool`。
- 新版本的**azdata**和更新的映像。
- 其他 bug 修复和改进。

### <a name="known-issues"></a>已知问题

以下部分介绍此版本的已知问题和限制。

#### <a name="deployment"></a>部署

- 不支持从以前的版本升级大数据数据群集。 在部署最新版本之前, 必须先备份并删除任何现有大数据群集。 有关详细信息, 请参阅[升级到新版本](deployment-upgrade.md)。

- 在 AKS 上部署后, 你可能会看到来自部署的以下两个警告事件。 这两个事件均为已知问题, 但不会阻止你在 AKS 上成功部署大数据群集。

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- 如果大数据群集部署失败, 则不会删除关联的命名空间。 这可能导致群集上出现孤立命名空间。 解决方法是在部署同名群集之前手动删除该命名空间。

#### <a name="cluster-administration-portal"></a>群集管理门户

群集管理门户不显示 SQL Server 主实例的终结点。 若要查找 master 实例的 IP 地址和端口, 请使用以下**kubectl**命令:

```
kubectl get svc endpoint-master-pool -n <your-big-data-cluster-name>
```

#### <a name="external-tables"></a>外部表

- 可以为具有不受支持列类型的表创建数据池外部表。 如果查询外部表, 会收到类似于以下内容的消息:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- 如果查询存储池外部表, 则在将基础文件同时复制到 HDFS 时, 可能会收到错误。

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

#### <a name="spark-and-notebooks"></a>Spark 和笔记本

- POD 重新启动时, Kubernetes 环境中的 IP 地址可能会发生更改。 在主-pod 重启的方案中, Spark 会话可能会失败, `NoRoteToHostException`并出现错误。 这是由不使用新 IP 地址刷新的 JVM 缓存引起的。

- 如果已在 Windows 上安装 Jupyter 并在 Windows 上安装了单独的 Python, Spark 笔记本可能会失败。 若要解决此问题, 请将 Jupyter 升级到最新版本。

- 在笔记本中, 如果单击 "**添加文本**" 命令, 将以预览模式而不是编辑模式添加文本单元。 可以单击 "预览" 图标切换到编辑模式并编辑该单元。

#### <a name="hdfs"></a>HDFS

- 如果右键单击 HDFS 中的文件进行预览, 可能会看到以下错误:

   `Error previewing file: File exceeds max size of 30MB`

   当前在 Azure Data Studio 中无法预览大于 30 MB 的文件。

- 对于包含对 hdfs-site.xml 的更改的 HDFS 的配置更改不受支持。

#### <a name="security"></a>安全性

- SA_PASSWORD 是环境的一部分, 可发现 (例如在电缆转储文件中)。 部署之后, 必须在主实例上重置 SA_PASSWORD。 这不是一个 bug, 而是一个安全步骤。 有关如何更改 Linux 容器中的 SA_PASSWORD 的详细信息, 请参阅[更改 SA 密码](../linux/quickstart-install-connect-docker.md#sapassword)。

- AKS 日志可能包含用于大数据群集部署的 SA 密码。

## <a id="ctp21"></a>CTP 2.1 (2018 年11月)

以下部分介绍 SQL Server 2019 CTP 2.1 中的大数据群集的新增功能和已知问题。

### <a name="new-features"></a>新增功能

- 在大数据群集中[部署 Python 和 R 应用](big-data-cluster-create-apps.md)。
- 新版本的**azdata**和更新的映像。 
- 其他 bug 修复和改进。

### <a name="known-issues"></a>已知问题

以下各节提供 CTP 2.1 中 SQL Server 大数据群集的已知问题。

#### <a name="deployment"></a>部署

- 不支持从以前的版本升级大数据数据群集。 在部署最新版本之前, 必须先备份并删除任何现有大数据群集。 有关详细信息, 请参阅[升级到新版本](deployment-upgrade.md)。

- 在 AKS 上部署后, 你可能会看到来自部署的以下两个警告事件。 这两个事件均为已知问题, 但不会阻止你在 AKS 上成功部署大数据群集。

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- 如果大数据群集部署失败, 则不会删除关联的命名空间。 这可能导致群集上出现孤立命名空间。 解决方法是在部署同名群集之前手动删除该命名空间。

#### <a name="admin-portal"></a>管理门户

- 当你[使用 msqlctl 命令创建应用](big-data-cluster-create-apps.md)并将其部署到 SQL Server 大数据群集上时, 群集管理门户将在管理部分的控制器部分中显示应用程序部署为 "未知" 的 pod。

#### <a name="external-tables"></a>外部表

- 可以为具有不受支持列类型的表创建数据池外部表。 如果查询外部表, 会收到类似于以下内容的消息:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- 如果查询存储池外部表, 则在将基础文件同时复制到 HDFS 时, 可能会收到错误。

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

#### <a name="spark-and-notebooks"></a>Spark 和笔记本

- POD 重新启动时, Kubernetes 环境中的 IP 地址可能会发生更改。 在主-pod 重启的方案中, Spark 会话可能会失败, `NoRoteToHostException`并出现错误。 这是由不使用新 IP 地址刷新的 JVM 缓存引起的。

- 如果已在 Windows 上安装 Jupyter 并在 Windows 上安装了单独的 Python, Spark 笔记本可能会失败。 若要解决此问题, 请将 Jupyter 升级到最新版本。

- 在笔记本中, 如果单击 "**添加文本**" 命令, 将以预览模式而不是编辑模式添加文本单元。 可以单击 "预览" 图标切换到编辑模式并编辑该单元。

#### <a name="hdfs"></a>HDFS

- 如果右键单击 HDFS 中的文件进行预览, 可能会看到以下错误:

   `Error previewing file: File exceeds max size of 30MB`

   当前在 Azure Data Studio 中无法预览大于 30 MB 的文件。

- 对于包含对 hdfs-site.xml 的更改的 HDFS 的配置更改不受支持。

#### <a name="security"></a>安全性

- SA_PASSWORD 是环境的一部分, 可发现 (例如在电缆转储文件中)。 部署之后, 必须在主实例上重置 SA_PASSWORD。 这不是一个 bug, 而是一个安全步骤。 有关如何更改 Linux 容器中的 SA_PASSWORD 的详细信息, 请参阅[更改 SA 密码](../linux/quickstart-install-connect-docker.md#sapassword)。

- AKS 日志可能包含用于大数据群集部署的 SA 密码。

## <a id="ctp20"></a>CTP 2.0 (2018 年10月)

以下部分介绍 SQL Server 2019 CTP 2.0 中的大数据群集的新增功能和已知问题。

### <a name="new-features"></a>新增功能

- 使用 azdata 管理工具的简单部署体验
- Azure Data Studio 中的本机笔记本体验
- 通过 SQL Server 的存储实例查询 HDFS 文件
- 通过 master 到 SQL Server、Oracle、MongoDB 和 HDFS 的数据虚拟化
- SQL Server 和 Oracle Azure Data Studio 中的数据虚拟化向导
- Master 上的 ML 服务
- 群集管理门户, 可用于监视和故障排除
- Spark 作业提交 Azure Data Studio 
- 群集管理门户中的 Spark UI
- 卷装载到存储类
- 从 master 对数据池进行查询
- 在 SSMS 中显示分布式查询计划
- Pip package for azdata 管理工具
- 通过控制器服务的内置部署引擎

### <a name="known-issues"></a>已知问题

以下各节提供 CTP 2.0 中 SQL Server 大数据群集的已知问题。

#### <a name="deployment"></a>部署

- 如果你使用的是 Azure Kubernetes Service (AKS), 则建议的 Kubernetes 版本为 1.10. *, 它不支持磁盘大小调整。 应确保在部署时相应地调整存储大小。 有关如何调整存储大小的详细信息, 请参阅[数据持久性](concept-data-persistence.md)一文。 对于部署在 Vm 上的 Kubernetes, 推荐的版本为1.11。

- 在 AKS 上部署后, 你可能会看到来自部署的以下两个警告事件。 这两个事件均为已知问题, 但不会阻止你在 AKS 上成功部署大数据群集。

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- 如果大数据群集部署失败, 则不会删除关联的命名空间。 这可能导致群集上出现孤立命名空间。 解决方法是在部署同名群集之前手动删除该命名空间。

#### <a name="external-tables"></a>外部表

- 可以为具有不受支持列类型的表创建数据池外部表。 如果查询外部表, 会收到类似于以下内容的消息:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- 如果查询存储池外部表, 则在将基础文件同时复制到 HDFS 时, 可能会收到错误。

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

#### <a name="spark-and-notebooks"></a>Spark 和笔记本

- POD 重新启动时, Kubernetes 环境中的 IP 地址可能会发生更改。 在主-pod 重启的方案中, Spark 会话可能会失败, `NoRoteToHostException`并出现错误。 这是由不使用新 IP 地址刷新的 JVM 缓存引起的。

- 如果已在 Windows 上安装 Jupyter 并在 Windows 上安装了单独的 Python, Spark 笔记本可能会失败。 若要解决此问题, 请将 Jupyter 升级到最新版本。

- 在笔记本中, 如果单击 "**添加文本**" 命令, 将以预览模式而不是编辑模式添加文本单元。 可以单击 "预览" 图标切换到编辑模式并编辑该单元。

#### <a name="hdfs"></a>HDFS

- 如果右键单击 HDFS 中的文件进行预览, 可能会看到以下错误:

   `Error previewing file: File exceeds max size of 30MB`

   当前在 Azure Data Studio 中无法预览大于 30 MB 的文件。

- 对于包含对 hdfs-site.xml 的更改的 HDFS 的配置更改不受支持。

#### <a name="security"></a>安全性

- SA_PASSWORD 是环境的一部分, 可发现 (例如在电缆转储文件中)。 部署之后, 必须在主实例上重置 SA_PASSWORD。 这不是一个 bug, 而是一个安全步骤。 有关如何更改 Linux 容器中的 SA_PASSWORD 的详细信息, 请参阅[更改 SA 密码](../linux/quickstart-install-connect-docker.md#sapassword)。

- AKS 日志可能包含用于大数据群集部署的 SA 密码。

## <a name="next-steps"></a>后续步骤

有关 SQL Server 大数据群集的详细信息, 请参阅[什么是 SQL Server 2019 大数据群集？](big-data-cluster-overview.md)。
