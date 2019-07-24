---
title: 为 HDFS 分层装入 ADLS Gen2
titleSuffix: How to mount ADLS Gen2
description: 本文介绍如何配置 HDFS 分层, 以将外部 Azure Data Lake Storage 文件系统装载到 SQL Server 2019 大数据群集 (预览版) 上的 HDFS 中。
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d7d8a6dd53452700853dca9774ed0196ed7546fe
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419345"
---
# <a name="how-to-mount-adls-gen2-for-hdfs-tiering-in-a-big-data-cluster"></a>如何在大数据群集中装载 HDFS 分层 ADLS Gen2

以下各节提供了有关如何使用 Azure Data Lake Storage Gen2 数据源配置 HDFS 分层的示例。

## <a name="prerequisites"></a>先决条件

- [已部署大数据群集](deployment-guidance.md)
- [大数据工具](deploy-big-data-tools.md)
  - **azdata**
  - **kubectl**

## <a id="load"></a>将数据加载到 Azure Data Lake Storage

以下部分介绍如何设置用于测试 HDFS 分层的 Azure Data Lake Storage Gen2。 如果已将数据存储在 Azure Data Lake Storage 中, 则可以跳过此部分以使用自己的数据。

1. [创建具有 Data Lake Storage Gen2 功能的存储帐户](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-quickstart-create-account)。

1. 在此存储帐户中为外部数据[创建 blob 容器](https://docs.microsoft.com/azure/storage/blobs/storage-quickstart-blobs-portal)。

1. 将 CSV 或 Parquet 文件上传到容器中。 这是将装载到大数据群集中的 HDFS 的外部 HDFS 数据。

## <a name="credentials-for-mounting"></a>用于装载的凭据

## <a name="use-oauth-credentials-to-mount"></a>使用 OAuth 凭据进行装载

为了使用 OAuth 凭据进行装载, 你需要执行以下步骤:

1. 中转到[Azure 门户](https://portal.azure.com)
1. 在左侧导航窗格中, 依次指向 "服务" 和 "Azure Active Directory"
1. 使用菜单中的 "应用注册", 创建 "Web 应用程序", 然后按照向导操作。 **请记住你在此处创建的名称**。 需要将此名称作为授权用户添加到 ADLS 帐户。
1. 创建 web 应用程序后, 请在应用程序的 "设置" 下中转到 "密钥"。
1. 选择一个密钥持续时间, 并单击 "保存"。 **保存生成的密钥。**
1.  返回到 "应用注册" 页, 单击顶部的 "终结点" 按钮。 **记下 "令牌终结点" URL**
1. 对于 OAuth, 你现在应记下以下内容:

    - 你在步骤3中创建的 Web 应用的 "应用程序 ID"
    - 在步骤5中刚刚生成的密钥
    - 步骤6中的令牌终结点

### <a name="adding-the-service-principal-to-your-adls-account"></a>将服务主体添加到你的 ADLS 帐户

1. 再次访问门户并打开 ADLS 帐户, 然后在左侧菜单中选择 "访问控制 (IAM)"。
1. 选择 "添加角色分配", 然后搜索在上面的步骤3中创建的名称 (请注意, 它不会显示在列表中, 但如果你搜索全名, 则会找到此名称)。
1. 现在添加 "存储 Blob 数据参与者 (预览版)" 角色。

请等待5-10 分钟, 然后再使用用于装载的凭据

### <a name="set-environment-variable-for-oauth-credentials"></a>为 OAuth 凭据设置环境变量

在可以访问大数据群集的客户端计算机上打开命令提示符。 使用以下格式设置环境变量:请注意, 凭据需要位于以逗号分隔的列表中。 "Set" 命令在 Windows 上使用。 如果使用的是 Linux, 请改用 "export"。

   ```text
    set MOUNT_CREDENTIALS=fs.azure.account.auth.type=OAuth,
    fs.azure.account.oauth.provider.type=org.apache.hadoop.fs.azurebfs.oauth2.ClientCredsTokenProvider,
    fs.azure.account.oauth2.client.endpoint=[token endpoint from step6 above],
    fs.azure.account.oauth2.client.id=[<Application ID> from step3 above],
    fs.azure.account.oauth2.client.secret=[<key> from step5 above]
   ```

## <a name="use-access-keys-to-mount"></a>使用访问密钥进行装载

你还可以使用访问密钥进行装载, 你可以在 Azure 门户上为你的 ADLS 帐户获取此访问密钥。

 > [!TIP]
   > 有关如何查找存储帐户的访问密钥 (`<storage-account-access-key>`) 的详细信息, 请参阅[查看帐户密钥和连接字符串](/azure/storage/common/storage-account-manage#view-account-keys-and-connection-string)。

### <a name="set-environment-variable-for-access-key-credentials"></a>设置访问密钥凭据的环境变量

1. 在可以访问大数据群集的客户端计算机上打开命令提示符。

1. 在可以访问大数据群集的客户端计算机上打开命令提示符。 使用以下格式设置环境变量。 请注意, 凭据需要位于以逗号分隔的列表中。 "Set" 命令在 Windows 上使用。 如果使用的是 Linux, 请改用 "export"。

   ```text
   set MOUNT_CREDENTIALS=fs.azure.abfs.account.name=<your-storage-account-name>.dfs.core.windows.net,
   fs.azure.account.key.<your-storage-account-name>.dfs.core.windows.net=<storage-account-access-key>
   ```

## <a id="mount"></a>装载远程 HDFS 存储

现在, 你已设置了访问密钥的 MOUNT_CREDENTIALS 环境变量或使用 OAuth, 接下来可以开始安装。 以下步骤将 Azure Data Lake 中的远程 HDFS 存储装载到大数据群集的本地 HDFS 存储中。

1. 使用**kubectl**在大数据群集中查找终结点**控制器-svc-外部**服务的 IP 地址。 查找**外部 IP**。

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

1. 使用群集用户名和密码通过控制器终结点的外部 IP 地址登录**azdata** :

   ```bash
   azdata login -e https://<IP-of-controller-svc-external>:30080/
   ```
1. 设置环境变量 MOUNT_CREDENTIALS (向上滚动获取说明)

1. 使用**azdata bdc 存储池装载创建**在 Azure 中装载远程 HDFS 存储。 运行以下命令之前, 请替换占位符值:

   ```bash
   azdata bdc storage-pool mount create --remote-uri abfs://<blob-container-name>@<storage-account-name>.dfs.core.windows.net/ --mount-path /mounts/<mount-name>
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
