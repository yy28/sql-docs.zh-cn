---
title: 为 HDFS 分层装入 S3
titleSuffix: SQL Server big data clusters
description: 本文介绍如何配置分层外部 S3 文件系统装载到 HDFS，SQL Server 2019 大数据群集 （预览版） 上的 HDFS。
author: nelgson
ms.author: negust
ms.reviewer: jroth
manager: craigg
ms.date: 04/15/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 79c09d5bcff26c9f5867e5b0fb38bd019b681b5c
ms.sourcegitcommit: 89abd4cd4323ae5ee284571cd69a9fe07d869664
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
ms.locfileid: "64330593"
---
# <a name="how-to-mount-s3-for-hdfs-tiering-in-a-big-data-cluster"></a>如何装载 S3 分层大数据群集中的 hdfs

以下部分提供如何配置 HDFS 分层 S3 存储数据源的示例。

## <a name="prerequisites"></a>先决条件

- [已部署的大数据群集](deployment-guidance.md)
- [大数据工具](deploy-big-data-tools.md)
  - **mssqlctl**
  - **kubectl**
- 创建并将数据上传到 S3 存储桶 
  - 上传 CSV 或 Parquet 文件复制到 S3 存储桶。 这是将装载到 HDFS 的大数据群集中的外部 HDFS 数据。

## <a name="access-keys"></a>访问密钥

1. 打开命令提示符可以访问你的大数据群集的客户端计算机上。

1. 创建一个名为的本地文件**filename.creds** ，其中包含你使用以下格式的 S3 帐户凭据：

   ```text
    fs.s3a.access.key=<Access Key ID of the key>
    fs.s3a.secret.key=<Secret Access Key of the key>
   ```

   > [!TIP]
   > 有关如何创建 S3 访问密钥的详细信息，请参阅[S3 访问密钥](https://docs.aws.amazon.com/general/latest/gr/aws-sec-cred-types.html#access-keys-and-secret-access-keys)。

## <a id="mount"></a> 将远程 HDFS 存储装载

现在，你的凭据文件准备好使用访问密钥，可以开始安装。 以下步骤将在 S3 到本地 HDFS 存储大数据群集的远程 HDFS 存储装载。

1. 使用**kubectl**若要查找的 IP 地址**mgmtproxy svc 外部**大数据群集中的服务。 寻找**外部 IP**。

   ```bash
   kubectl get svc mgmtproxy-svc-external -n <your-cluster-name>
   ```

1. 登录方式**mssqlctl**管理代理终结点的外部 IP 地址使用你的群集用户名和密码：

   ```bash
   mssqlctl login -e https://<IP-of-mgmtproxy-svc-external>:30777/ -u <username> -p <password>
   ```

1. 将在 Azure 中使用远程 HDFS 存储装载**mssqlctl 存储装载创建**。 将占位符值替换为之前运行以下命令：

   ```bash
   mssqlctl storage mount create --remote-uri s3a://<S3 bucket name> --mount-path /mounts/<mount-name> --credential-file <path-to-s3-credentials>/file.creds
   ```

   > [!NOTE]
   > 装载创建命令是异步的。 在此期间，没有任何消息，指示是否已成功装载。 请参阅[状态](#status)部分，以检查你装载的状态。

如果安装成功，您应该能够查询 HDFS 数据并对其运行 Spark 作业。 它将出现在指定的位置中的大数据群集的 HDFS `--mount-path`。

## <a id="status"></a> 获取装载的状态

若要列出的大数据群集中的所有装载状态，请使用以下命令：

```bash
mssqlctl storage mount status
```

若要列出的在 HDFS 中的特定路径装载状态，请使用以下命令：

```bash
mssqlctl storage mount status --mount-path <mount-path-in-hdfs>
```

## <a id="delete"></a> 删除装载

若要删除装载，请使用**mssqlctl 存储装载删除**命令，并在 HDFS 中指定的装载路径：

```bash
mssqlctl storage mount delete --mount-path <mount-path-in-hdfs>
```

## <a name="next-steps"></a>后续步骤

有关 SQL Server 2019 大数据群集的详细信息，请参阅[什么是 SQL Server 2019 大数据群集？](big-data-cluster-overview.md)。
