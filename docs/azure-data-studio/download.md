---
title: 下载并安装 Azure Data Studio |Microsoft Docs
description: 下载和为 Windows 安装 Azure 数据 Studio、 macOS 或 Linux
ms.custom: tools|sos
ms.date: 11/06/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f177b7756a1afc7d28f4f3bd85ac46c1f7563cbe
ms.sourcegitcommit: 6c9d35d03c1c349bc82b9ed0878041d976b703c6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/06/2018
ms.locfileid: "51217805"
---
# <a name="download-and-install-azure-data-studio"></a>下载并安装 Azure Data Studio

[!INCLUDE[name-sos](../includes/name-sos.md)]可在Windows，macOS和Linux上运行。

下载并安装最新版本中，*年 11 月发布*:

> [!NOTE]
> 如果要从SQL Operations Studio进行更新并希望保留设置，键盘快捷键或代码段，请参阅[移动用户设置](#move-user-settings)。

|平台|下载|发布日期| 版本 |
|:---|:---|:---|:---|
|Windows|[安装程序](https://go.microsoft.com/fwlink/?linkid=2038320)<br>[.zip](https://go.microsoft.com/fwlink/?linkid=2038323)|2018 年 11 月 6日日 |1.2.4|
|macOS|[.zip](https://go.microsoft.com/fwlink/?linkid=2038327)|2018 年 11 月 6日日 |1.2.4|
|Linux|[.deb](https://go.microsoft.com/fwlink/?linkid=2038405)<br>[.rpm](https://go.microsoft.com/fwlink/?linkid=2038401)<br>[.tar.gz](https://go.microsoft.com/fwlink/?linkid=2038332)|2018 年 11 月 6日日 |1.2.4|

有关最新版本的详细信息，请参阅[发行说明](release-notes.md)。

## <a name="get-azure-data-studio-for-windows"></a>获取 Windows Azure Data Studio

此版本的[!INCLUDE[name-sos](../includes/name-sos-short.md)]包含一个标准的Windows安装程序体验和一个.zip： 

**安装程序**

1. 下载并运行[[!INCLUDE[name-sos](../includes/name-sos-short.md)]适用于 Windows 的安装程序](https://go.microsoft.com/fwlink/?linkid=2038320)。
1. 启动[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]应用。


**zip 文件**

1. 下载[ [!INCLUDE[name-sos](../includes/name-sos-short.md)] Windows 的.zip](https://go.microsoft.com/fwlink/?linkid=2038323)。
2. 浏览到下载的文件并将其解压缩。
3. 运行 `\azuredatastudio-windows\azuredatastudio.exe`


## <a name="get-azure-data-studio-for-macos"></a>获取适用于 macOS 的 Azure Data Studio

1. 下载适用于 macOS的[[!INCLUDE[name-sos](../includes/name-sos-short.md)]](https://go.microsoft.com/fwlink/?linkid=2038327)。
2. 若要展开 zip 的内容，请双击它。
3. 若要使[!INCLUDE[name-sos](../includes/name-sos-short.md)]推出*快速启动板*，拖动*Azure 数据 Studio.app*到*应用程序*文件夹。


## <a name="get-azure-data-studio-for-linux"></a>获取适用于 Linux 的 Azure Data Studio

1. 使用其中一个安装程序或tar.gz存档下载[!INCLUDE[name-sos](../includes/name-sos-short.md)] for Linux：
    - [.deb](https://go.microsoft.com/fwlink/?linkid=2038405)
    - [.rpm](https://go.microsoft.com/fwlink/?linkid=2038401)
    - [.tar.gz](https://go.microsoft.com/fwlink/?linkid=2038332)
1. 若要解压缩文件，并启动[!INCLUDE[name-sos](../includes/name-sos-short.md)]，请打开一个新的终端窗口并键入以下命令：

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


## <a name="uninstall-azure-data-studio"></a>卸载 Azure Data Studio


如果您使用Windows安装程序安装了[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]，则以与删除任何Windows应用程序相同的方式卸载。

如果您使用.zip或其他存档安装了[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]，则只需删除这些文件即可。

## <a name="supported-operating-systems"></a>支持的操作系统

[!INCLUDE[name-sos](../includes/name-sos-short.md)]在Windows，macOS和Linux上运行，并支持在以下平台上运行：

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

## <a name="recommended-system-requirements"></a>建议的系统要求
为获得最佳体验，请使用建议的系统要求。

|             | CPU 核心数 | 内存/RAM |
|:-----------:|:---------:|:----------:|
| 建议 |     4     |      8     |
|   最低要求   |     2     |      4     |
|             |           |            |

## <a name="check-for-updates"></a>检查更新
要检查最新更新，请单击窗口左下角的齿轮图标，然后单击**检查更新**

## <a name="supported-sql-offerings"></a>支持的 SQL 产品/服务

* 此版本的Azure Data Studio适用于所有受支持的SQL Server 2014版本 -  [!INCLUDE [sql-server-2019预览版](..\includes\sssqlv15-md.md)]](https://support.microsoft.com/lifecycle?C2=1044)，并支持使用Azure SQL数据库和Azure SQL数据仓库中的最新云功能。 Azure Data Studio还为Azure SQL托管实例提供预览支持。

## <a name="move-user-settings"></a>移动用户设置

如果你想要移动自定义设置、 键盘快捷方式或代码段，请按照以下步骤。如果要从SQL Operations Studio版本升级到Azure Data Studio，这一点很重要。

*如果您已有Azure Data Studio，或者您从未安装或自定义SQL Operations Studio，则可以忽略此部分。*


1. 通单击左下方的齿轮并单击“设置”，打开**设置。**。 

   ![打开设置](./media/download/open-settings.png)

2. 右键单击顶部的**用户设置**选项卡，然后单击**在资源管理器中展现**

   ![显示在浏览器](./media/download/reveal-in-explorer.png)

3. 复制此文件夹中的所有文件并保存在本地驱动器上易于查找的位置，例如Documents文件夹。 

   ![复制设置](./media/download/copy-settings.png)

4. 在新版本的Azure Data Studio中，按照步骤1-2，然后在步骤3中将保存的内容粘贴到文件夹中。您还可以手动复制各自位置的设置，键绑定或片段。

5. 如果覆盖现有安装，请在安装之前删除旧安装目录，以避免连接到资源浏览器的Azure帐户时出错。

## <a name="next-steps"></a>后续步骤

请参阅以下快速入门之一以便开始使用：
- [连接并查询 SQL Server](quickstart-sql-server.md)
- [连接并查询 Azure SQL 数据库](quickstart-sql-database.md)
- [连接并查询 Azure 数据仓库](quickstart-sql-dw.md)

参与[!INCLUDE[name-sos](../includes/name-sos-short.md)]:
- [https://github.com/Microsoft/azuredatastudio](https://github.com/Microsoft/azuredatastudio) 

[Microsoft 隐私声明](https://go.microsoft.com/fwlink/?LinkId=521839)并[使用情况数据收集](usage-data-collection.md)。
