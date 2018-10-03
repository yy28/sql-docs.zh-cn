---
title: 下载并安装 Azure Data Studio |Microsoft Docs
description: 下载和为 Windows 安装 Azure 数据 Studio、 macOS 或 Linux
ms.custom: tools|sos
ms.date: 09/24/2018
ms.prod: sql
ms.reviewer: alayu; sstein
ms.prod_service: sql-tools
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 88b79feb3b04dcc7f872653b2e24a9f70c370f57
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "48037976"
---
# <a name="download-and-install-azure-data-studio"></a>下载并安装 Azure Data Studio

[!INCLUDE[name-sos](../includes/name-sos.md)] 在 Windows、 macOS 和 Linux 上运行。

下载并安装最新版本中，*年 9 月 GA 版本*:

> [!NOTE]
> 如果正在从 SQL Operations Studio 更新，并且想要保留您的设置、 键盘快捷方式或代码片段，请参阅[移动用户设置](#move-user-settings)。

|平台|下载|发布日期| 版本 |
|:---|:---|:---|:---|
|Windows|[安装程序](https://go.microsoft.com/fwlink/?linkid=2024683)<br>[.zip](https://go.microsoft.com/fwlink/?linkid=2024680)|2018 年 9 月 24日日 |1.0|
|macOS|[.zip](https://go.microsoft.com/fwlink/?linkid=2024677)|2018 年 9 月 24日日 |1.0|
|Linux|[.deb](https://go.microsoft.com/fwlink/?linkid=2024668)<br>[.rpm](https://go.microsoft.com/fwlink/?linkid=2024672)<br>[.tar.gz](https://go.microsoft.com/fwlink/?linkid=2024675)|2018 年 9 月 24日日 |1.0|

有关最新版本的详细信息，请参阅[发行说明](release-notes.md)。

## <a name="get-azure-data-studio-for-windows"></a>获取 Windows Azure 数据 Studio

此版本的[!INCLUDE[name-sos](../includes/name-sos-short.md)]包括标准 Windows 安装程序体验和.zip 格式： 

**安装程序**

1. 下载并运行[[!INCLUDE[name-sos](../includes/name-sos-short.md)]适用于 Windows 安装程序](https://go.microsoft.com/fwlink/?linkid=2024683)。
1. 启动[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]应用。


**.zip 文件**

1. 下载[ [!INCLUDE[name-sos](../includes/name-sos-short.md)] Windows 的.zip](https://go.microsoft.com/fwlink/?linkid=2024680)。
2. 浏览到下载的文件并将其解压缩。
3. 运行 `\azuredatastudio-windows\azuredatastudio.exe`


## <a name="get-azure-data-studio-for-macos"></a>获取适用于 macOS 的 Azure Data Studio

1. 下载[[!INCLUDE[name-sos](../includes/name-sos-short.md)]适用于 macOS](https://go.microsoft.com/fwlink/?linkid=2024677)。
2. 若要展开的 zip 的内容，请双击它。
3. 若要使[!INCLUDE[name-sos](../includes/name-sos-short.md)]推出*快速启动板*，拖动*Azure 数据 Studio.app*到*应用程序*文件夹。


## <a name="get-azure-data-studio-for-linux"></a>获取适用于 Linux 的 Azure 数据 Studio

1. 下载[!INCLUDE[name-sos](../includes/name-sos-short.md)]通过使用其中一个安装程序或 tar.gz 存档适用于 Linux:
    - [.deb](https://go.microsoft.com/fwlink/?linkid=2024668)
    - [.rpm](https://go.microsoft.com/fwlink/?linkid=2024672)
    - [.tar.gz](https://go.microsoft.com/fwlink/?linkid=2024675)
1. 若要解压缩文件，并启动[!INCLUDE[name-sos](../includes/name-sos-short.md)]，打开新的终端窗口并键入以下命令：

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
   > 在 Debian、 Redhat 和 Ubuntu 上，您可能缺少依赖项。 使用以下命令安装这些依赖项，具体取决于你的 Linux 版本：
   

   **Debian:** 
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


## <a name="uninstall-azure-data-studio"></a>卸载 Azure 数据 Studio

如果您安装了[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]使用 Windows 安装程序，然后卸载相同的方式删除任何 Windows 应用程序。

如果您安装了[!INCLUDE[name-sos-short](../includes/name-sos-short.md)].zip 或其他存档，然后只需删除的文件。

## <a name="supported-operating-systems"></a>支持的操作系统

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 支持以下平台上和在 Windows、 macOS 和 Linux 上运行：

### <a name="windows"></a>Windows
- Windows 10（64 位）
- Windows 8.1（64 位）
- Windows 8（64 位）
- Windows 7 (SP1) （64 位）-需要[KB2533623](https://www.microsoft.com/en-us/download/details.aspx?id=26767)
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

## <a name="check-for-updates"></a>检查更新
若要检查最新的更新，请单击的窗口，然后单击左下角的齿轮图标**检查更新**

## <a name="move-user-settings"></a>移动用户设置

如果你想要移动自定义设置、 键盘快捷方式或代码段，请按照以下步骤。 这是重要的当从 SQL Operations Studio 版本升级到 Azure Data Studio 执行的操作。

*如果已有 Azure Data Studio，或你永远不会安装或自定义 SQL Operations Studio，则可以忽略此部分。*


1. 通过单击左下角的齿轮，然后单击打开设置**设置。**

   ![打开设置](./media/download/open-settings.png)

2. 右键单击**用户设置**选项卡顶部，单击**在资源管理器中展现**

   ![显示在浏览器](./media/download/reveal-in-explorer.png)

3. 在此文件夹中复制的所有文件并保存在易于查找相似文档文件夹的本地驱动器上的位置。

   ![复制设置](./media/download/copy-settings.png)

4. 在 Azure Data Studio 的新版本，请按照的步骤 1-2，然后为第 3 步将保存的内容粘贴到文件夹。 您可手动将复制设置、 键绑定或在其各自的位置中的代码段。


## <a name="next-steps"></a>后续步骤

请参阅以下快速入门中，若要开始之一：
- [连接并查询 SQL Server](quickstart-sql-server.md)
- [连接并查询 Azure SQL 数据库](quickstart-sql-database.md)
- [连接并查询 Azure 数据仓库](quickstart-sql-dw.md)

参与[!INCLUDE[name-sos](../includes/name-sos-short.md)]:
- [https://github.com/Microsoft/azuredatastudio](https://github.com/Microsoft/azuredatastudio) 

[Microsoft 隐私声明](https://go.microsoft.com/fwlink/?LinkId=521839)并[使用情况数据收集](usage-data-collection.md)。
