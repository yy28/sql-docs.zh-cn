---
title: "设置 Linux SQL Server 在 Azure 中 VM |Microsoft 文档"
description: "本教程演示如何在 Azure 中创建 SQL Server 自 2017 年 Linux 虚拟机。"
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 07/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 222e23b2-51e7-429b-b8e5-61e0ebe7df9b
ms.translationtype: MT
ms.sourcegitcommit: ea75391663eb4d509c10fb785fcf321558ff0b6e
ms.openlocfilehash: 0470622b0fe5a8835213617a4fc2e8c74f674873
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="create-a-linux-sql-server-2017-virtual-machine-with-the-azure-portal"></a>使用 Azure 端口创建 Linux SQL Server 2017 虚拟机

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Azure 提供了已安装的 SQL Server 自 2017 年 1 RC2 的 Linux 虚拟机映像。 本主题提供关于如何使用 Azure 端口创建 Linux SQL Server 虚拟机的简短演练。 

## <a name="create-a-linux-vm-with-sql-server-installed"></a>在安装了 SQL Server 的情况下创建 Linux VM

打开[Azure 门户](https://portal.azure.com/)。

1. 单击**新建**左侧。

1. 在**新建**边栏选项卡，单击**计算**。

1. 单击**所有请参阅**旁边**特色应用**标题。

   ![请参阅所有 VM 映像](./media/sql-server-linux-azure-virtual-machine/azure-compute-blade.png)

1. 在搜索框中，键入**SQL Server 2017**，按**Enter**开始搜索。

    ![SQL Server 自 2017 年 VM 映像的搜索筛选器](./media/sql-server-linux-azure-virtual-machine/searchfilter.png)

    > [!TIP]
    > 此筛选器显示 SQL Server 2017 可用的 Linux 虚拟机映像。 随着时间推移，将会列出适用于支持的其他 Linux 分发版的 SQL Server 2017 映像。 你还可以单击此[链接](https://ms.portal.azure.com/#blade/Microsoft_Azure_Marketplace/GalleryFeaturedMenuItemBlade/selectedMenuItemId/home/searchQuery/sql%20server%202017)直接转到搜索结果的 SQL Server 自 2017 年。 

1. 从搜索结果中选择一个 SQL Server 2017 映像。

1. 单击 **“创建”**。

1. 上**基础知识**边栏选项卡，填写你的 Linux VM 的详细信息。 

    ![基础知识边栏选项卡](./media/sql-server-linux-azure-virtual-machine/basics.png)

    > [!Note]
    > 可以选择使用 SSH 公钥或密码进行身份验证。 SSH 更安全。 有关如何生成 SSH 密钥的说明，请参阅[创建 SSH 密钥在 Linux 和 Mac 上 Azure 中的 Linux Vm 的](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-mac-create-ssh-keys)。 

1. 单击 **“确定”**。

1. 上**大小**边栏选项卡，选择机大小。 有关开发和功能测试，我们建议的 VM 大小为**DS2**或更高版本。 对于性能测试，使用**DS13**或更高版本。

    ![选择 VM 大小](./media/sql-server-linux-azure-virtual-machine/vmsizes.png)

    若要查看其他大小，选择**查看所有**。 有关 VM 机大小的详细信息，请参阅[Linux VM 大小](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes)。

1. 然后单击“选择”。

1. 上**设置**边栏选项卡，你可以对设置进行更改或保留默认设置。

1. 单击 **“确定”**。

1. 上**摘要**页上，单击**确定**以创建 VM。

> [!NOTE]
> Azure VM 将防火墙预配置为打开 SQL Server 端口 1433，用于远程连接。 但若要远程连接，还需添加下一节所述的网络安全组规则。

## <a id="remote"></a>为远程连接配置

要在 Azure VM 上远程连接至 SQL Server，必须对网络安全组配置入站规则。 该规则允许 SQL Server 侦听的端口（默认为 1433）上的流量。 下列步骤演示了如何使用 Azure 端口完成这一步。 

1. 在门户中，选择**虚拟机**，然后选择 SQL Server VM。

1. 在属性列表中，选择**网络接口**。

1. 然后选择 VM 的网络接口。

    ![网络接口](./media/sql-server-linux-azure-virtual-machine/networkinterfaces.png)

1. 单击网络安全组链接。

    ![网络安全组](./media/sql-server-linux-azure-virtual-machine/networksecuritygroup.png)

1. 网络安全组，选择的属性中**入站安全规则**。

1. 单击**+ 添加**按钮。

1. 输入“SQLServerRemoteConnections”作为名称。

1. 在**服务**列表中，选择**MS SQL**。

    ![MS SQL 安全组规则](./media/sql-server-linux-azure-virtual-machine/sqlnsgrule.png)

1. 单击**确定**保存为你的 VM 的规则。

## <a id="connect"></a>连接到 Linux VM

如果你已经使用 BASH shell，连接到 Azure VM 使用**ssh**命令。 在下列命令中，替换 VM 用户名和 IP 地址，连接到 Linux VM。

```bash
ssh -l AzureAdmin 100.55.555.555
```

可以在 Azure 门户中查找 VM 的 IP 地址。

![在 Azure 门户中的 IP 地址](./media/sql-server-linux-azure-virtual-machine/vmproperties.png)

如果在 Windows 上运行且缺少 Bash Shell，那么可以安装 SSH 客户端，如 PuTTY。

1. [下载并安装 PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)。

1. 运行 PuTTY。

1. 在 PuTTY 配置屏幕中输入 VM 的公用 IP 地址。

1. 单击“打开”，按提示输入用户名和密码。

有关连接到 Linux Vm 的详细信息，请参阅[使用门户在 Azure 上创建 Linux VM](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-quick-create-portal#ssh-to-the-vm)。

## <a name="configure-sql-server"></a>配置 SQL Server

1. 连接至 Linux VM 后，打开一个新的命令终端。

1. 使用下列命令设置 SQL Server。

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup 
   ```

   接受许可条款，输入系统管理员帐户的密码。 可在出现系统提示时启动服务器。

1. （可选）[安装 SQL Server 工具](sql-server-linux-setup-tools.md)。

## <a name="next-steps"></a>后续步骤

既然你已在 Azure 中的 SQL Server 2017 虚拟机，你可以本地使用连接**sqlcmd**运行 TRANSACT-SQL 查询。

如果已为远程 SQL Server 连接配置了 Azure VM，则应该能够进行远程连接。 有关从远程 Windows 计算机连接到 Linux 上的 SQL Server 的示例，请参阅[使用 SSMS 连接到 Linux 上的 SQL Server 的 Windows 上](sql-server-linux-develop-use-ssms.md)。

有关在 Azure 中的 Linux 虚拟机的更多常规信息，请参阅[Linux 虚拟机文档](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/)。

