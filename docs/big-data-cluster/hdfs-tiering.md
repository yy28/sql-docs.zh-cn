---
title: 配置 HDFS 分层
titleSuffix: SQL Server 2019 big data clusters
description: 本文介绍如何配置 HDFS 的分层，从而在 SQL Server 2019 大数据群集 （预览版） 上装载到 HDFS 的外部的 Azure Data Lake 存储文件系统。
author: nelgson
ms.author: negust
ms.reviewer: jroth
manager: craigg
ms.date: 02/29/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 04f493109997d4b673a6a308de5c9ebee6eac7e4
ms.sourcegitcommit: 56fb7b648adae2c7b81bd969de067af1a2b54180
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/02/2019
ms.locfileid: "57239122"
---
# <a name="configure-hdfs-tiering-on-sql-server-2019-big-data-clusters"></a>配置 SQL Server 2019 大数据群集上分层的 HDFS

HDFS 分层提供的功能来装载外部的在 HDFS 中的 HDFS 兼容文件系统。 本文介绍如何配置 SQL Server 2019 大数据群集 （预览版） 为分层的 HDFS。 在此期间，CTP 2.3 会仅支持连接到 Azure 数据湖存储第 2 代，这是本文的重点。

## <a name="hdfs-tiering-overview"></a>HDFS 分层概述

使用分层，应用程序可以无缝访问很多外部存储区中的数据，就像数据驻留在 HDFS 中。 装载是元数据操作，其中介绍在外部文件系统的命名空间的元数据复制到 HDFS。 此元数据包括有关外部目录和文件以及其权限和 Acl 的信息。 相应的数据是仅复制的按需访问数据本身时。 现在可以从 SQL Server 大数据群集访问的外部文件系统数据。 可以运行 Spark 作业和 SQL 查询对此数据将存储在 HDFS 群集上的任何本地数据上运行它们一样。

> [!NOTE]
> HDFS 分层是 Microsoft 开发的功能，已作为 Apache Hadoop 3.1 分发的一部分发布的早期版本。 有关详细信息，请参阅[ https://issues.apache.org/jira/browse/HDFS-9806 ](https://issues.apache.org/jira/browse/HDFS-9806)有关详细信息。

以下部分提供如何配置 HDFS 分层与 Azure 数据湖存储第 2 代数据源的示例。

## <a name="prerequisites"></a>先决条件

- [已部署的大数据群集](deployment-guidance.md)
- [大数据工具](deploy-big-data-tools.md)
  - **mssqlctl**
  - **kubectl**

## <a id="load"></a> 将数据加载到 Azure Data Lake 存储

以下部分介绍如何设置用于测试 HDFS 分层的 Azure 数据湖存储第 2 代。 如果已在 Azure Data Lake 存储中存储的数据，则可以跳过此部分以使用你自己的数据。

1. [创建存储帐户与数据湖存储第 2 代功能](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-quickstart-create-account)。

1. [创建 blob 容器](https://docs.microsoft.com/azure/storage/blobs/storage-quickstart-blobs-portal)外部数据此存储帐户中。

1. 将 CSV 或 Parquet 文件上传到容器。 这是将装载到 HDFS 的大数据群集中的外部 HDFS 数据。

## <a id="mount"></a> 将远程 HDFS 存储装载

以下步骤将 Azure Data Lake 中到本地 HDFS 存储中的大数据群集远程 HDFS 存储装载。

1. 打开命令提示符可以访问你的大数据群集的客户端计算机上。

1. 创建一个名为的本地文件**files.creds** ，其中包含你使用以下格式的 Azure 数据湖存储第 2 代帐户凭据：

   ```text
   fs.azure.abfs.account.name=<your-storage-account-name>.dfs.core.windows.net
   fs.azure.account.key.<your-storage-account-name>.dfs.core.windows.net=<storage-account-access-key>
   ```

   > [!TIP]
   > 有关如何查找访问密钥的详细信息 (`<storage-account-access-key>`) 你的存储帐户，请参阅[查看和复制访问密钥](https://docs.microsoft.com/azure/storage/common/storage-account-manage?#view-and-copy-access-keys)。

1. 使用**kubectl**若要查找的 IP 地址**终结点服务代理**大数据群集中的服务。 寻找**外部 IP**。

   ```bash
   kubectl get svc endpoint-service-proxy -n <your-cluster-name>
   ```

1. 登录方式**mssqlctl**服务代理终结点使用你的群集用户名和密码：

   ```bash
   mssqlctl login -e https://<IP-of-endpoint-service-proxy>:30777/ -u <username> -p <password>
   ```

1. 将在 Azure 中使用远程 HDFS 存储装载**mssqlctl 存储装载创建**。 将占位符值替换为之前运行以下命令：

   ```bash
   mssqlctl storage mount create --remote-uri abfs://<blob-container-name>@<storage-account-name>.dfs.core.windows.net/ --local-path /mounts/<mount-name> --credential-file <path-to-adls-credentials>/file.creds
   ```

   > [!NOTE]
   > 装载创建命令是异步的。 在此期间，没有任何消息，指示是否已成功装载。 请参阅[状态](#status)部分，以检查你装载的状态。

如果安装成功，您应该能够查询 HDFS 数据并对其运行 Spark 作业。 它将出现在指定的位置中的大数据群集的 HDFS `--local-path`。

## <a id="status"></a> 获取装载的状态

若要列出的大数据群集中的所有装载状态，请使用以下命令：

```bash
mssqlctl storage mount status
```

若要列出的在 HDFS 中的特定路径装载状态，请使用以下命令：

```bash
mssqlctl storage mount status --local-path <mount-path-in-hdfs>
```

## <a id="delete"></a> 删除装载

若要删除装载，请使用**mssqlctl 存储装载删除**命令，并在 HDFS 中指定的装载路径：

```bash
mssqlctl storage mount delete --local-path <mount-path-in-hdfs>
```

## <a id="issues"></a> 已知的问题和限制

使用分层在 SQL Server 大数据群集中的 HDFS 时，以下列表提供了已知的问题和当前限制：

- 如果所装入的外部目录的大小大于此群集的容量，装载失败。

- 如果装载陷入`CREATING`状态的时间长，它很可能已失败。 在此情况下，取消该命令并删除装入，如有必要。 验证您的参数和凭据正确重试之前。

- 不能在现有目录上创建装载。

- 不能在现有装载创建装载。

- 如果不存在任何装入点的祖先，则将创建的权限默认为 r-xr-xr-x (555)。

- 装入创建可能需要一些时间，具体取决于的数量和装载的文件的大小。 在此过程中下装载, 的文件不会对用户可见。 虽然创建装载，但所有文件将都添加到临时路径，默认为`/_temporary/_mounts/<mount-location>`。

- 装入创建命令是异步的。 运行该命令后，可以检查装入状态，以了解装入状态。

- 在创建时装载，参数用于 **-本地路径**是实质上是装载的唯一标识符。 在后续命令中，必须使用相同的字符串 （包括"/"最后，如果存在）。

- 装载是只读的。 无法创建任何目录或下装载的文件。

- 我们不建议装载目录和文件，可以更改。 创建装载后，任何更改或更新到远程位置将不会反映在 HDFS 中装入。 如果在远程位置中发生更改，可以选择删除并重新创建装入以反映已更新的状态。

## <a name="next-steps"></a>后续步骤

有关 SQL Server 2019 大数据群集的详细信息，请参阅[什么是 SQL Server 2019 大数据群集？](big-data-cluster-overview.md)。