---
title: "SQL Server 的帮助查看器和脱机内容 | Microsoft Docs"
ms.custom: 
ms.date: 06/27/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: sql-non-specified
ms.technology: server-general
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2014
- SQL Server 2016
- SQL Server 2017
ms.assetid: 51f8a08c-51d0-41d8-8bc5-1cb4d42622fb
caps.latest.revision: "8"
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 048b1d257287b8f0a4645f57ce88c30b24a9f654
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2017
---
# <a name="help-viewer-and-offline-content-for-sql-server"></a>SQL Server 的帮助查看器和脱机内容
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
  
  
本文向你介绍如何安装帮助查看器和脱机查看 SQL Server 文档。 本文包含用于 [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)]、SQL Server 2016 和 SQL Server 2017 的文档 。 

## <a name="install-help-viewer"></a>安装帮助查看器
下表根据使用的 SQL Server 版本，列出了安装帮助查看器的工具。 安装列出的一种工具来安装帮助查看器。


|**SQL Server 版本**|**安装帮助查看器的工具**|**已安装的帮助查看器版本**|
|---------|---------|---------|
|SQL Server 2017<br>SQL Server 2016     |   [最新版 SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)<br><br>[最新版 SQL Server Data Tools for Visual Studio 2015](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)<br><br>Visual Studio 2017（仅支持 SQL Server 2016）  |  v2.x       |
|SQL Server 2014    | SQL Server 2014 Management Studio<br><br>Visual Studio 2012 之前的 Visual Studio 版本        |  v1.x       |


> [!IMPORTANT]
> SQL Server 2016 安装的帮助查看器 1.1 无法用于查看关于 SQL Server 2016 和 SQL Server 2017 的文档。
> <br>
> <br>
> SQL Server 2017 不会安装帮助查看器。
> <br>
> <br>
> 若要使用 Visual Studio 2017 安装帮助查看器，请单击“Visual Studio 安装程序”程序中的“各个组件”选项卡，单击“代码工具”类别中的“帮助查看器”，然后单击“安装”。 
> <br>
> <br>
> 可以使用帮助查看器 2.x 查看 [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)] 的本地帮助，前提是已选择“从磁盘安装内容”。 


## <a name="sql-server-2016-sql-server-2017-offline-content"></a>SQL Server 2016 和 SQL Server 2017 脱机内容  
 
