---
title: 为 HDFS 分层装入 S3
titleSuffix: SQL Server big data clusters
description: 本文介绍如何配置 HDFS 分层, 以将外部 S3 文件系统装载到 SQL Server 2019 大数据群集 (预览版) 上的 HDFS 中。
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 28c80d6076f07c8a4f1605149f4b5c730c8349a1
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419336"
---
# <a name="how-to-mount-s3-for-hdfs-tiering-in-a-big-data-cluster"></a>如何在大数据群集中为 HDFS 分层装载 S3

以下部分提供了如何使用 S3 存储数据源配置 HDFS 分层的示例。

## <a name="prerequisites"></a>先决条件

- [已部署大数据群集](deployment-guidance.md)
- [大数据工具](deploy-big-data-tools.md)
  - **azdata**
  - **kubectl**
- 创建数据并将其上传到 S3 存储桶 
  - 将 CSV 或 Parquet 文件上传到 S3 存储桶。 这是将装载到大数据群集中的 HDFS 的外部 HDFS 数据。

## <a name="access-keys"></a>访问密钥

### <a name="set-environment-variable-for-access-key-credentials"></a>设置访问密钥凭据的环境变量

在可以访问大数据群集的客户端计算机上打开命令提示符。 使用以下格式设置环境变量。 请注意, 凭据需要位于以逗号分隔的列表中。 "Set" 命令在 Windows 上使用。 如果使用的是 Linux, 请改用 "export"。

   ```text
    set MOUNT_CREDENTIALS=fs.s3a.access.key=<Access Key ID of the key>,
    fs.s3a.secret.key=<Secret Access Key of the key>
   ```

   > [!TIP]
   > 有关如何创建 S3 访问密钥的详细信息, 请参阅[s3 访问密钥](https://docs.aws.amazon.com/general/latest/gr/aws-sec-cred-types.html#access-keys-and-secret-access-keys)。

## <a id="mount"></a>装载远程 HDFS 存储

现在, 你已准备好带有访问密钥的凭据文件, 接下来可以开始安装。 以下步骤将 S3 中的远程 HDFS 存储装载到大数据群集的本地 HDFS 存储中。

1. 使用**kubectl**在大数据群集中查找终结点**控制器-svc-外部**服务的 IP 地址。 查找**外部 IP**。

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

1. 使用群集用户名和密码通过控制器终结点的外部 IP 地址登录**azdata** :

   ```bash
   azdata login -e https://<IP-of-controller-svc-external>:30080/
   ```
   
1. 按照上述说明设置环境变量 MOUNT_CREDENTIALS

1. 使用**azdata bdc 存储池装载创建**在 Azure 中装载远程 HDFS 存储。 运行以下命令之前, 请替换占位符值:

   ```bash
   azdata bdc storage-pool mount create --remote-uri s3a://<S3 bucket name> --mount-path /mounts/<mount-name>
   ```

   > [!NOTE]
   > 装载 create 命令是异步的。 此时, 没有消息指示装载是否成功。 请参阅 "[状态](#status)" 部分以检查装载状态。

如果安装成功, 则应该能够查询 HDFS 数据并对其运行 Spark 作业。 它将显示在由`--mount-path`指定的位置中的大数据群集的 HDFS 中。

## <a id="status"></a>获取装入状态

若要列出大数据群集中所有装载的状态, 请使用以下命令:

```bash
azdata bdc storage-pool mount status
```

若要在 HDFS 中列出特定路径下的装入状态, 请使用以下命令:

```bash
azdata bdc storage-pool mount status --mount-path <mount-path-in-hdfs>
```

## <a name="refresh-a-mount"></a>刷新装载

以下示例刷新装入。

```bash
azdata bdc hdfs mount refresh --mount-path <mount-path-in-hdfs>
```

## <a id="delete"></a>删除装载

若要删除装载, 请使用**azdata bdc 存储池装载 delete**命令, 并在 HDFS 中指定装载路径:

```bash
azdata bdc storage-pool mount delete --mount-path <mount-path-in-hdfs>
```

## <a name="next-steps"></a>后续步骤

有关 SQL Server 2019 大数据群集的详细信息, 请参阅[什么是 SQL Server 2019 大数据群集？](big-data-cluster-overview.md)。
