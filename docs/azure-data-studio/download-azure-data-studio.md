---
title: 下载并安装 Azure Data Studio
description: 下载并安装适用于 Windows、macOS 或 Linux 的 Azure Data Studio
ms.prod: azure-data-studio
ms.technology: ''
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.reviewer: maghan
ms.custom: seodec18
ms.date: 7/17/2020
ms.openlocfilehash: 367711588e9a58358abff972a8f8637aefdf013a
ms.sourcegitcommit: 9470c4d1fc8d2d9d08525c4f811282999d765e6e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/17/2020
ms.locfileid: "86459029"
---
# <a name="download-and-install-azure-data-studio"></a>下载并安装 Azure Data Studio

Azure Data Studio 在 Windows、macOS 和 Linux 上运行。

下载并安装最新版本：

> [!NOTE]
> 如果是从 SQL Operations Studio 进行更新且希望保留设置、键盘快捷方式或代码片段，请参阅[移动用户设置](#move-user-settings)。

|平台|下载|发布日期| 版本 |
|:---|:---|:---|:---|
| Windows | [用户安装程序（推荐）](https://go.microsoft.com/fwlink/?linkid=2135512)<br>[系统安装程序](https://go.microsoft.com/fwlink/?linkid=2135513)<br>[.zip](https://go.microsoft.com/fwlink/?linkid=2135514) | 2020 年 7 月 17 日 | 1.20.1 |
| macOS | [.zip](https://go.microsoft.com/fwlink/?linkid=2135266) | 2020 年 7 月 17 日 | 1.20.1 |
| Linux | [.deb](https://go.microsoft.com/fwlink/?linkid=2135515)<br>[.rpm](https://go.microsoft.com/fwlink/?linkid=2135268)<br>[.tar.gz](https://go.microsoft.com/fwlink/?linkid=2135267) | 2020 年 7 月 17 日| 1.20.1 |

有关最新版本的详细信息，请参阅[发行说明](release-notes.md)。

## <a name="get-azure-data-studio-for-windows"></a>获取适用于 Windows 的 Azure Data Studio

此版本的 Azure Data Studio 包含标准 Windows Installer 体验和 .zip 文件。

建议使用用户安装程序，因为它不需要管理员权限，可简化安装和升级。 用户安装程序不需要管理员权限，因为它位于用户本地的 AppData (LOCALAPPDATA) 文件夹下。 用户安装程序还提供更流畅的后台更新体验。 有关详细信息，请参阅 [Windows 用户设置](https://code.visualstudio.com/updates/v1_26#_user-setup-for-windows)。

**用户安装程序**（推荐）

1. 下载并运行[适用于 Windows 的 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 用户安装程序](https://go.microsoft.com/fwlink/?linkid=2135512)。
2. 启动 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] 应用。

**系统安装程序**

1. 下载并运行[适用于 Windows 的 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 系统安装程序](https://go.microsoft.com/fwlink/?linkid=2135513)。
2. 启动 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] 应用。

**zip 文件**

1. 下载[适用于 Windows 的 [!INCLUDE[name-sos](../includes/name-sos-short.md)] .zip](https://go.microsoft.com/fwlink/?linkid=2135514)。
2. 浏览到下载文件并将其解压缩。
3. `\azuredatastudio-windows\azuredatastudio.exe`运行

## <a name="get-azure-data-studio-for-macos"></a>获取适用于 macOS 的 Azure Data Studio

1. 下载[适用于 macOS 的 [!INCLUDE[name-sos](../includes/name-sos-short.md)]](https://go.microsoft.com/fwlink/?linkid=2135266)。
2. 若要展开 zip 的内容，请双击。
3. 若要使 Azure Data Studio 在启动板中可用，请将 Azure Data Studio.app 拖到“Applications”文件夹中  。

## <a name="get-azure-data-studio-for-linux"></a>获取适用于 Linux 的 Azure Data Studio

1. 通过使用安装程序之一或 tar.gz 存档来下载适用于 Linux 的 [!INCLUDE[name-sos](../includes/name-sos-short.md)]：
    - [.deb](https://go.microsoft.com/fwlink/?linkid=2135515)
    - [.rpm](https://go.microsoft.com/fwlink/?linkid=2135268)
    - [.tar.gz](https://go.microsoft.com/fwlink/?linkid=2135267)
1. 若要提取文件并启动 [!INCLUDE[name-sos](../includes/name-sos-short.md)]，请打开一个新的终端窗口并键入以下命令：

   **Debian 安装：**

   ```bash
   cd ~
   sudo dpkg -i ./Downloads/azuredatastudio-linux-<version string>.deb

   azuredatastudio
   ```

   **rpm 安装：**

   ```bash
   cd ~
   yum install ./Downloads/azuredatastudio-linux-<version string>.rpm

   azuredatastudio
   ```

   **tar.gz 安装：**

   ```bash
   cd ~
   cp ~/Downloads/azuredatastudio-linux-<version string>.tar.gz ~ 
   tar -xvf ~/azuredatastudio-linux-<version string>.tar.gz 
   echo 'export PATH="$PATH:~/azuredatastudio-linux-x64"' >> ~/.bashrc
   source ~/.bashrc
   azuredatastudio
   ```

   > [!NOTE]
   > 在 Debian、Redhat 和 Ubuntu 上，可能缺少依赖项。 使用以下命令安装这些依赖项，具体取决于你的 Linux 版本：

   **Debian：**

   ```bash
   sudo apt-get install libunwind8
   ```

   **Redhat：**

   ```bash
   yum install libXScrnSaver
   ```

   **Ubuntu：**

   ```bash
   sudo apt-get install libxss1

   sudo apt-get install libgconf-2-4

   sudo apt-get install libunwind8
   ```

## <a name="download-insiders-build-of-azure-data-studio"></a>下载 Azure Data Studio 的预览体验内部版本

通常，用户应下载上述 Azure Data Studio 的稳定版本。 但是，如果用户希望试用 Beta 版功能并向我们提供反馈，可以下载 [Azure Data Studio 的预览体验内部版本。](https://github.com/microsoft/azuredatastudio#try-out-the-latest-insiders-build-from-main)

## <a name="uninstall-azure-data-studio"></a>卸载 Azure Data Studio

如果使用 Windows 安装程序安装了 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]，则卸载方式与删除任何 Windows 应用程序相同。

如果使用 .zip 或其他存档安装了 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]，则只需删除文件。

## <a name="supported-operating-systems"></a>受支持的操作系统

Azure Data Studio 在 Windows、macOS 和 Linux 上运行，并在以下平台上受支持：

### <a name="windows"></a>Windows

- Windows 10（64 位）
- Windows 8.1（64 位）
- Windows 8（64 位）
- Windows 7 (SP1)（64 位）- 需要 [KB2533623](https://www.microsoft.com/download/details.aspx?id=26767)
- Windows Server 2019
- Windows Server 2016
- Windows Server 2012 R2（64 位）
- Windows Server 2012（64 位）
- Windows Server 2008 R2（64 位）

### <a name="macos"></a>macOS

- macOS 10.15 Catalina
- macOS 10.14 Mojave
- macOS 10.13 High Sierra
- macOS 10.12 Sierra

### <a name="linux"></a>Linux

- Red Hat Enterprise Linux 7.4
- Red Hat Enterprise Linux 7.3
- SUSE Linux Enterprise Server v12 SP2
- Ubuntu 16.04

## <a name="recommended-system-requirements"></a>建议的系统要求

| 推荐/最低 | CPU 内核数 | 内存/RAM |
|---------------------|-----------|------------|
| 建议         |     4     |   8 GB     |
|   最小值           |     2     |   4 GB     |

## <a name="check-for-updates"></a>检查更新

若要检查最新更新，请单击窗口左下角的齿轮图标，然后单击“检查更新”

## <a name="supported-sql-offerings"></a>支持的 SQL 产品/服务

- 此版本的 Azure Data Studio 适用于所有[受支持的 SQL Server 2014 - [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 版本](https://support.microsoft.com/lifecycle?C2=1044)，并且支持与 Azure SQL 数据库和 Azure SQL 数据仓库中的最新云功能配合使用。 Azure Data Studio 还提供对 Azure SQL 托管实例的预览支持。

## <a name="upgrade-from-sql-operations-studio"></a>从 SQL Operations Studio 升级

如果用户仍在使用 SQL Operations Studio，则需要升级到 Azure Data Studio。 SQL Operations Studio 是 Azure Data Studio 的预览名称和预览版本。 2018 年 9 月，我们已[将该名称更改为 Azure Data Studio](https://cloudblogs.microsoft.com/sqlserver/2018/09/25/azure-data-studio-for-sql-server/) 并发布了正式 (GA) 版本。 由于不再更新或支持 SQL Operations Studio，因此我们要求所有 SQL Operations Studio 用户下载最新版本的 Azure Data Studio 以获取最新功能、安全更新以及修补程序。

从旧的预览版升级到最新 Azure Data Studio 时会丢失当前的设置和扩展。 若要迁移设置，请按照以下“移动用户设置”部分中的说明进行操作：

## <a name="move-user-settings"></a>移动用户设置

若要迁移自定义设置、键盘快捷方式或代码片段，请执行以下步骤。 若要从 SQL Operations Studio 版本升级到 Azure Data Studio，请务必执行此操作。

如果已经拥有 Azure Data Studio，或从未安装或自定义过 SQL Operations Studio，可忽略此部分。

1. 单击左下方的齿轮，然后单击“设置”，以打开设置。

   ![open-settings](./media/download/open-settings.png)

2. 右键单击顶部的“用户设置”选项卡，然后单击“在资源管理器中显示”

   ![reveal-in-explorer](./media/download/reveal-in-explorer.png)

3. 复制此文件夹中的所有文件，并将其保存在本地驱动器上易于查找的位置，例如文档文件夹。

   ![copy-settings](./media/download/copy-settings.png)

4. 在新版 Azure Data Studio 中，执行步骤 1-2，然后在步骤 3 中将保存的内容粘贴到文件夹。 也可以在其各自位置上手动复制设置、键绑定或代码片段。

5. 若要覆盖现有安装，请在安装之前删除旧安装目录，以避免连接到资源浏览器的 Azure 帐户时出错。

## <a name="next-steps"></a>后续步骤

请参阅以下快速入门以开始使用：

- [连接并查询 SQL Server](quickstart-sql-server.md)
- [连接并查询 Azure SQL 数据库](quickstart-sql-database.md)
- [连接并查询 Azure 数据仓库](quickstart-sql-dw.md)

[!INCLUDE[get-help-sql-tools](../includes/paragraph-content/get-help-sql-tools.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]

[Microsoft 隐私声明](https://go.microsoft.com/fwlink/?LinkId=521839)和[使用情况数据收集](usage-data-collection.md)。
