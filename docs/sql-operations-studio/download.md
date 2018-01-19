---
title: "下载并安装 Microsoft SQL 操作 Studio （预览版） |Microsoft 文档"
description: "下载和安装 Microsoft SQL 操作 Studio （预览版） for Windows、 macOS 或 Linux"
ms.custom: tools|sos
ms.date: 01/17/2018
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: 
ms.topic: article
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e8828b5f94c5500aa7ef3bffd48556e599e41124
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2018
---
# <a name="download-and-install-sql-operations-studio-preview"></a>下载并安装 SQL 操作 Studio （预览版）

[!INCLUDE[name-sos](../includes/name-sos.md)]在 Windows、 macOS 和 Linux 上运行。

下载并安装最新版本中，*年 1 月公共预览版*:

|平台|下载|发布日期|
|:---|:---|:---|
|Windows|[安装程序](https://go.microsoft.com/fwlink/?linkid=866480)<br>[.zip](https://go.microsoft.com/fwlink/?linkid=866479)|2018 年 1 月 17 日 |
|macOS|[.zip](https://go.microsoft.com/fwlink/?linkid=866481)|2018 年 1 月 17 日 |
|Linux|[.deb](https://go.microsoft.com/fwlink/?linkid=866484)<br>[.rpm](https://go.microsoft.com/fwlink/?linkid=866483)<br>[.tar.gz](https://go.microsoft.com/fwlink/?linkid=866482)|2018 年 1 月 17 日|

有关最新版本的详细信息，请参阅[发行说明](release-notes.md)。

## <a name="get-sql-operations-studio-preview-for-windows"></a>获取 Windows SQL 操作 Studio （预览版）

此版本的[!INCLUDE[name-sos](../includes/name-sos-short.md)]包括标准的 Windows 安装程序体验和.zip: 

**安装程序**

1. 下载并运行[[!INCLUDE[name-sos](../includes/name-sos-short.md)]面向 Windows 安装程序](https://go.microsoft.com/fwlink/?linkid=866480)。
1. 启动[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]应用。


**.zip 文件**

1. 下载[[!INCLUDE[name-sos](../includes/name-sos-short.md)]适用于 Windows 的.zip](https://go.microsoft.com/fwlink/?linkid=866479)。
2. 浏览到下载的文件并将它解压缩。
3. 运行 `\sqlops-windows\sqlops.exe`


## <a name="get-sql-operations-studio-preview-for-macos"></a>获取 macOS SQL 操作 Studio （预览版）

1. 下载[[!INCLUDE[name-sos](../includes/name-sos-short.md)]为 macOS](https://go.microsoft.com/fwlink/?linkid=866481)。
2. 若要展开此 zip 的内容，请双击它。
3. 若要使[!INCLUDE[name-sos](../includes/name-sos-short.md)]位于*快速启动板*，拖动*sqlops.app*到*应用程序*文件夹。


## <a name="get-sql-operations-studio-preview-for-linux"></a>获取适用于 Linux 的 SQL 操作 Studio （预览版）

1. 下载[[!INCLUDE[name-sos](../includes/name-sos-short.md)]适用于 Linux](https://go.microsoft.com/fwlink/?linkid=866482)。
1. 若要提取的文件和启动[!INCLUDE[name-sos](../includes/name-sos-short.md)]，打开新的终端窗口并键入以下命令：

   ```bash
   cd ~
   cp ~/Downloads/sqlops-linux-<version string>.tar.gz ~
   tar -xvf ~/sqlops-linux-<version string>.tar.gz
   echo 'export PATH="$PATH:~/sqlops-linux-x64"' >> ~/.bashrc
   source ~/.bashrc
   sqlops
   ```

   > [!NOTE]
   > 在 Ubuntu 和 Redhat 上，您可能必须缺失的依赖关系。 使用以下命令安装这些依赖项，具体取决于你的 Linux 版本：
   
   **Ubuntu:** 
   ```bash
   sudo apt-get install libxss1

   sudo apt-get install libgconf-2-4

   sudo apt-get install libunwind8
   ```

   **Redhat:** 
   ```bash
   yum install libXScrnSaver
   ```

## <a name="uninstall-sql-operations-studio-preview"></a>卸载 SQL 操作 Studio （预览版）

如果你安装[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]使用 Windows 安装程序，然后卸载相同的方式删除所有 Windows 应用程序。

如果你安装[!INCLUDE[name-sos-short](../includes/name-sos-short.md)].zip 或其他存档，然后只需删除的文件。

## <a name="supported-operating-systems"></a>支持的操作系统

[!INCLUDE[name-sos](../includes/name-sos-short.md)]在 Windows、 macOS 和 Linux 上运行，并且支持以下平台上：

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
- macOS 10.13 高 Sierra
- macOS 10.12 Sierra

### <a name="linux"></a>Linux
- Red Hat Enterprise Linux 7.4
- Red Hat Enterprise Linux 7.3
- SUSE Linux Enterprise Server v12 SP2
- Ubuntu 16.04

## <a name="check-for-updates"></a>检查更新
若要检查最新的更新，请单击的窗口中，然后单击左下角的齿轮图标**检查更新**

## <a name="next-steps"></a>后续步骤

请参阅以下快速入门中，若要开始之一：
- [连接和查询 SQL Server](quickstart-sql-server.md)
- [连接和查询 Azure SQL 数据库](quickstart-sql-database.md)
- [连接和查询 Azure 数据仓库](quickstart-sql-dw.md)

贡献[!INCLUDE[name-sos](../includes/name-sos-short.md)]:
- [https://github.com/Microsoft/sqlopsstudio](https://github.com/Microsoft/sqlopsstudio) 

[Microsoft 隐私声明](https://go.microsoft.com/fwlink/?LinkId=521839)和[使用情况数据收集](usage-data-collection.md)。
