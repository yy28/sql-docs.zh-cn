---
title: SQL Server 帮助内容和帮助查看器 | Microsoft Docs
ms.custom: ''
ms.date: 12/10/2019
ms.prod: sql
ms.technology: ''
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 51f8a08c-51d0-41d8-8bc5-1cb4d42622fb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1352a7f469e72100f7a2e0573c87cbb8422fe413
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "77608487"
---
# <a name="sql-server-offline-help-and-help-viewer"></a>SQL Server 脱机帮助和帮助查看器

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

可使用 Microsoft Help Viewer，从联机源或本地磁盘处下载和安装 SQL Server 帮助包。 然后，在脱机状态下查看内容。 此 Help Viewer 可使用几种不同的工具进行安装。 本文介绍安装 Help Viewer 的相关工具、如何安装脱机帮助内容，以及如何查看帮助。

下载帮助查看器内容需要 Internet 访问权限。 然后可以将内容迁移到没有 Internet 访问权限的计算机。

>[!NOTE]
> 要获取当前版 SQL Server 的本地内容，请安装当前版本的 SQL Server Management Studio [SQL Server Management Studio 18.x](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。

## <a name="what-tools-install-the-help-viewer-versions"></a>Help Viewer 版本的安装工具是什么？

Microsoft Help Viewer 有两个主要版本。  版本 1.x 和 2.x。 每个版本支持不同版本的 SQL Server 内容。  脱机丛书的格式随时间推移而改变，且较旧的 Help Viewer 版本不支持较新的丛书版本。

|**内容集**|**安装 Help Viewer 的工具**|**Help Viewer 版本**|
|-|-|-|
|SQL Server 2019 <br><br><br>SQL Server 2017 <br>SQL Server 2016 | [Visual Studio 2019 (\*1)](https://docs.microsoft.com/visualstudio/install/install-visual-studio?view=vs-2019) <br>[SQL Server Management Studio 18.x](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) <br><br>[Visual Studio 2017 (\*1)](https://docs.microsoft.com/visualstudio/install/install-visual-studio?view=vs-2017) <br>[SQL Server Management Studio 17.x](https://docs.microsoft.com/sql/ssms/release-notes-ssms?view=sql-server-2017#1791) <br>[SQL Server Data Tools for Visual Studio 2015](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt) <br>Visual Studio 2015 | v2.3 <br><br><br>v2.2 |
|SQL Server 2014<br>SQL Server 2012|SQL Server 2016 安装程序 (\*2)<br>SQL Server 2014 Management Studio<br>SQL Server 2014 安装程序 (\*2)<br>SQL Server Management Studio 2012<br>SQL Server 2012 安装程序 (\*2)| v1.x|
| | | |

(\*1) 要使用 Visual Studio 2019 或 2017 安装 Help Viewer，请在“Visual Studio 安装程序”的“单个组件”选项卡上，选择“代码工具”\>“Help Viewer”\>“安装”     。

(\*2) 表示 SQL Server 安装程序中的“文档组件”选项  。

>[!NOTE]
> - SQL Server 2016 可安装 Help Viewer 1.1，但后者不支持 SQL Server 2016 帮助内容。 要查看 SQL Server 2016 的内容，需要 Help Viewer 的 v2.x 版本。 有关详细信息，请参阅 [SQL Server 2016 发行说明](sql-server-2016-release-notes.md)。
> - Help Viewer 2.x 至少可以显示 SQL Server 版本 2014 - 2019 的文档。
> - 获取 Help Viewer 2.3 或更高版本的一种简单方法是先下载最新版本的 `SSMS.exe`（免费）。 然后使用 SSMS 的“帮助”  菜单。
> - 从 SQL Server 2017 开始，便无法从 SQL Server 安装程序安装 Help Viewer。

## <a name="use-help-viewer-v2x"></a>使用帮助查看器 v2.x

对于此方法，建议使用 Help Viewer 2.3 或更高版本。 [最新版本的 SSMS.exe](../ssms/download-sql-server-management-studio-ssms.md) 中的“帮助”  菜单提供 2.3 版本或更高版本。

### <a name="to-download-and-install-offline-help-content-with-help-viewer-v2x"></a>使用 Help Viewer v2.x 下载并安装脱机帮助内容

1. 在 SSMS 或 VS 中，单击“帮助”菜单中的“添加和删除帮助内容”  。 

   ![HelpViewer2 添加/删除内容](../sql-server/media/sql-server-help-installation/addremovecontent.png)  

   帮助查看器随即打开“管理内容”选项卡。  
   
2. 要安装最新帮助内容包，请在“安装源”下选择“联机”  。
   
   ![HelpViewer2_ManageContent_OnlineSource](../sql-server/media/sql-server-help-installation/helpviewer2-managecontent-onlinesource.png)  
   
   >[!NOTE]
   > 要从磁盘（SQL Server 2014 帮助）进行安装，请在“安装源”下选择“磁盘”，并指定磁盘位置  。
   
   “管理内容”选项卡上的“本地存储路径”显示内容在本地计算机上的安装位置。 要更改位置，请单击“移动”，在“到”字段中输入不同的文件夹路径，然后单击“确定”    。
   如果在更改本地存储路径后帮助安装失败，请关闭并重新打开 Help Viewer。 确保本地存储路径中显示了新位置，然后重试安装。

3. 在每个要安装的内容包（丛书）旁，单击“添加”  。 
   要安装所有 SQL Server 帮助内容，请添加 SQL Server 下的全部 13 本丛书。 
   
4. 单击右下方的“更新”  。 
   添加丛书时，左侧的帮助目录将自动更新。 
   
   ![HelpViewer2_ManageContent_AddContent](../sql-server/media/sql-server-help-installation/helpviewer2-managecontent-addcontent.png)     
   
> [!NOTE]
> 并非 SQL Server 目录中的所有顶部节点标题都与相应的可下载帮助丛书的名称完全匹配。 TOC 标题映射的丛书名称如下：

(*) 内容来自 SQL Server 2017 第一个正式发布版内容以及较旧的 2016 内容。 自 2019 年 1 月起，这些丛书将作为包含内容编辑的单独、完整 SQL Server 2016 和 SQL Server 2017 丛书删除。  

| | 内容窗格 | SQL Server 丛书 |
|-----|-----|-----|
|*|Analysis Services 语言参考 | Analysis Services (MDX) 语言参考|
|*|数据分析表达式 (DAX) 参考 | 数据分析表达式 (DAX) 参考|
|*|数据挖掘扩展插件 (DMX) 参考 | 数据挖掘扩展插件 (DMX) 参考|
|*|SQL Server 机器学习入门 | Microsoft 机器学习服务|
|*|Power Query M 参考 | Power Query M 参考|
||SQL Server 2016 文档 | SQL Server 2016 文档|
||SQL Server 2017 文档| SQL Server 2017 文档|
|*|SQL Server 开发人员指南 | SQL Server Developer 参考|
|*|下载 SQL Server Management Studio | SQL Server Management Studio|
|*|Microsoft SQL Server 客户端编程的主页 | SQL Server 连接驱动程序|
|*|Linux 上的 SQL Server | Linux 上的 SQL Server|
|*|SQL Server 技术文档 | SQL Server 技术文档（SSIS、SSRS、数据库引擎、安装程序）|
|*|用于 Azure SQL 数据库的工具和实用程序 | SQL Server 工具|
|*|Transact-SQL 引用（数据库引擎） | Transact-SQL 参考|
|*|Xquery 语言参考 (SQL Server) | Xquery 语言参考 (SQL Server)|
| &nbsp; | &nbsp; | &nbsp; |

> [!NOTE]
> 如果帮助查看器在添加内容时冻结（挂起），请将 %LOCALAPPDATA%\Microsoft\HelpViewer2.x\HlpViewer_SSMSx_en-US.settings 或 HlpViewer_VisualStudiox_en-US.settings 文件中的 Cache LastRefreshed="\<mm/dd/yyyy> 00:00:00" 行更改为将来的某个日期。 有关此问题的详细信息，请参阅 [《Visual Studio 帮助查看器冻结》](/visualstudio/welcome-to-visual-studio)。

### <a name="to-view-offline-help-content-in-ssms-with-help-viewer-v2x"></a>使用 Help Viewer v2.x 查看 SSMS 中的脱机帮助内容

要在 SSMS 中查看已安装的帮助，请按 CTRL+ALT+F1，或从“帮助”菜单中选择“添加或删除内容”启动帮助查看器  。 

   ![HelpViewer2 添加/删除内容](../sql-server/media/sql-server-help-installation/addremovecontent.png)  

帮助查看器随即打开“管理内容”选项卡，并在左窗格中显示已安装的帮助目录。 单击目录中的项目以在右窗格显示它们。
> [!TIP]
> 如果内容窗格不可见，请在左边距上单击“内容”。 单击图钉图标使内容窗格保持打开状态。  

   ![显示内容的帮助查看器 v2.x](../sql-server/media/sql-server-help-installation/helpviewer2-withcontentinstalled.png)

### <a name="to-view-offline-help-content-in-vs-with-help-viewer-v2x"></a>使用 Help Viewer v2.x 查看 VS 中的脱机帮助内容

在 Visual Studio 中查看已安装的帮助：
1. 请指向“帮助”菜单上的“设置帮助首选项”，并选择“在帮助查看器中启动”   。 

   ![VS 帮助视图设置首选项帮助查看器](../sql-server/media/sql-server-help-installation/launchviewer.png)

2. 在“帮助”菜单中单击“查看帮助”以显示帮助查看器中的内容  。 

   ![查看帮助](../sql-server/media/sql-server-help-installation/viewhelp.png)

   帮助目录显示在左侧，选定的帮助项目显示在右侧。
  
## <a name="use-help-viewer-v1x"></a>使用帮助查看器 v1.x

在本部分中，将执行以下常规步骤：

- 手动下载 SQL Server 2014 脱机丛书（由四部分组成）。
- 使用 SSMS 或 VS 的“帮助”  菜单启动 Help Viewer。
- 最后，让 Help Viewer 知道 SQL Server 2014 的 `*.msha` 文件位于本地硬盘上。

更早版本的 SSMS 和 VS 提供了 Help Viewer 的 1.x 版本。 1.x 能够显示 SQL Server 版本 2012 和 2014 的脱机丛书。 但 1.x 不能显示 SQL Server 2016 或更高版本的脱机图书。

在你将 SQL Server 2014 脱机图书下载到本地硬盘之后，Help Viewer 2.3 仍能显示 SQL Server 2014 脱机图书。

### <a name="to-download-and-install-offline-help-content-with-help-viewer-v1x"></a>使用 Help Viewer v1.x 下载并安装脱机帮助内容

此过程将使用帮助查看器 1.x 从 Microsoft 下载中心下载 SQL Server 2014 帮助，并将其安装在计算机上。

1. 请导航到 [Microsoft SQL Server 2014 产品文档](https://www.microsoft.com/download/details.aspx?id=42557)下载站点并单击“下载”  。

2. 在消息框中单击“保存”，将 SQLServer2014Documentation\_\*.exe 文件保存到计算机   。

   > [!NOTE]
   > 对于防火墙和代理受限的环境，请将下载内容保存到 USB 驱动器，或其他可以接入环境的便携媒体。

3. 双击 .exe 解压缩帮助内容文件，并将该文件保存到本地文件夹或共享文件夹。

4. 启动 SSMS 或 VS 并单击“帮助”菜单中的“管理帮助设置”，打开“帮助库管理器”   。

5. 单击“从磁盘安装内容”，然后浏览到帮助内容文件解压缩到的文件夹  。

   ![HelpLibraryManager_MainPage_InstallFromDisk](../sql-server/media/sql-server-help-installation/helplibrarymanager-mainpage-installfromdisk.png)

   ![HelpLibraryManager_InstallContentFromDisk_dialog1](../sql-server/media/sql-server-help-installation/helplibrarymanager-installcontentfromdisk-dialog1.png)

   > [!IMPORTANT]
   > 要避免安装只包含一部分目录的本地帮助内容，请务必使用“帮助库管理器”中的“从磁盘安装内容”选项   。  如果已使用“联机安装内容”，而帮助查看器显示部分目录，请参阅此[博客文章](https://blogs.msdn.microsoft.com/womeninanalytics/2016/06/21/troubleshoot-local-help-for-sql-server-2014/)获取故障排除步骤  。

6. 单击 `HelpContentSetup.msha` 文件，单击“打开”  **，然后单击“下一步”** 。

7. 单击要安装的文档旁边的“添加”，然后单击“更新”。  

   ![HelpLibraryManager_InstallContentFromDisk_dialog2](../sql-server/media/sql-server-help-installation/helplibrarymanager-installcontentfromdisk-dialog2.png)

8. 单击“完成”，然后单击“退出”   。

### <a name="to-view-offline-help-content-with-help-viewer-v1x"></a>使用 Help Viewer v1.x 查看脱机帮助内容

1. 要查看已安装的帮助，请打开“帮助库管理器”，单击“选择联机或本地帮助”，然后单击“我想要使用本地帮助”    。

2. 在“帮助”  菜单中单击“查看帮助”  ，打开帮助查看器来查看内容。 已安装的内容将在左窗格中列出。

   ![HelpViewer1_withContentInstalled_ZoomedIn](../sql-server/media/sql-server-help-installation/helpviewer1-withcontentinstalled-zoomedin.png)  

## <a name="view-online-help"></a>查看联机帮助

联机帮助始终显示最新内容。 

### <a name="to-view-sql-server-online-help-in-ssms-17x"></a>在 SSMS 17.x 中查看 SQL Server 联机帮助

- 在“帮助”菜单中单击“查看帮助”   。 [https://docs.microsoft.com/sql/sql-server/](https://docs.microsoft.com/sql/sql-server/) 中的最新 SQL Server 2016/2017 文档在浏览器中显示。

   ![查看帮助](../sql-server/media/sql-server-help-installation/viewhelp.png)

### <a name="to-view-visual-studio-online-help-in-visual-studio"></a>在 Visual Studio 中查看 Visual Studio 联机帮助

1. 请指向“帮助”菜单上的“设置帮助首选项”，并选择“在浏览器中启动”或“在帮助查看器中启动”    。 
2. 在“帮助”菜单中单击“查看帮助”  。 最新的 Visual Studio 帮助将显示在选定环境中。 

**使用帮助查看器 v1.x 查看联机帮助**

1. 在“帮助”菜单上单击“管理帮助设置”，打开“帮助库管理器”   。  
2. 在“帮助库管理器”对话框中，单击“选择联机帮助或本地帮助”  。  
   
   ![HelpLibraryManager_MainPage_ChooseOnlineORLocal.png](../sql-server/media/sql-server-help-installation/helplibrarymanager-mainpage-chooseonlineorlocal.png.png)  
   
3. 单击“我想要使用联机帮助”，单击“确定”，然后单击“退出”    。  
   
   ![HelpLibraryManager_ChooseOnlineORLocalHelp_OnlineHelpSelected_dialog](../sql-server/media/sql-server-help-installation/helplibrarymanager-chooseonlineorlocalhelp-onlinehelpselected-dialog.png)

4. 在“帮助”  菜单中单击“查看帮助”  ，打开帮助查看器来查看内容。

## <a name="view-f1-help"></a>查看 F1 帮助

在 SSMS 或 VS 的对话框中   按 F1，或单击“帮助”或“?”图标时，浏览器或 Help Viewer 中将显示上下文相关的联机帮助项目。

### <a name="to-view-f1-help"></a>查看 F1 帮助

1. 在“帮助”菜单中，单击“设置帮助首选项”，并选择“在浏览器中启动”或“在 Help Viewer 中启动”    。
2. 当这些选项可用时，   请在对话框内按 F1，或单击“帮助”或“?”图标，以便在所选环境中查看上下文相关的联机项目。

> [!NOTE]
> F1 帮助仅在联机状态可用。 F1 帮助不提供脱机资源。

## <a name="systems-without-internet-access"></a>没有 internet 访问权限的系统
在具有 Internet 访问权限的系统上下载了脱机丛书之后，可以使用以下步骤将内容迁移到没有 Internet 访问权的系统。

  >[!NOTE]
  >必须在脱机系统上安装支持帮助查看器的软件（如 SQL Server Management Studio）。

1. 打开帮助查看器 (Ctrl + Alt + F1)。
1. 选择感兴趣的文档。 例如，通过 SQL 进行筛选并选择 SQL Server 技术文档。
1. 标识可以在“本地存储路径”下找到的磁盘上文件的物理路径  。
1. 使用文件系统资源管理器导航到此位置。
    1.  默认位置是： `C:\Program Files (x86)\Microsoft SQL Server\140\Tools\Binn\ManagementStudio\Extensions\Application`
1. 选择三个文件夹（“ContentStore”、“传入”、“IndexStore”），并将它们复制到脱机系统上的同一位置    。 可能需要使用临时媒体设备（如 USB 或 CD）。
1. 移动这些文件后，在脱机系统上启动帮助查看器，然后便可以使用 SQL Server 技术文档。

![physical-location-of-offline-content.png](media/sql-server-help-installation/physical-location-of-offline-content.png)

## <a name="next-steps"></a>后续步骤
[Microsoft Help Viewer - Visual Studio](/visualstudio/ide/microsoft-help-viewer)  

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
