---
title: "SQL Server 的帮助查看器 | Microsoft Docs"
ms.custom: 
ms.date: 02/15/2017
ms.prod: sql-non-specified
ms.technology: server-general
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2014
- SQL Server 2016
ms.assetid: 51f8a08c-51d0-41d8-8bc5-1cb4d42622fb
caps.latest.revision: 8
author: sabotta
ms.author: carlasab
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: fc2435ccea3b01328c3c4623e62fbf12ee53e400
ms.lasthandoff: 04/11/2017

---
# <a name="help-viewer-for-sql-server"></a>SQL Server 的帮助查看器
  
  
  
本文逐步讲解如何安装本地帮助，以及如何显示联机帮助和本地帮助。 本文介绍 Microsoft 帮助查看器 1.1 和 2.2，并提供 [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)] 和 [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] 的文档。 

>[!IMPORTANT]
>帮助查看器不支持代理设置，也不支持 ISO 格式。  

>**F1 和帮助**
>>按 F1 会在线显示相应的主题。 无法在本地帮助中显示该主题。

## <a name="includesscurrentmdincludessscurrent-mdmd-and-help-viewer-22"></a>[!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] 和帮助查看器 2.2  
帮助查看器 2.2 在 2016 年 4 月预览版 (13.0.12500.29) 和更高版本的 [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] Management Studio 中以及 Visual Studio 2015 中提供。  

> [![下载 SSMS](../release-notes/media/download.png)](https://msdn.microsoft.com/library/mt238290.aspx) **[下载 SQL Server Management Studio 的最新版本](https://msdn.microsoft.com/library/mt238290.aspx)**  

**安装与帮助查看器 2.2 配合使用的本地帮助**  
1. 启动 SQL Server Management Studio 或 Visual Studio，然后在“帮助”菜单中单击“添加和删除帮助内容”，打开帮助查看器 2.2。  
2. 单击“管理内容”选项卡。  
3. 若要从联机源安装帮助，请在“安装源”区域中单击“联机”。  
![HelpViewer2_ManageContent_OnlineSource](../release-notes/media/helpviewer2-managecontent-onlinesource.png)  
7. 单击要安装的文档旁边的“添加”，然后单击“更新”。  
![HelpViewer2_ManageContent_AddContent](../release-notes/media/helpviewer2-managecontent-addcontent.png)     
  
   >[!IMPORTANT] 
   >在 SQL Server Management Studio 和 Visual Studio 中，在添加文档的过程中帮助查看器应用程序可能冻结（挂起）。 若要解决此问题，请执行以下操作。 有关此问题的详细信息，请参阅 [《Visual Studio 帮助查看器冻结》](https://msdn.microsoft.com/library/mt654096.aspx)。  
   >>在记事本中打开 %LOCALAPPDATA%\Microsoft\HelpViewer2.2\HlpViewer_SSMS16_en-US.settings |HlpViewer_VisualStudio14_en US.settings 文件，并将下面代码中的日期更改为在将来的某个日期。 仅当已安装 Visual Studio 时，才会在本地计算机上提供此文件。 
   >>>Cache LastRefreshed="12/31/2017 00:00:00"  
  
    左窗格中的目录会自动更新，以包含添加的文档。  
![HelpViewer2_withContentInstalled](../release-notes/media/helpviewer2-withcontentinstalled.png)

1. （可选）“管理内容”选项卡上的“本地存储路径”框显示文档在本地计算机上的安装位置。 若要将文档移到其他位置，请单击“移动”，在“移动内容”对话框的“到”字段中输入文件夹路径，然后单击“确定”。

   ![HelpViewer2_Move Content Dialog](../release-notes/media/helpviewer2-move-content-dialog.png)

   移动内容后，新位置将显示在“本地存储路径”中。
      
   >[!IMPORTANT]
   > 如果显示了一条消息指出移动操作失败，请关闭消息框并关闭帮助查看器，然后重新打开帮助查看器。 现在，内容的新位置应会显示在“本地存储路径”中。   
  
**在 SQL Server Management Studio 中显示本地帮助或联机帮助**  
* 若要查看本地帮助，请在“帮助”菜单中单击“添加和删除帮助内容”，然后单击“帮助查看器主页”选项卡查看文档。  
    >[!NOTE]
    >文本“帮助查看器主页”会根据你在目录中单击的主题发生变化。   
* 若要查看联机帮助，请在“帮助”菜单中单击“查看帮助”。 文档将显示在浏览器中。  
![HelpViewer2_SSMS_ChooseOnlineORLocalHelp](../release-notes/media/helpviewer2-ssms-chooseonlineorlocalhelp.png)  
  
  
**在 Visual Studio 中显示本地帮助或联机帮助**  
* 在“帮助”菜单中单击“帮助设置首选项”，然后执行以下操作之一。  
   * 单击“在浏览器中启动”可查看联机帮助。 在“帮助”菜单中单击“查看帮助”时，文档将显示在浏览器中。  
   * 单击“在帮助查看器中启动”可查看本地帮助。 在“帮助”菜单中单击“查看帮助”时，文档将显示在帮助查看器中。  
     
     ![HelpViewer2_VisualStudio_ChooseOnlineORLocalHelp](../release-notes/media/helpviewer2-visualstudio-chooseonlineorlocalhelp.png)  
  
  
## <a name="includesssql14mdincludessssql14-mdmd-and-help-viewer-11"></a>[!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)] 和帮助查看器 1.1  
 Help Viewer 1.1 在 [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)] Management Studio 以及低于 Visual Studio 2012 的 Visual Studio 版本中提供。   
 
>[!NOTE]
> 也可以使用帮助查看器 2.2 查看 [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)] 的本地帮助，前提是选择“从磁盘安装内容”。 帮助查看器 2.2 在 2016 年 4 月预览版 (13.0.12500.29) 和更高版本的 [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] Management Studio 中以及 Visual Studio 2015 中提供。 
   
