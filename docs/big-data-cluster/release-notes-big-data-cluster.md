---
title: 发行说明
titleSuffix: SQL Server big data clusters
description: 本文介绍了最新的更新以及 SQL Server 2019 大数据群集 （预览版） 的已知的问题。
author: rothja
ms.author: jroth
manager: jroth
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 1f2d7f5a1d4a966edbce3c4ad96a7b31bd604b48
ms.sourcegitcommit: f7ad034f748ebc3e5691a5e4c3eb7490e5cf3ccf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/29/2019
ms.locfileid: "67469124"
---
# <a name="release-notes-for-big-data-clusters-on-sql-server"></a>对于 SQL Server 上的大数据群集的发行说明

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文列出的更新，并了解最新版本的 SQL 服务器大数据群集的问题。

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a id="ctp31"></a> CTP 3.1 （年 6 月）

以下部分介绍的新功能和 SQL Server 2019 CTP 3.1 中的大数据群集的已知的问题。

### <a name="whats-new"></a>新增功能

| 新增功能或更新 | 详细信息 |
|:---|:---|
| `mssqlctl` 命令更改 | `mssqlctl cluster` 命令已重命名为`mssqlctl bdc`。 有关详细信息，请参阅[`mssqlctl`引用](reference-mssqlctl.md)。 |
| 新`mssqlctl`状态命令和群集管理门户中的删除。 | 群集管理门户将在此版本中删除。 已添加到新状态命令`mssqlctl`现有监视命令的补数。 |
| Spark 计算池 | 创建其他节点，而无需纵向扩展存储提升 Spark 的计算能力。 此外，您可以开始不会使用 spark 的存储池节点。 分离 Spark 和存储。 有关详细信息，请参阅[配置存储，没有 spark](deployment-custom-configuration.md#sparkstorage)。 |
| MSSQL Spark 连接器 | 读取/写入数据池外部表的支持。 上一版本支持读/写到主实例仅限表。 有关详细信息，请参阅[如何读取和写入到 SQL Server 从 Spark 使用 MSSQL Spark 连接器](spark-mssql-connector.md)。 |
| 机器学习中使用 MLeap | [在 Spark 中的 MLeap 机器学习模型进行训练和评分中使用的 Java 语言扩展。 SQL Server](spark-create-machine-learning-model.md)。 |

### <a name="known-issues"></a>已知问题

以下部分介绍的已知的问题和在此版本的限制。

#### <a name="hdfs"></a>HDFS

- 如果右键单击来预览它的 HDFS 中的某个文件时，可能会看到以下错误：

   `Error previewing file: File exceeds max size of 30MB`

   目前没有办法来预览文件大于 30 MB 的 Azure Data Studio。

- 不支持对 HDFS 涉及对 hdfs-site.xml 更改的配置更改。

#### <a name="deployment"></a>部署

- 不支持从以前的版本升级的大数据数据群集。

   > [!IMPORTANT]
   > 必须备份您的数据，然后删除现有的大数据群集 (使用以前版本的**mssqlctl**) 之前部署的最新版本。 有关详细信息，请参阅[升级到新版本](deployment-upgrade.md)。

- 在部署后在 AKS 上，可能会看到从部署的以下两个警告事件。 这两个这些事件已知问题，但它们不会阻止您成功部署 AKS 上的大数据群集。

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- 如果大数据群集部署失败，则不会删除关联的命名空间。 这可能导致在群集上的孤立命名空间。 一种解决方法是在部署具有相同名称的群集之前手动删除该命名空间。

#### <a name="external-tables"></a>外部表

- 大数据群集部署将不再创建**SqlDataPool**并**SqlStoragePool**外部数据源。 可以创建这些数据源手动来支持对数据池和存储池数据虚拟化。

   > [!NOTE]
   > 创建这些外部数据源的 URI 是 Ctp 之间的差异。 请参阅以下 TRANSACT-SQL 命令，请参阅如何创建它们 

   ```sql
   -- Create default data sources for SQL Big Data Cluster
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
       CREATE EXTERNAL DATA SOURCE SqlDataPool
       WITH (LOCATION = 'sqldatapool://controller-svc/default');
 
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
       CREATE EXTERNAL DATA SOURCE SqlStoragePool
       WITH (LOCATION = 'sqlhdfs://controller-svc/default');
   ```

- 它是可以创建一个表，其中包含不支持的列类型的数据池外部表。 如果查询外部表，您会收到类似于以下内容一条消息：

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- 如果查询存储池外部表，可能会遇到错误，如果基础文件要在同一时间复制到 HDFS。

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- 如果要创建向 Oracle 使用字符数据类型的外部表，Azure Data Studio 的虚拟化向导将这些列作为 VARCHAR 解释外部表定义中。 外部表 DDL 中，这将导致失败。 请修改使用 NVARCHAR2 类型，或手动创建 EXTERNAL TABLE 语句，而不是使用向导指定 NVARCHAR 的 Oracle 架构。

#### <a name="application-deployment"></a>应用程序部署

- 在从 RESTful API 调用 R、 Python 或 MLeap 应用程序，该调用将超时在 5 分钟内。

#### <a name="spark-and-notebooks"></a>Spark 和笔记本

- POD IP 地址可能会更改 Kubernetes 环境中，为 Pod 重新启动。 在 master pod 将重新启动的方案中，Spark 会话可能会因`NoRoteToHostException`。 这由于不使用新的 IP 获取刷新的 JVM 缓存的地址。

- 如果您有在 Windows 上的已安装的 Jupyter 和单独的 Python，Spark 笔记本可能会失败。 若要解决此问题，请升级到最新版本的 Jupyter。

- 在笔记本中，如果单击**添加文本**命令，在预览模式而非编辑模式中添加文本单元格。 您可以单击预览图标以切换到编辑模式和编辑该单元格。

#### <a name="security"></a>安全性

- SA_PASSWORD 是一部分的环境和可发现性 （例如在 cord 转储文件中）。 在部署后，必须重置 SA_PASSWORD 主实例上。 这不是一个 bug，但安全步骤。 有关如何更改 SA_PASSWORD Linux 容器中的详细信息，请参阅[更改 SA 密码](../linux/quickstart-install-connect-docker.md#sapassword)。

- AKS 日志可能包含用于大数据群集部署的 SA 密码。

## <a id="ctp30"></a> CTP 3.0 （5 月）

以下部分介绍的新功能和 SQL Server 2019 CTP 3.0 中的大数据群集的已知的问题。

### <a name="whats-new"></a>新增功能

| 新增功能或更新 | 详细信息 |
|:---|:---|
| mssqlctl 更新  | 多个 mssqlctl [命令和参数更新](../big-data-cluster/reference-mssqlctl.md)  。 这包括对“mssqlctl login”命令的更新，该命令现在以控制器用户名和终结点为目标  。 |
| 存储增强功能 | 支持日志和数据的不同存储配置。 此外，减少了大数据群集的持久卷声明数。 |
| 多个计算池实例 | 支持多个计算池实例。 |
| 新池行为和功能 | 现在，默认情况下，计算池仅用于“ROUND_ROBIN”分发中的存储池和数据池操作  。 数据池现在可以使用新的新“REPLICATED”分发类型，这意味着同一数据在所有数据池实例上都有  。 |
| 外部表的改进 | HADOOP 数据源类型的外部表现在支持读取最大 1 MB 的行。 外部表（ODBC、存储池、数据池）现在支持与 SQL Server 表一样宽的行。 |

### <a name="known-issues"></a>已知问题

以下部分介绍的已知的问题和在此版本的限制。

#### <a name="hdfs"></a>HDFS

- 当您尝试在 HDFS 中创建一个新的文件夹时，azure Data Studio 将返回错误。 若要启用此功能，安装 Azure Data Studio 的预览体验成员版本：
  
   - [Windows 用户的安装程序-**预览体验成员版本**](https://azuredatastudio-update.azurewebsites.net/latest/win32-x64-user/insider)
   - [Windows 系统安装程序-**预览体验成员版本**](https://azuredatastudio-update.azurewebsites.net/latest/win32-x64/insider)
   - [Windows ZIP-**预览体验成员版本**](https://azuredatastudio-update.azurewebsites.net/latest/win32-x64-archive/insider)
   - [macOS ZIP-**预览体验成员版本**](https://azuredatastudio-update.azurewebsites.net/latest/darwin/insider)
   - [Linux tar 文件。GZ-**预览体验成员版本**](https://azuredatastudio-update.azurewebsites.net/latest/linux-x64/insider)

- 如果右键单击来预览它的 HDFS 中的某个文件时，可能会看到以下错误：

   `Error previewing file: File exceeds max size of 30MB`

   目前没有办法来预览文件大于 30 MB 的 Azure Data Studio。

- 不支持对 HDFS 涉及对 hdfs-site.xml 更改的配置更改。

#### <a name="deployment"></a>部署

- 在 CTP 3.0 中不支持启用了 GPU 的大数据群集的上一个部署过程。 正在调查的备用部署过程。 现在，文章"部署大数据具有 GPU 支持的群集并运行 TensorFlow"具有已暂时未发布的以避免混淆。

- 不支持从以前的版本升级的大数据数据群集。

   > [!IMPORTANT]
   > 必须备份您的数据，然后删除现有的大数据群集 (使用以前版本的**mssqlctl**) 之前部署的最新版本。 有关详细信息，请参阅[升级到新版本](deployment-upgrade.md)。

- 在部署后在 AKS 上，可能会看到从部署的以下两个警告事件。 这两个这些事件已知问题，但它们不会阻止您成功部署 AKS 上的大数据群集。

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- 如果大数据群集部署失败，则不会删除关联的命名空间。 这可能导致在群集上的孤立命名空间。 一种解决方法是在部署具有相同名称的群集之前手动删除该命名空间。

#### <a name="external-tables"></a>外部表

- 大数据群集部署将不再创建**SqlDataPool**并**SqlStoragePool**外部数据源。 可以创建这些数据源手动来支持对数据池和存储池数据虚拟化。

   > [!NOTE]
   > 创建这些外部数据源的 URI 是 Ctp 之间的差异。 请参阅以下 TRANSACT-SQL 命令，请参阅如何创建它们 

   ```sql
   -- Create default data sources for SQL Big Data Cluster
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
       CREATE EXTERNAL DATA SOURCE SqlDataPool
       WITH (LOCATION = 'sqldatapool://controller-svc/default');
 
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
       CREATE EXTERNAL DATA SOURCE SqlStoragePool
       WITH (LOCATION = 'sqlhdfs://controller-svc/default');
   ```

- 它是可以创建一个表，其中包含不支持的列类型的数据池外部表。 如果查询外部表，您会收到类似于以下内容一条消息：

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- 如果查询存储池外部表，可能会遇到错误，如果基础文件要在同一时间复制到 HDFS。

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- 如果要创建向 Oracle 使用字符数据类型的外部表，Azure Data Studio 的虚拟化向导将这些列作为 VARCHAR 解释外部表定义中。 外部表 DDL 中，这将导致失败。 请修改使用 NVARCHAR2 类型，或手动创建 EXTERNAL TABLE 语句，而不是使用向导指定 NVARCHAR 的 Oracle 架构。

#### <a name="application-deployment"></a>应用程序部署

- 在从 RESTful API 调用 R、 Python 或 MLeap 应用程序，该调用将超时在 5 分钟内。

#### <a name="spark-and-notebooks"></a>Spark 和笔记本

- POD IP 地址可能会更改 Kubernetes 环境中，为 Pod 重新启动。 在 master pod 将重新启动的方案中，Spark 会话可能会因`NoRoteToHostException`。 这由于不使用新的 IP 获取刷新的 JVM 缓存的地址。

- 如果您有在 Windows 上的已安装的 Jupyter 和单独的 Python，Spark 笔记本可能会失败。 若要解决此问题，请升级到最新版本的 Jupyter。

- 在笔记本中，如果单击**添加文本**命令，在预览模式而非编辑模式中添加文本单元格。 您可以单击预览图标以切换到编辑模式和编辑该单元格。

#### <a name="security"></a>安全性

- SA_PASSWORD 是一部分的环境和可发现性 （例如在 cord 转储文件中）。 在部署后，必须重置 SA_PASSWORD 主实例上。 这不是一个 bug，但安全步骤。 有关如何更改 SA_PASSWORD Linux 容器中的详细信息，请参阅[更改 SA 密码](../linux/quickstart-install-connect-docker.md#sapassword)。

- AKS 日志可能包含用于大数据群集部署的 SA 密码。

## <a id="ctp25"></a> CTP 2.5 （年 4 月）

以下部分介绍的新功能和 SQL Server 2019 CTP 2.5 中的大数据群集的已知的问题。

### <a name="whats-new"></a>新增功能

| 新增功能或更新 | 详细信息 |
|:---|:---|
| 部署配置文件 | 使用默认和自定义[部署配置 JSON 文件](deployment-guidance.md#configfile)进行大数据群集部署，而不是使用环境变量。 |
| 提示的部署 | `mssqlctl cluster create` 现在会提示进行默认部署的任何必要设置。 |
| 服务终结点和 Pod 名称更改 | 以下外部终结点已更改名称：<br/>&nbsp;&nbsp;&nbsp;- **endpoint-master-pool** => **master-svc-external**<br/>&nbsp;&nbsp;&nbsp;- **endpoint-controller** => **controller-svc-external**<br/>&nbsp;&nbsp;&nbsp;- **endpoint-service-proxy** => **mgmtproxy-svc-external**<br/>&nbsp;&nbsp;&nbsp;- **endpoint-security** => **gateway-svc-external**<br/>&nbsp;&nbsp;&nbsp;- **endpoint-app-service-proxy** => **appproxy-svc-external**|
| mssqlctl 的改进  | 使用 mssqlctl [列出外部终结点](deployment-guidance.md#endpoints)，并通过 `--version` 参数检查 mssqlctl 的版本   。 |
| 脱机安装 | 对于脱机的大数据群集部署的指南。 |
| HDFS 分层的改进 | S3 分层、 装入缓存和 OAuth 支持 ADLS 第 2 代。 |
| 新`mssql`Spark SQL Server 连接器 | |

### <a name="known-issues"></a>已知问题

以下部分介绍的已知的问题和在此版本的限制。

#### <a name="deployment"></a>部署

- 不支持从以前的版本升级的大数据数据群集。

   > [!IMPORTANT]
   > 必须备份您的数据，然后删除现有的大数据群集 (使用以前版本的**mssqlctl**) 之前部署的最新版本。 有关详细信息，请参阅[升级到新版本](deployment-upgrade.md)。

- 在部署后在 AKS 上，可能会看到从部署的以下两个警告事件。 这两个这些事件已知问题，但它们不会阻止您成功部署 AKS 上的大数据群集。

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- 如果大数据群集部署失败，则不会删除关联的命名空间。 这可能导致在群集上的孤立命名空间。 一种解决方法是在部署具有相同名称的群集之前手动删除该命名空间。

#### <a name="external-tables"></a>外部表

- 大数据群集部署将不再创建**SqlDataPool**并**SqlStoragePool**外部数据源。 可以创建这些数据源手动来支持对数据池和存储池数据虚拟化。

   ```sql
   -- Create default data sources for SQL Big Data Cluster
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
       CREATE EXTERNAL DATA SOURCE SqlDataPool
       WITH (LOCATION = 'sqldatapool://service-mssql-controller:8080/datapools/default');
 
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
       CREATE EXTERNAL DATA SOURCE SqlStoragePool
       WITH (LOCATION = 'sqlhdfs://nmnode-0-svc:50070');
   ```

- 它是可以创建一个表，其中包含不支持的列类型的数据池外部表。 如果查询外部表，您会收到类似于以下内容一条消息：

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- 如果查询存储池外部表，可能会遇到错误，如果基础文件要在同一时间复制到 HDFS。

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- 如果要创建向 Oracle 使用字符数据类型的外部表，Azure Data Studio 的虚拟化向导将这些列作为 VARCHAR 解释外部表定义中。 外部表 DDL 中，这将导致失败。 请修改使用 NVARCHAR2 类型，或手动创建 EXTERNAL TABLE 语句，而不是使用向导指定 NVARCHAR 的 Oracle 架构。

#### <a name="application-deployment"></a>应用程序部署

- 在从 RESTful API 调用 R、 Python 或 MLeap 应用程序，该调用将超时在 5 分钟内。

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

## <a id="ctp24"></a> CTP 2.4 （年 3 月）

以下部分介绍的新功能和 SQL Server 2019 CTP 2.4 中的大数据群集的已知的问题。

### <a name="whats-new"></a>新增功能

| 新增功能或更新 | 详细信息 |
|:---|:---|
| 关于 GPU 支持在 Spark 中使用 TensorFlow 运行深度学习的指南。 | [部署具有 GPU 支持的大数据群集并运行 TensorFlow](spark-gpu-tensorflow.md)。 |
| 默认情况下，不再继续创建数据源 SqlDataPool 和 SqlStoragePool   。 | 请根据需要手动创建它们。 查看[已知问题](#externaltablesctp24)。 |
| 数据池的 `INSERT INTO SELECT` 支持。 | 有关示例，请参阅[教程：使用 Transact-SQL 将数据引入 SQL Server 数据池](tutorial-data-pool-ingest-sql.md)。 |
| `FORCE SCALEOUTEXECUTION` 和 `DISABLE SCALEOUTEXECUTION` 选项。 | 强制或禁用查询外部表的计算池的使用。 例如， `SELECT TOP(100) * FROM web_clickstreams_hdfs_book_clicks OPTION(FORCE SCALEOUTEXECUTION)` 。 |
| 更新的 AKS 部署建议。 | 当在 AKS 上评估大数据群集时，我们现在建议使用大小为 Standard_L8s 的单个节点  。 |
| Spark 运行时升级到 Spark 2.4。 | |

### <a name="known-issues"></a>已知问题

以下部分介绍的已知的问题和在此版本的限制。

#### <a name="deployment"></a>部署

- 不支持从以前的版本升级的大数据数据群集。

   > [!IMPORTANT]
   > 必须备份您的数据，然后删除现有的大数据群集 (使用以前版本的**mssqlctl**) 之前部署的最新版本。 有关详细信息，请参阅[升级到新版本](deployment-upgrade.md)。

- 在部署后在 AKS 上，可能会看到从部署的以下两个警告事件。 这两个这些事件已知问题，但它们不会阻止您成功部署 AKS 上的大数据群集。

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- 如果大数据群集部署失败，则不会删除关联的命名空间。 这可能导致在群集上的孤立命名空间。 一种解决方法是在部署具有相同名称的群集之前手动删除该命名空间。

#### <a name="kubeadm-deployments"></a>kubeadm 部署

如果您使用 kubeadm Kubernetes 部署多台计算机上，群集管理门户不正确显示连接到大数据群集所需的终结点。 如果遇到此问题，请使用以下解决方法来发现服务终结点 IP 地址：

- 如果从连接在群集中，查询你想要连接到的终结点的服务 IP Kubernetes。 例如，以下**kubectl**命令显示 SQL Server 主实例的 IP 地址：

   ```bash
   kubectl get service endpoint-master-pool -n <clusterName> -o=custom-columns="IP:.spec.clusterIP,PORT:.spec.ports[*].nodePort"
   ```

- 如果您正在连接从群集外部的使用以下步骤连接：

   1. 获取运行 SQL Server 主实例的节点的 IP 地址： `kubectl get pod mssql-master-pool-0 -o jsonpath="Name: {.metadata.name} Status: {.status.hostIP}" -n <clusterName>`。

   1. 连接到 SQL Server 主实例使用此 IP 地址。

   1. 查询**cluster_endpoint_table** master 数据库中的其他外部终结点。

      如果失败，并且连接超时，就可以单独节点之间设有防火墙。 在这种情况下，必须与 Kubernetes 群集管理员联系并要求向外部公开的节点 ip。 这可能是任何节点。 然后可以使用该 IP 和相应的端口连接到群集中运行的各种服务。 例如，管理员可以通过运行来查找此 IP:

      ```
      [root@m12hn01 config]# kubectl cluster-info
      Kubernetes master is running at https://172.50.253.99:6443
      KubeDNS is running at https://172.30.243.91:6443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
      ```

#### <a name="delete-cluster-fails"></a>删除群集失败

当你尝试删除包含的群集**mssqlctl**，将失败并出现以下错误：

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

新的 Python Kubernetes 客户端 （版本 9.0.0） 更改删除命名空间 API，这当前违反**mssqlctl**。 只有具有更高版本的 Kubernetes python 客户端安装时，才会出现此问题。 可以通过直接删除群集使用来解决此问题**kubectl** (`kubectl delete ns <ClusterName>`)，也可以使用较旧版本安装`sudo pip install kubernetes==8.0.1`。

#### <a id="externaltablesctp24"></a> 外部表

- 大数据群集部署将不再创建**SqlDataPool**并**SqlStoragePool**外部数据源。 可以创建这些数据源手动来支持对数据池和存储池数据虚拟化。

   ```sql
   -- Create default data sources for SQL Big Data Cluster
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
       CREATE EXTERNAL DATA SOURCE SqlDataPool
       WITH (LOCATION = 'sqldatapool://service-mssql-controller:8080/datapools/default');
 
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
       CREATE EXTERNAL DATA SOURCE SqlStoragePool
       WITH (LOCATION = 'sqlhdfs://service-master-pool:50070');
   ```

- 它是可以创建一个表，其中包含不支持的列类型的数据池外部表。 如果查询外部表，您会收到类似于以下内容一条消息：

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- 如果查询存储池外部表，可能会遇到错误，如果基础文件要在同一时间复制到 HDFS。

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- 如果要创建向 Oracle 使用字符数据类型的外部表，Azure Data Studio 的虚拟化向导将这些列作为 VARCHAR 解释外部表定义中。 外部表 DDL 中，这将导致失败。 请修改使用 NVARCHAR2 类型，或手动创建 EXTERNAL TABLE 语句，而不是使用向导指定 NVARCHAR 的 Oracle 架构。

#### <a name="application-deployment"></a>应用程序部署

- 在从 RESTful API 调用 R、 Python 或 MLeap 应用程序，该调用将超时在 5 分钟内。

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

## <a id="ctp23"></a> CTP 2.3 （年 2 月）

以下部分介绍的新功能和 SQL Server 2019 CTP 2.3 中的大数据群集的已知的问题。

### <a name="whats-new"></a>新增功能

| 新增功能或更新 | 详细信息 |
| :---------- | :------ |
| 在 IntelliJ 中的大数据群集上提交 Spark 作业。 | [在 IntelliJ 中的 SQL Server 大数据群集上提交 Spark 作业](spark-submit-job-intellij-tool-plugin.md) |
| 用于应用程序部署和群集管理的常见 CLI。 | [如何在 SQL Server 2019 大数据群集（预览版）上部署应用](big-data-cluster-create-apps.md) |
| 将应用程序部署到大数据群集的 VS Code 扩展。 | [如何使用 VS Code 将应用程序部署到 SQL Server 大数据群集](app-deployment-extension.md) |
| 对 mssqlctl 工具命令用法的更改  。 | 有关更多详细信息，请参阅 [mssqlctl 的已知问题](#mssqlctlctp23)。 |
| 在大数据群集中使用 Sparklyr | [在 SQL Server 2019 大数据群集中使用 Sparklyr](sparklyr-from-RStudio.md) |
| 通过 **HDFS 分层**将兼容 HDFS 的外部存储装入大数据群集。 | 请参阅 [HDFS 分层](hdfs-tiering.md)。 |
| SQL Server 主实例和 HDFS/Spark 网关的新的统一连接体验。 | 请参阅 [SQL Server 主实例和 HDFS/Spark 网关](connect-to-big-data-cluster.md)。 |
| 使用 mssqlctl cluster delete 命令删除群集现在仅删除属于大数据群集的命名空间中的对象  。 | 不会删除命名空间。 但是，在早期版本中，此命令会删除整个命名空间。 |
| 安全性终结点名称已更改并合并  。 | service-security-lb 和 service-security-nodeport 已合并到 endpoint-security 终结点中    。 |
| 代理终结点名称已更改并合并  。 | service-proxy-lb 和 service-proxy-nodeport 已合并到 endpoint-service-proxy 终结点中    。 |
| 控制器终结点名称已更改并合并  。 | service-mssql-controller-lb 和 service-mssql-controller-nodeport 已合并到 endpoint-controller 终结点中    。 |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>已知问题

以下部分介绍的已知的问题和在此版本的限制。

#### <a name="deployment"></a>部署

- 不支持从以前的版本升级的大数据数据群集。

   > [!IMPORTANT]
   > 必须备份您的数据，然后删除现有的大数据群集 (使用以前版本的**mssqlctl**) 之前部署的最新版本。 有关详细信息，请参阅[升级到新版本](deployment-upgrade.md)。

- **ACCEPT_EULA**环境变量必须是"yes"是"以接受 EULA。 以前的版本中允许使用"y"和"Y"，但这些不再被接受，并将导致部署失败。

- **CLUSTER_PLATFORM**像在以前的版本中，环境变量不具有默认值。

- 在部署后在 AKS 上，可能会看到从部署的以下两个警告事件。 这两个这些事件已知问题，但它们不会阻止您成功部署 AKS 上的大数据群集。

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- 如果大数据群集部署失败，则不会删除关联的命名空间。 这可能导致在群集上的孤立命名空间。 一种解决方法是在部署具有相同名称的群集之前手动删除该命名空间。

#### <a name="kubeadm-deployments"></a>kubeadm 部署

如果您使用 kubeadm Kubernetes 部署多台计算机上，群集管理门户不正确显示连接到大数据群集所需的终结点。 如果遇到此问题，请使用以下解决方法来发现服务终结点 IP 地址：

- 如果从连接在群集中，查询你想要连接到的终结点的服务 IP Kubernetes。 例如，以下**kubectl**命令显示 SQL Server 主实例的 IP 地址：

   ```bash
   kubectl get service endpoint-master-pool -n <clusterName> -o=custom-columns="IP:.spec.clusterIP,PORT:.spec.ports[*].nodePort"
   ```

- 如果您正在连接从群集外部的使用以下步骤连接：

   1. 获取运行 SQL Server 主实例的节点的 IP 地址： `kubectl get pod mssql-master-pool-0 -o jsonpath="Name: {.metadata.name} Status: {.status.hostIP}" -n <clusterName>`。

   1. 连接到 SQL Server 主实例使用此 IP 地址。

   1. 查询**cluster_endpoint_table** master 数据库中的其他外部终结点。

      如果失败，并且连接超时，就可以单独节点之间设有防火墙。 在这种情况下，必须与 Kubernetes 群集管理员联系并要求向外部公开的节点 ip。 这可能是任何节点。 然后可以使用该 IP 和相应的端口连接到群集中运行的各种服务。 例如，管理员可以通过运行来查找此 IP:

      ```
      [root@m12hn01 config]# kubectl cluster-info
      Kubernetes master is running at https://172.50.253.99:6443
      KubeDNS is running at https://172.30.243.91:6443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
      ```

#### <a id="mssqlctlctp23"></a> mssqlctl

- **Mssqlctl**工具更改从动词-名词命令名词谓词顺序的排序。 例如，`mssqlctl create cluster`现在`mssqlctl cluster create`。

- `--name`参数现在是在创建与群集时所需`mssqlctl cluster create`。

   ```bash
   mssqlctl cluster create --name <cluster_name>
   ```

- 有关升级到最新版本的大数据群集的重要信息和**mssqlctl**，请参阅[升级到新版本](deployment-upgrade.md)。

#### <a name="external-tables"></a>外部表

- 它是可以创建一个表，其中包含不支持的列类型的数据池外部表。 如果查询外部表，您会收到类似于以下内容一条消息：

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- 如果查询存储池外部表，可能会遇到错误，如果基础文件要在同一时间复制到 HDFS。

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- 如果要创建向 Oracle 使用字符数据类型的外部表，Azure Data Studio 的虚拟化向导将这些列作为 VARCHAR 解释外部表定义中。 外部表 DDL 中，这将导致失败。 请修改使用 NVARCHAR2 类型，或手动创建 EXTERNAL TABLE 语句，而不是使用向导指定 NVARCHAR 的 Oracle 架构。

#### <a name="application-deployment"></a>应用程序部署

- 在从 RESTful API 调用 R、 Python 或 MLeap 应用程序，该调用将超时在 5 分钟内。

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

## <a id="ctp22"></a> CTP 2.2 (2018 年 12 月)

以下部分介绍的新功能和 SQL Server 2019 CTP 2.2 中的大数据群集的已知的问题。

### <a name="new-features"></a>新增功能

- 使用群集管理门户的访问`/portal`(**https://\<ip 地址\>: 30777/门户**)。
- 更改从主池服务名称`service-master-pool-lb`并`service-master-pool-nodeport`到`endpoint-master-pool`。
- 新版本**mssqlctl**和更新映像。
- 其他 bug 修复和改进。

### <a name="known-issues"></a>已知问题

以下部分介绍的已知的问题和在此版本的限制。

#### <a name="deployment"></a>部署

- 不支持从以前的版本升级的大数据数据群集。 必须备份和部署最新版本之前删除任何现有的大数据群集。 有关详细信息，请参阅[升级到新版本](deployment-upgrade.md)。

- 在部署后在 AKS 上，可能会看到从部署的以下两个警告事件。 这两个这些事件已知问题，但它们不会阻止您成功部署 AKS 上的大数据群集。

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- 如果大数据群集部署失败，则不会删除关联的命名空间。 这可能导致在群集上的孤立命名空间。 一种解决方法是在部署具有相同名称的群集之前手动删除该命名空间。

#### <a name="cluster-administration-portal"></a>群集管理门户

群集管理门户不显示 SQL Server 主实例的终结点。 若要查找的主实例的 IP 地址和端口，请使用以下**kubectl**命令：

```
kubectl get svc endpoint-master-pool -n <your-big-data-cluster-name>
```

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

## <a id="ctp21"></a> CTP 2.1 (2018 年 11 月)

以下部分介绍的新功能和 SQL Server 2019 CTP 2.1 中的大数据群集的已知的问题。

### <a name="new-features"></a>新增功能

- [将 Python 和 R 的应用部署](big-data-cluster-create-apps.md)大数据群集中。
- 新版本**mssqlctl**和更新映像。 
- 其他 bug 修复和改进。

### <a name="known-issues"></a>已知问题

以下部分提供有关 SQL Server CTP 2.1 中的大数据群集的已知的问题。

#### <a name="deployment"></a>部署

- 不支持从以前的版本升级的大数据数据群集。 必须备份和部署最新版本之前删除任何现有的大数据群集。 有关详细信息，请参阅[升级到新版本](deployment-upgrade.md)。

- 在部署后在 AKS 上，可能会看到从部署的以下两个警告事件。 这两个这些事件已知问题，但它们不会阻止您成功部署 AKS 上的大数据群集。

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- 如果大数据群集部署失败，则不会删除关联的命名空间。 这可能导致在群集上的孤立命名空间。 一种解决方法是在部署具有相同名称的群集之前手动删除该命名空间。

#### <a name="admin-portal"></a>管理门户

- 当您[使用 msqlctl ctp 命令创建应用](big-data-cluster-create-apps.md)并将其部署大数据群集，群集管理员门户显示了 pod 为"未知"的管理员部分的控制器部分中部署应用程序所在的 SQL Server 上。

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

## <a id="ctp20"></a> CTP 2.0 (2018 年 10 月)

以下部分介绍的新功能和 SQL Server 2019 CTP 2.0 中的大数据群集的已知的问题。

### <a name="new-features"></a>新增功能

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
