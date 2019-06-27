---
title: 从
titleSuffix: Azure Data Studio
description: 下载和为 Windows 安装 Azure 数据 Studio、 macOS 或 Linux
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
manager: jroth
ms.custom: seodec18
ms.date: 06/25/2019
ms.reviewer: alayu; sstein
ms.openlocfilehash: 3954e9dbe1159608cb0141e908ae65b7cde7fa81
ms.sourcegitcommit: 65ceea905030582f8d89e75e97758abf3b1f0bd6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2019
ms.locfileid: "67400115"
---
# <a name="download-and-install-azure-data-studio"></a>下载并安装 Azure Data Studio

[!INCLUDE[name-sos](../includes/name-sos.md)] 在 Windows、 macOS 和 Linux 上运行。


下载并安装最新版本中，*年 6 月发行*:

> [!NOTE]
> 如果要从 SQL Operations Studio 进行更新，并且希望保留设置、键盘快捷方式或代码片段，请参阅[移动用户设置](#move-user-settings)。

|平台|下载|发布日期| 版本 |
|:---|:---|:---|:---|
|Windows|[用户的安装程序 （推荐）](https://go.microsoft.com/fwlink/?linkid=2094100)<br>[系统安装程序](https://go.microsoft.com/fwlink/?linkid=2094200)<br>[.zip](https://go.microsoft.com/fwlink/?linkid=2094201)|2019 年 6 月 6日日 |1.8.0|
|macOS|[.zip](https://go.microsoft.com/fwlink/?linkid=2094202)|2019 年 6 月 6日日 |1.8.0|
|Linux|[.deb](https://go.microsoft.com/fwlink/?linkid=2094203)<br>[.rpm](https://go.microsoft.com/fwlink/?linkid=2094102)<br>[.tar.gz](https://go.microsoft.com/fwlink/?linkid=2094101)|2019 年 6 月 6日日 |1.8.0|

有关最新版本的详细信息，请参阅[发行说明](release-notes.md)。

## <a name="get-azure-data-studio-for-windows"></a>获取 Windows Azure Data Studio

此版本的[!INCLUDE[name-sos](../includes/name-sos-short.md)]包括标准 Windows 安装程序体验和一个.zip 文件。

*用户的安装程序*建议，因为它不需要管理员权限，这简化了安装和升级。 用户的安装程序不需要管理员权限，因为位置是在用户本地 AppData (LOCALAPPDATA) 文件夹下。 用户的安装程序还提供了更流畅的后台更新体验。 有关详细信息，请参阅[的 Windows 用户设置](https://code.visualstudio.com/updates/v1_26#_user-setup-for-windows)。


**用户的安装程序**（推荐）

1. 下载并运行[ [!INCLUDE[name-sos](../includes/name-sos-short.md)] *用户*适用于 Windows 安装程序](https://go.microsoft.com/fwlink/?linkid=2094100)。
2. 启动[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]应用。

**系统安装程序**

1. 下载并运行[ [!INCLUDE[name-sos](../includes/name-sos-short.md)] *系统*适用于 Windows 安装程序](https://go.microsoft.com/fwlink/?linkid=2094200)。
2. 启动[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]应用。


**zip 文件**

1. 下载[ [!INCLUDE[name-sos](../includes/name-sos-short.md)] Windows 的.zip](https://go.microsoft.com/fwlink/?linkid=2094201)。
2. 浏览到下载的文件并将其解压缩。
3. 运行 `\azuredatastudio-windows\azuredatastudio.exe`


## <a name="get-azure-data-studio-for-macos"></a>获取适用于 macOS 的 Azure Data Studio

1. 下载适用于 macOS 的 [[!INCLUDE[name-sos](../includes/name-sos-short.md)]](https://go.microsoft.com/fwlink/?linkid=2094202)。
2. 若要展开 zip 的内容，请双击它。
3. 若要使[!INCLUDE[name-sos](../includes/name-sos-short.md)]推出*快速启动板*，拖动*Azure 数据 Studio.app*到*应用程序*文件夹。


## <a name="get-azure-data-studio-for-linux"></a>获取适用于 Linux 的 Azure Data Studio

1. 使用其中一个安装程序或 tar.gz 存档下载适用于 Linux 的 [!INCLUDE[name-sos](../includes/name-sos-short.md)]：
    - [.deb](https://go.microsoft.com/fwlink/?linkid=2094203)
    - [.rpm](https://go.microsoft.com/fwlink/?linkid=2094102)
    - [.tar.gz](https://go.microsoft.com/fwlink/?linkid=2094101)
1. 若要解压缩文件并启动 [!INCLUDE[name-sos](../includes/name-sos-short.md)]，请打开新的终端窗口并键入以下命令：

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
## <a name="download-insiders-build-of-azure-data-studio"></a>下载 Azure Data Studio 的预览体验成员的版本
一般情况下，用户应下载 Azure Data Studio 更高版本的稳定的版本。 但是，如果你想要试用我们的 beta 功能并向我们提供反馈，您可以下载[预览体验成员版本的 Azure Data Studio。](https://github.com/microsoft/azuredatastudio#try-out-the-latest-insiders-build-from-master)

## <a name="uninstall-azure-data-studio"></a>卸载 Azure Data Studio

如果你使用 Windows 安装程序安装了 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]，则卸载方法与移除任何 Windows 应用程序的方法相同。

如果你使用 .zip 或其他存档安装了 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]，则只需删除这些文件。

## <a name="supported-operating-systems"></a>支持的操作系统

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 在 Windows、macOS 和 Linux 上运行，并在以下平台上受支持：

### <a name="windows"></a>Windows
- Windows 10（64 位）
- Windows 8.1（64 位）
- Windows 8（64 位）
- Windows 7 (SP1) （64 位）-需要[KB2533623](https://www.microsoft.com/download/details.aspx?id=26767)
- Windows Server 2016
- Windows Server 2012 R2（64 位）
- Windows Server 2012（64 位）
- Windows Server 2008 R2（64 位）

### <a name="macos"></a>macOS
- macOS 10.13 High Sierra
- macOS 10.12 Sierra

### <a name="linux"></a>Linux
- Red Hat Enterprise Linux 7.4
- Red Hat Enterprise Linux 7.3
- SUSE Linux Enterprise Server v12 SP2
- Ubuntu 16.04

## <a name="recommended-system-requirements"></a>建议的系统要求
为获得最佳体验，请使用建议的系统要求。
[需要此处更新来量化内存]

|             | CPU 核心数 | 内存/RAM |
|:-----------|:---------|:----------|
| 建议 |     4     |      8 GB    |
|   最低要求   |     2     |      4 GB     |
|             |           |            |

## <a name="check-for-updates"></a>检查更新
要检查最新更新，请单击窗口左下角的齿轮图标，然后单击**检查更新**

## <a name="supported-sql-offerings"></a>支持的 SQL 产品/服务

* 此版本的 Azure Data Studio [适用于所有受支持版本的 SQL Server 2014 - [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]](https://support.microsoft.com/lifecycle?C2=1044)，同时支持与 Azure SQL 数据库和 Azure SQL 数据仓库中的最新云功能配合使用。 Azure Data Studio 还为 Azure SQL 托管实例提供预览支持。

## <a name="upgrade-from-sql-operations-studio"></a>从 SQL Operations Studio 升级

如果您仍在使用 SQL Operations Studio，你需要升级到 Azure Data Studio。 SQL Operations Studio 时的预览名称和 Azure Data Studio 的预览版本。 在 2018 年 9 月，我们[该名称更改为 Azure Data Studio](https://cloudblogs.microsoft.com/sqlserver/2018/09/25/azure-data-studio-for-sql-server/)和发布正式版 (GA) 版本。 因为 SQL Operations Studio 将不再更新或受支持，我们要求所有 SQL Operations Studio 用户若要下载最新版本的 Azure Data Studio，以获取最新功能，安全更新和修补程序。
 
从旧的预览版升级到最新的 Azure Data Studio，将会丢失您的当前设置和扩展。 若要移动你的设置，请遵循以下*移动用户设置*部分：


## <a name="move-user-settings"></a>移动用户设置

如果想要移动自定义设置、键盘快捷方式或代码片段，请执行以下步骤。 如果要从 SQL Operations Studio 版本升级到 Azure Data Studio，执行这些步骤非常重要。

*如果已有 Azure Data Studio，或者从未安装或自定义 SQL Operations Studio，则可以忽略此部分。*


1. 打开**设置**：单击左下方的齿轮并单击**设置**。

   ![打开设置](./media/download/open-settings.png)

2. 右键单击顶部的**用户设置**选项卡，然后单击**在资源管理器中展现**

   ![reveal-in-explorer](./media/download/reveal-in-explorer.png)

3. 复制此文件夹中的所有文件并保存在本地驱动器上易于查找的位置，例如 Documents 文件夹。

   ![复制设置](./media/download/copy-settings.png)

4. 在新版 Azure Data Studio 中，请执行步骤 1-2，然后在步骤 3 中将保存的内容粘贴到文件夹中。 还可以手动从各自的位置复制设置、键绑定或代码片段。

5. 如果要覆盖现有安装，请在安装前删除旧安装目录，以避免在资源浏览器连接到 Azure 帐户时出错。

## <a name="next-steps"></a>后续步骤

请参阅以下快速入门之一以便开始使用：
- [连接并查询 SQL Server](quickstart-sql-server.md)
- [连接并查询 Azure SQL 数据库](quickstart-sql-database.md)
- [连接并查询 Azure 数据仓库](quickstart-sql-dw.md)

[!INCLUDE[get-help-sql-tools](../includes/paragraph-content/get-help-sql-tools.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]

[Microsoft 隐私声明](https://go.microsoft.com/fwlink/?LinkId=521839)并[使用情况数据收集](usage-data-collection.md)。