**安装与帮助查看器 1.1 配合使用的本地帮助**  
1. 导航到帮助内容的[下载站点](https://www.microsoft.com/en-us/download/details.aspx?id=42557)，然后单击“下载”。  
2. 在消息框中单击“保存”，将 SQLServer2014Documentation_*.exe 文件保存到计算机。  
   >[!NOTE]
   >对于防火墙和代理受限的环境，请将下载内容保存到 USB 驱动器，或其他可以接入环境的便携媒体。   
3. 双击 .exe 解压缩帮助内容文件并将该文件保存到本地文件夹或共享文件夹。  
4. 启动 SQL Server Management Studio 或 Visual Studio，然后在“帮助”菜单中单击“管理帮助设置”，打开“帮助库管理器”。  
7. 单击“从磁盘安装内容”，然后浏览到帮助内容文件解压缩到的文件夹。  
  
选择“从磁盘安装内容”  |浏览到内容帮助文件   
---------|---------  
![HelpLibraryManager_MainPage_InstallFromDisk](../release-notes/media/helplibrarymanager-mainpage-installfromdisk.png)    | ![HelpLibraryManager_InstallContentFromDisk_dialog1](../release-notes/media/helplibrarymanager-installcontentfromdisk-dialog1.png)          
  
>[!IMPORTANT]
> 若要避免安装只包含一部分目录的本地帮助内容，请使用“帮助库管理器”中的“从磁盘安装内容”选项。  
>>如果你已使用“联机安装内容”选项，而帮助查看器显示部分目录，请参阅此[博客文章](https://blogs.msdn.microsoft.com/womeninanalytics/2016/06/21/troubleshoot-local-help-for-sql-server-2014/)获取故障排除步骤。 

8. 依次单击 HelpContentSetup.msha 文件、“打开”、“下一步”。  
9. 单击要安装的文档旁边的“添加”，然后单击“更新”。  
  
   ![HelpLibraryManager_InstallContentFromDisk_dialog2](../release-notes/media/helplibrarymanager-installcontentfromdisk-dialog2.png)  
10. 依次单击“完成”、“退出”，然后在“帮助”菜单中单击“查看帮助”打开帮助查看器来查看内容。 左窗格中的目录内应会列出已安装的内容。  
  
    ![HelpViewer1_withContentInstalled_ZoomedIn](../release-notes/media/helpviewer1-withcontentinstalled-zoomedin.png)  
  
**显示本地帮助或联机帮助**  
1. 在“帮助”菜单中单击“管理帮助设置”打开“帮助库管理器”。  
2. 在“帮助库管理器”对话框中，单击“选择联机帮助或本地帮助”。  
  
   ![HelpLibraryManager_MainPage_ChooseOnlineORLocal.png](../release-notes/media/helplibrarymanager-mainpage-chooseonlineorlocal.png.png)  
3. 执行以下操作之一，然后依次单击“确定”、“退出”。  
   * 单击“我想要使用联机帮助”  
   * 单击“我想要使用本地帮助”。  
  
   ![HelpLibraryManager_ChooseOnlineORLocalHelp_OnlineHelpSelected_dialog](../release-notes/media/helplibrarymanager-chooseonlineorlocalhelp-onlinehelpselected-dialog.png)  
  
如果你已选择使用联机帮助，则在“帮助”菜单中单击“查看帮助”时，浏览器将会启动并显示 MSDN 上的 [Books Online for SQL Server 2014](https://msdn.microsoft.com/library/ms130214(v=sql.120).aspx)（有关 SQL Server 2014 的联机丛书）一文。 如果你已选择使用本地帮助，则单击“查看帮助”会启动帮助查看器。  

## <a name="additional-information"></a>其他信息
[Microsoft 帮助查看器 - Visual Studio 2015](https://msdn.microsoft.com/library/hh580782.aspx)

