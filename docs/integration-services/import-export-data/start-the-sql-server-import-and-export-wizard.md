---
title: "启动 SQL Server 导入和导出向导-> |Microsoft 文档"
ms.custom: 
ms.date: 06/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Import and Export Wizard
- starting SQL Server Import and Export Wizard
- Import and Export Wizard
- starting Import and Export Wizard
ms.assetid: 5fc4f6d1-1f6f-444e-9aeb-827f85e1c405
caps.latest.revision: 130
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 4fd91a36594a8d0d50e3f4eb8490497d6fe0e172
ms.contentlocale: zh-cn
ms.lasthandoff: 09/27/2017

---
# <a name="start-the-sql-server-import-and-export-wizard"></a>启动 SQL Server 导入和导出向导

 > 与以前版本的 SQL Server 相关的内容，请参阅[运行 SQL Server 导入和导出向导](https://msdn.microsoft.com/en-US/library/ms140052(SQL.120).aspx)。

启动[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]导入和导出向导中本主题中所述的方式之一从中导入数据并将数据导出到任何支持的数据源。

> [!IMPORTANT]
> 本主题仅介绍如何 **启动** 向导。 如果你正在寻找其他事情，请参阅[相关的任务和内容](#related)。

你可以启动向导：
-   如果要将向导导入或导出任何支持的数据源，可使用 [“开始”菜单](#startStart)。
-   如果要将向导导入或导出任何支持的数据源，可使用 [命令提示符](#startCmd)。 
-   如果要将向导导入或导出 SQL Server，可使用 [SQL Server Management Studio (SSMS)](#startSSMS)。
-   如果要将向导导入或导出 SQL Server，可使用 [具有 SQL Server Data Tools (SSDT) 的 Visual Studio](#startVS)。

## <a name="prerequisite---is-the-wizard-installed-on-your-computer"></a>系统必备组件的是在计算机上安装向导？
如果想要运行向导，但是尚未在计算机上安装 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，则可以通过安装 SQL Server Data Tools (SSDT) 来安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导。 有关详细信息，请参阅 [下载 SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx)。

> [!NOTE]
> 若要使用 64 位版本的 SQL Server 导入和导出向导，你必须安装 SQL Server。 SQL Server Data Tools (SSDT) 和 SQL Server Management Studio (SSMS) 是 32 位应用程序，仅安装 32 位文件，包括 32 位版本的向导。

## <a name="startStart"></a> “开始”菜单  
### <a name="start-the-sql-server-import-and-export-wizard-from-the-start-menu"></a>从开始菜单启动 SQL Server 导入和导出向导
1.  上**启动**菜单上，找到并展开**Microsoft SQL Server 2016**。
3.  单击以下选项之一。
  
    -   **SQL Server 2016 导入和导出数据(64 位)**
          
    -   **SQL Server 2016 导入和导出数据(32 位)**  
  
    运行 64 位版本的向导，除非你知道数据源需要 32 位数据访问接口。
 
    ![启动向导“开始”](../../integration-services/import-export-data/media/start-wizard-start.jpg)
  
## <a name="startCmd"></a> Command prompt
### <a name="start-the-sql-server-import-and-export-wizard-from-the-command-prompt"></a>从命令提示符下启动 SQL Server 导入和导出向导  
在命令提示符窗口中，从以下位置之一运行 **DTSWizard.exe** 。  
  
-   **C:\Program Files\Microsoft SQL Server\130\DTS\Binn** （对于 64 位版本）。  
  
-   **C:\Program Files (x86)\Microsoft SQL Server\130\DTS\Binn** （对于 32 位版本）。  
  
运行 64 位版本的向导，除非你知道数据源需要 32 位数据访问接口。

![启动向导 cmd](../../integration-services/import-export-data/media/start-wizard-cmd.jpg)  
  
## <a name="startSSMS"></a> SQL Server Management Studio (SSMS)
### <a name="start-the-sql-server-import-and-export-wizard-from-sql-server-management-studio-ssms"></a>从 SQL Server Management Studio (SSMS) 中启动 SQL Server 导入和导出向导    
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例。
    
2.  展开“数据库”。
3.  右键单击某个数据库。
4.  指向“任务” 。
5.  单击以下选项之一。
  
    -   **导入数据**
      
    -   **导出数据**  

    ![启动向导 SSMS](../../integration-services/import-export-data/media/start-wizard-ssms.jpg) 

如果尚未安装 SQL Server，或已具有 SQL Server 但未安装 SQL Server Management Studio，请参阅[下载 SQL Server Management Studio (SSMS)](../../ssms/download-sql-server-management-studio-ssms.md)。
  
## <a name="startVS"></a>Visual Studio
### <a name="start-the-sql-server-import-and-export-wizard-from-visual-studio-with-sql-server-data-tools-ssdt"></a>从 SQL Server Data Tools (SSDT) 与 Visual Studio 启动 SQL Server 导入和导出向导 
 在具有 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]的 Visual Studio 中，在 Integration Services 项目打开的情况下，执行以下列操作之一。 
  
-   在“项目”  菜单上，单击“SSIS 导入和导出向导” 。 

    ![启动向导项目](../../integration-services/import-export-data/media/start-wizard-project.jpg) 
    
    \- 或 -
    
-   在解决方案资源管理器中，右键单击“SSIS 包”  文件夹，再单击“SSIS 导入和导出向导” 。

    ![启动向导包](../../integration-services/import-export-data/media/start-wizard-packages.jpg)

如果尚未安装 Visual Studio，或已具有 Visual Studio 但未安装 SQL Server Data Tools，请参阅[下载 SQL Server Data Tools (SSDT)](../../ssdt/download-sql-server-data-tools-ssdt.md)。

## <a name="get-the-wizard"></a>获得向导
如果想要运行向导，但是尚未在计算机上安装 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，则可以通过安装 SQL Server Data Tools (SSDT) 来安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导。 有关详细信息，请参阅 [下载 SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx)。

## <a name="get-help-while-the-wizard-is-running"></a>在向导运行期间获得帮助
> [!TIP]
> 从向导的任何页面或对话框中点击 F1 键，可查看当前页的相关文档。   

 ## <a name="whats-next"></a>下一步是什么？  
 当你启动向导时，第一页是“欢迎使用 SQL Server 导入和导出向导” 。 不必在此页上执行任何操作。 有关详细信息，请参阅 [欢迎使用 SQL Server 导入和导出向导](../../integration-services/import-export-data/welcome-to-sql-server-import-and-export-wizard.md)。  
  
## <a name="related"></a>相关的任务和内容  
 以下是一些其他基本任务。
-   **请参阅快速示例说明在向导的工作原理。**

    -   **如果想要查看屏幕快照。** 在一页-看一看这个简单的端到端示例[开始导入和导出向导的这个简单的示例使用](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)。

    -   **如果你更愿意观看视频。** 观看此四分钟的视频演示向导并清楚地说明的 YouTube、 只需如何将数据导出到 Excel-[使用 SQL Server 导入和导出向导导出到 Excel](https://go.microsoft.com/fwlink/?linkid=829049)。

-   **了解有关该向导的工作原理的详细信息。**

    -   **了解有关该向导的详细信息。** 如果正在寻找有关该向导的概述，请参阅 [使用 SQL Server 导入和导出向导来导入和导出数据](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)。

    -   **了解有关向导中的步骤。** 如果你正在寻找有关向导中的步骤的信息，请参阅[的 SQL Server 导入和导出向导中的步骤](../../integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard.md)。 此外没有单独的页的向导的每一页的文档。

    -   **了解如何连接到数据源和目标。** 如果你正在寻找有关如何连接到你的数据的信息，从此处的列表中选择所需的页[连接到数据源的 SQL Server 导入和导出向导](../../integration-services/import-export-data/connect-to-data-sources-with-the-sql-server-import-and-export-wizard.md)。 没有单独的几个常用的数据源的每个文档的页面。



