---
title: 配置 HDFS 分层
titleSuffix: SQL Server big data clusters
description: 本文介绍如何配置 HDFS 的分层，从而在 SQL Server 2019 大数据群集 （预览版） 上装载到 HDFS 的外部的 Azure Data Lake 存储文件系统。
author: nelgson
ms.author: negust
ms.reviewer: mikeray
manager: jroth
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 823e24b4ec78996140fa3f17cef9c1e56365a3f7
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/10/2019
ms.locfileid: "67728733"
---
# <a name="configure-hdfs-tiering-on-sql-server-big-data-clusters"></a>配置 SQL Server 大数据群集上分层的 HDFS

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

HDFS 分层提供的功能来装载外部的在 HDFS 中的 HDFS 兼容文件系统。 本文介绍如何配置 SQL Server 2019 大数据群集 （预览版） 为分层的 HDFS。 在此期间，我们支持连接到 Azure 数据湖存储第 2 代和 Amazon S3。 

## <a name="hdfs-tiering-overview"></a>HDFS 分层概述

使用分层，应用程序可以无缝访问很多外部存储区中的数据，就像数据驻留在本地 HDFS。 装载是元数据操作，其中介绍在外部文件系统的命名空间的元数据复制到本地 HDFS。 此元数据包括有关外部目录和文件以及其权限和 Acl 的信息。 通过例如的查询访问数据本身时，相应的数据是仅复制的按需。 现在可以从 SQL Server 大数据群集访问的外部文件系统数据。 可以运行 Spark 作业和 SQL 查询对此数据将存储在 HDFS 群集上的任何本地数据上运行它们一样。

### <a name="caching"></a>Caching
现在，默认情况下，将为已装载的数据的缓存保留的总存储，HDFS 的 1%。 缓存是一种全局设置跨装载。

> [!NOTE]
> HDFS 分层是 Microsoft 开发的功能，已作为 Apache Hadoop 3.1 分发的一部分发布的早期版本。 有关详细信息，请参阅[ https://issues.apache.org/jira/browse/HDFS-9806 ](https://issues.apache.org/jira/browse/HDFS-9806)有关详细信息。

以下部分提供如何配置 HDFS 分层与 Azure 数据湖存储第 2 代数据源的示例。

## <a name="prerequisites"></a>先决条件

- [已部署的大数据群集](deployment-guidance.md)
- [大数据工具](deploy-big-data-tools.md)
  - **mssqlctl**
  - **kubectl**

## <a name="mounting-instructions"></a>装载说明

我们支持连接到 Azure 数据湖存储第 2 代和 Amazon S3。 如何将安装对这些存储类型的说明可在以下文章：

- [如何装载 ADLS hdfs 分层大数据群集中的第 2 代](hdfs-tiering-mount-adlsgen2.md)
- [如何装载 S3 分层大数据群集中的 hdfs](hdfs-tiering-mount-s3.md)

## <a id="issues"></a> 已知的问题和限制

使用分层在 SQL Server 大数据群集中的 HDFS 时，以下列表提供了已知的问题和当前限制：

- 如果装载陷入`CREATING`状态的时间长，它很可能已失败。 在此情况下，取消该命令并删除装入，如有必要。 验证您的参数和凭据正确重试之前。

- 不能在现有目录上创建装载。

- 不能在现有装载创建装载。

- 如果不存在任何装入点的祖先，则将创建的权限默认为 r-xr-xr-x (555)。

- 装入创建可能需要一些时间，具体取决于的数量和装载的文件的大小。 在此过程中下装载, 的文件不会对用户可见。 虽然创建装载，但所有文件将都添加到临时路径，默认为`/_temporary/_mounts/<mount-location>`。

- 装入创建命令是异步的。 运行该命令后，可以检查装入状态，以了解装入状态。

- 在创建时装载，参数用于 **-安装路径**是实质上是装载的唯一标识符。 在后续命令中，必须使用相同的字符串 （包括"/"最后，如果存在）。

- 装载是只读的。 无法创建任何目录或下装载的文件。

- 我们不建议装载目录和文件，可以更改。 创建装载后，任何更改或更新到远程位置将不会反映在 HDFS 中装入。 如果在远程位置中发生更改，可以选择删除并重新创建装入以反映已更新的状态。

## <a name="next-steps"></a>后续步骤

有关 SQL Server 2019 大数据群集的详细信息，请参阅[什么是 SQL Server 2019 大数据群集？](big-data-cluster-overview.md)。
