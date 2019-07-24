---
title: 配置 HDFS 分层
titleSuffix: SQL Server big data clusters
description: 本文介绍如何配置 HDFS 分层, 以将外部 Azure Data Lake Storage 文件系统装载到 SQL Server 2019 大数据群集 (预览版) 上的 HDFS 中。
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 17eedf9f0797a0adb5eda6ca8ee090fc762e1491
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419374"
---
# <a name="configure-hdfs-tiering-on-sql-server-big-data-clusters"></a>在 SQL Server 大数据群集上配置 HDFS 分层

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

HDFS 分层可以在 HDFS 中装载与 HDFS 兼容的外部文件系统。 本文介绍如何为 SQL Server 2019 大数据群集 (预览版) 配置 HDFS 分层。 目前, 我们支持连接到 Azure Data Lake Storage Gen2 和 Amazon S3。 

## <a name="hdfs-tiering-overview"></a>HDFS 分层概述

使用分层, 应用程序可以无缝访问各种外部存储区中的数据, 就像数据驻留在本地 HDFS 中一样。 装载是一种元数据操作, 其中描述外部文件系统上的命名空间的元数据将复制到本地 HDFS。 此元数据包括有关外部目录和文件及其权限和 Acl 的信息。 当通过 (例如查询) 访问数据本身时, 只按需复制相应的数据。 现在可以从 SQL Server 大数据群集访问外部文件系统数据。 你可以对此数据运行 Spark 作业和 SQL 查询, 其方式与在群集上的 HDFS 中存储的任何本地数据相同。

### <a name="caching"></a>Caching
默认情况下, 默认情况下, 将保留总共 1% 的 HDFS 存储空间来缓存装载的数据。 缓存是跨装载的全局设置。

> [!NOTE]
> HDFS 分层是由 Microsoft 开发的一项功能, 其早期版本已作为 Apache Hadoop 3.1 分发的一部分发布。 有关详细信息, 请[https://issues.apache.org/jira/browse/HDFS-9806](https://issues.apache.org/jira/browse/HDFS-9806)参阅获取详细信息。

以下各节提供了有关如何使用 Azure Data Lake Storage Gen2 数据源配置 HDFS 分层的示例。

## <a name="refresh"></a>刷新

HDFS 分层支持刷新。 刷新现有装载以获取远程数据的最新快照。

## <a name="prerequisites"></a>先决条件

- [已部署大数据群集](deployment-guidance.md)
- [大数据工具](deploy-big-data-tools.md)
  - **azdata**
  - **kubectl**

## <a name="mounting-instructions"></a>安装说明

支持连接到 Azure Data Lake Storage Gen2 和 Amazon S3。 有关如何针对这些存储类型进行装载的说明, 请参阅以下文章:

- [如何在大数据群集中装载 HDFS 分层 ADLS Gen2](hdfs-tiering-mount-adlsgen2.md)
- [如何在大数据群集中为 HDFS 分层装载 S3](hdfs-tiering-mount-s3.md)

## <a id="issues"></a>已知问题和限制

以下列表提供了在 SQL Server 大数据群集中使用 HDFS 分层时的已知问题和当前限制:

- 如果装载处于`CREATING`长时间状态, 则很可能已失败。 在这种情况下, 请取消命令, 并在必要时删除装入。 请在重试之前验证你的参数和凭据是否正确。

- 无法在现有目录上创建装载。

- 无法在现有装载内创建装载。

- 如果装入点的任何祖先节点不存在, 则将创建其权限默认为 r-xr-xr (555) 的。

- 装载创建可能需要一些时间, 具体取决于要装入的文件的数量和大小。 在此过程中, 用户无法看到装载下的文件。 创建装载时, 会将所有文件添加到临时路径, 默认值为`/_temporary/_mounts/<mount-location>`。

- 装载创建命令是异步的。 运行该命令后, 可以检查装载状态以了解装载状态。

- 创建装载时, 用于 **--装载路径**的参数实质上是装载的唯一标识符。 必须在后续命令中使用相同的字符串 (包含结尾的 "/" (如果存在)。

- 装载为只读。 不能在装入时创建任何目录或文件。

- 不建议装载可以更改的目录和文件。 创建装载后, 对远程位置所做的任何更改或更新都不会反映在 HDFS 中的装载。 如果在远程位置发生更改, 则可以选择删除并重新创建装载, 以反映已更新的状态。

## <a name="next-steps"></a>后续步骤

有关 SQL Server 2019 大数据群集的详细信息, 请参阅[什么是 SQL Server 2019 大数据群集？](big-data-cluster-overview.md)。
