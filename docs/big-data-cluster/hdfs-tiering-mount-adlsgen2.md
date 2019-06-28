---
title: 为 HDFS 分层装入 ADLS Gen2
titleSuffix: How to mount ADLS Gen2
description: 本文介绍如何配置 HDFS 的分层，从而在 SQL Server 2019 大数据群集 （预览版） 上装载到 HDFS 的外部的 Azure Data Lake 存储文件系统。
author: nelgson
ms.author: negust
ms.reviewer: jroth
manager: jroth
ms.date: 06/27/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 1d06b668a6c8badef75a0e90d3f58b67b1269984
ms.sourcegitcommit: ab867100949e932f29d25a3c41171f01156e923d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2019
ms.locfileid: "67419049"
---
# <a name="how-to-mount-adls-gen2-for-hdfs-tiering-in-a-big-data-cluster"></a>如何装载 ADLS hdfs 分层大数据群集中的第 2 代

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

## <a name="credentials-for-mounting"></a>用于装载的凭据

## <a name="use-oauth-credentials-to-mount"></a>使用 OAuth 凭据装载

若要使用的 OAuth 凭据装载，需要按照以下步骤：

1. 转到[Azure 门户](https://portal.azure.com)
1. 请转到左侧的导航窗格中，"服务"和"Azure Active Directory"上的时钟
1. 使用"应用注册"菜单中，创建"Web 应用程序并按照向导。 **请记住在此处创建的名称**。 您需要将此名称添加到 ADLS 帐户的授权用户。
1. 创建 web 应用程序后，请转到"密钥"下的"设置"应用程序。
1. 选择密钥的持续时间并单击保存。 **保存生成的密钥。**
1.  返回到应用注册页中，并单击顶部的"终结点"按钮。 **记下的"令牌终结点"URL**
1. 现在应具有的 OAuth 记下以下操作：

    - "应用程序 ID"的 Web 应用在上面步骤 3 中创建
    - 在步骤 5 中生成的密钥
    - 步骤 6 中令牌终结点

### <a name="adding-the-service-principal-to-your-adls-account"></a>将服务主体添加到在 ADLS 帐户

1. 同样，转到门户并打开在 ADLS 帐户并在左侧菜单中选择访问控制 (IAM)。
1. 选择"添加角色分配"，然后搜索你在步骤 3 中创建以上 （请注意，它未显示在列表中，但将找到是否你搜索的完整名称） 的名称。
1. 现在，添加"存储 Blob 数据参与者 （预览）"角色。

等待 5-10 分钟，然后使用装载的凭据

### <a name="set-environment-variable-for-oauth-credentials"></a>设置环境变量中的 OAuth 凭据

打开命令提示符可以访问你的大数据群集的客户端计算机上。 设置环境变量使用以下格式：请注意，凭据必须位于一个逗号分隔列表。 在 Windows 上使用 set 命令。 如果使用的 Linux，则改为使用导出。

   ```text
    set MOUNT_CREDENTIALS=fs.azure.account.auth.type=OAuth,
    fs.azure.account.oauth.provider.type=org.apache.hadoop.fs.azurebfs.oauth2.ClientCredsTokenProvider,
    fs.azure.account.oauth2.client.endpoint=[token endpoint from step6 above],
    fs.azure.account.oauth2.client.id=[<Application ID> from step3 above],
    fs.azure.account.oauth2.client.secret=[<key> from step5 above]
   ```

## <a name="use-access-keys-to-mount"></a>使用访问键来装载

此外可以装载使用可以获取有关在 Azure 门户上在 ADLS 帐户访问密钥。

 > [!TIP]
   > 有关如何查找访问密钥的详细信息 (`<storage-account-access-key>`) 你的存储帐户，请参阅[查看帐户密钥和连接字符串](/azure/storage/common/storage-account-manage#view-account-keys-and-connection-string)。

### <a name="set-environment-variable-for-access-key-credentials"></a>设置环境变量中的访问密钥凭据

1. 打开命令提示符可以访问你的大数据群集的客户端计算机上。

1. 打开命令提示符可以访问你的大数据群集的客户端计算机上。 使用以下格式的环境变量设置。 请注意，凭据必须位于一个逗号分隔列表。 在 Windows 上使用 set 命令。 如果使用的 Linux，则改为使用导出。

   ```text
   set MOUNT_CREDENTIALS=fs.azure.abfs.account.name=<your-storage-account-name>.dfs.core.windows.net,
   fs.azure.account.key.<your-storage-account-name>.dfs.core.windows.net=<storage-account-access-key>
   ```

## <a id="mount"></a> 将远程 HDFS 存储装载

既然已设置为访问密钥或使用 OAuth MOUNT_CREDENTIALS 环境变量，可以开始安装。 以下步骤将 Azure Data Lake 中到本地 HDFS 存储大数据群集的远程 HDFS 存储装载。

1. 使用**kubectl**若要查找的终结点的 IP 地址**控制器 svc 外部**大数据群集中的服务。 寻找**外部 IP**。

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

1. 登录方式**mssqlctl**控制器终结点的外部 IP 地址使用你的群集用户名和密码：

   ```bash
   mssqlctl login -e https://<IP-of-controller-svc-external>:30080/
   ```
1. 设置环境变量 MOUNT_CREDENTIALS （滚动进行说明）

1. 将在 Azure 中使用远程 HDFS 存储装载**mssqlctl bdc 存储池装入创建**。 将占位符值替换为之前运行以下命令：

   ```bash
   mssqlctl bdc storage-pool mount create --remote-uri abfs://<blob-container-name>@<storage-account-name>.dfs.core.windows.net/ --mount-path /mounts/<mount-name>
   ```

   > [!NOTE]
   > 装载创建命令是异步的。 在此期间，没有任何消息，指示是否已成功装载。 请参阅[状态](#status)部分，以检查你装载的状态。

如果安装成功，您应该能够查询 HDFS 数据并对其运行 Spark 作业。 它将出现在指定的位置中的大数据群集的 HDFS `--mount-path`。

## <a id="status"></a> 获取装载的状态

若要列出的大数据群集中的所有装载状态，请使用以下命令：

```bash
mssqlctl bdc storage-pool mount status
```

若要列出的在 HDFS 中的特定路径装载状态，请使用以下命令：

```bash
mssqlctl bdc storage-pool mount status --mount-path <mount-path-in-hdfs>
```

## <a id="delete"></a> 删除装载

若要删除装载，请使用**mssqlctl bdc 存储池装入删除**命令，并在 HDFS 中指定的装载路径：

```bash
mssqlctl bdc storage-pool mount delete --mount-path <mount-path-in-hdfs>
```

## <a name="next-steps"></a>后续步骤

有关 SQL Server 2019 大数据群集的详细信息，请参阅[什么是 SQL Server 2019 大数据群集？](big-data-cluster-overview.md)。