**安装脱机内容**  
1. 启动 SQL Server Management Studio 或 Visual Studio，然后在“帮助”菜单中单击“添加和删除帮助内容”，打开帮助查看器。  
2. 单击“管理内容”选项卡。  
3. 若要从联机源安装帮助，请在“安装源”区域中单击“联机”。  
![HelpViewer2_ManageContent_OnlineSource](../sql-server/media/helpviewer2-managecontent-onlinesource.png)  
7. 单击要安装的文档旁边的“添加”，然后单击“更新”。  
![HelpViewer2_ManageContent_AddContent](../sql-server/media/helpviewer2-managecontent-addcontent.png)     
  
   >[!IMPORTANT] 
   >在 SQL Server Management Studio 和 Visual Studio 中，在添加文档的过程中帮助查看器应用程序可能冻结（挂起）。 若要解决此问题，请执行以下操作。 有关此问题的详细信息，请参阅 [《Visual Studio 帮助查看器冻结》](https://msdn.microsoft.com/library/mt654096.aspx)。  
   >>在记事本中打开 %LOCALAPPDATA%\Microsoft\HelpViewer2.3\HlpViewer_SSMS16_en-US.settings | HlpViewer_VisualStudio15_en-US.settings 文件，并将下面代码中的日期更改为将来的某个日期。 仅当已安装 Visual Studio 时，才会在本地计算机上提供此文件。 
   >>>Cache LastRefreshed="12/31/2017 00:00:00"  
  
    左窗格中的目录会自动更新，以包含添加的文档。  
![HelpViewer2_withContentInstalled](../sql-server/media/helpviewer2-withcontentinstalled.png)

1. （可选）“管理内容”选项卡上的“本地存储路径”框显示文档在本地计算机上的安装位置。 若要将文档移到其他位置，请单击“移动”，在“移动内容”对话框的“到”字段中输入文件夹路径，然后单击“确定”。

   ![HelpViewer2_Move Content Dialog](../sql-server/media/helpviewer2-move-content-dialog.png)

   移动内容后，新位置将显示在“本地存储路径”中。
      
   >[!IMPORTANT]
   > 如果显示了一条消息指出移动操作失败，请关闭消息框并关闭帮助查看器，然后重新打开帮助查看器。 现在，内容的新位置应会显示在“本地存储路径”中。   
 
## <a name="includesssql14mdincludessssql14-mdmd-offline-content"></a>[!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)] 脱机内容 
 
  
**安装脱机内容**  
1. 导航到帮助内容的[下载站点](https://www.microsoft.com/en-us/download/details.aspx?id=42557)，然后单击“下载”。  
2. 在消息框中单击“保存”，将 SQLServer2014Documentation_*.exe 文件保存到计算机。  

 对于防火墙和代理受限的环境，请将下载内容保存到 USB 驱动器，或其他可以接入环境的便携媒体。   

3. 双击 .exe 解压缩帮助内容文件并将该文件保存到本地文件夹或共享文件夹。  
4. 启动 SQL Server Management Studio 或 Visual Studio，然后在“帮助”菜单中单击“管理帮助设置”，打开“帮助库管理器”。  
5. 单击“从磁盘安装内容”，然后浏览到帮助内容文件解压缩到的文件夹。  
  
     选择“从磁盘安装内容”  |浏览到内容帮助文件   
     ---------|---------  
     ![HelpLibraryManager_MainPage_InstallFromDisk](../sql-server/media/helplibrarymanager-mainpage-installfromdisk.png)    | ![HelpLibraryManager_InstallContentFromDisk_dialog1](../sql-server/media/helplibrarymanager-installcontentfromdisk-dialog1.png)          
  
     >[!IMPORTANT]
     > 若要避免安装只包含一部分目录的本地帮助内容，请使用“帮助库管理器”中的“从磁盘安装内容”选项。  
     >>如果你已使用“联机安装内容”选项，而帮助查看器显示部分目录，请参阅此[博客文章](https://blogs.msdn.microsoft.com/womeninanalytics/2016/06/21/troubleshoot-local-help-for-sql-server-2014/)获取故障排除步骤。 

8. 依次单击 HelpContentSetup.msha 文件、“打开”、“下一步”。  
9. 单击要安装的文档旁边的“添加”，然后单击“更新”。  
  
   ![HelpLibraryManager_InstallContentFromDisk_dialog2](../sql-server/media/helplibrarymanager-installcontentfromdisk-dialog2.png)  
10. 单击“完成”，单击“退出”。
11. 再次打开“帮助库管理器”，单击“选择联机或本地帮助”，然后单击“使用本地帮助”。
12. 在“帮助”菜单中单击“查看帮助”，打开帮助查看器来查看内容。 左窗格中的目录内应会列出已安装的内容。  
  
    ![HelpViewer1_withContentInstalled_ZoomedIn](../sql-server/media/helpviewer1-withcontentinstalled-zoomedin.png)  
  
## <a name="view-online-content-in-help-viewer"></a>在帮助查看器中查看联机内容

在帮助查看器 v2.x 中，可通过执行以下任一操作来查看联机内容。

- 在 SQL Server Management Studio 中，单击“帮助”菜单中的“查看帮助”。 文档将显示在浏览器中。
![HelpViewer2_SSMS_ChooseOnlineORLocalHelp](../sql-server/media/helpviewer2-ssms-chooseonlineorlocalhelp.png)

- 在 Visual Studio 中，单击“帮助”菜单中的“设置帮助首选项”，然后单击“在浏览器中启动”。 在“帮助”菜单中单击“查看帮助”时，文档将显示在浏览器中。

![HelpViewer2_VisualStudio_ChooseOnlineORLocalHelp](../sql-server/media/helpviewer2-visualstudio-chooseonlineorlocalhelp.png)   

在帮助查看器 v1.x 中，可通过执行以下操作来查看联机内容。
1. 在“帮助”菜单中单击“管理帮助设置”打开“帮助库管理器”。  
2. 在“帮助库管理器”对话框中，单击“选择联机帮助或本地帮助”。  
  
   ![HelpLibraryManager_MainPage_ChooseOnlineORLocal.png](../sql-server/media/helplibrarymanager-mainpage-chooseonlineorlocal.png.png)  
3. 单击“我想要使用联机帮助”，单击“确定”，然后单击“退出”。  

   ![HelpLibraryManager_ChooseOnlineORLocalHelp_OnlineHelpSelected_dialog](../sql-server/media/helplibrarymanager-chooseonlineorlocalhelp-onlinehelpselected-dialog.png)

## <a name="f1-help-and-other-tips"></a>F1 帮助和其他提示

按 F1 会在线显示相应的主题。 无法在本地帮助中显示该主题。

此外，帮助查看器不支持代理设置，也不支持 ISO 格式。 

## <a name="additional-information"></a>其他信息
[Microsoft Help Viewer - Visual Studio](/visualstudio/ide/microsoft-help-viewer)  
[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
