---
title: 启动 SQL Server 导入和导出向导 | Microsoft Docs
ms.custom: ''
ms.date: 06/20/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Import and Export Wizard
- starting SQL Server Import and Export Wizard
- Import and Export Wizard
- starting Import and Export Wizard
ms.assetid: 5fc4f6d1-1f6f-444e-9aeb-827f85e1c405
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8db11de67db871df75605099191a2ae0e34be0b9
ms.sourcegitcommit: a13256f484eee2f52c812646cc989eb0ce6cf6aa
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/25/2019
ms.locfileid: "56801331"
---
# <a name="start-the-sql-server-import-and-export-wizard"></a>启动 SQL Server 导入和导出向导


用本主题中介绍的其中一种方式启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导，从支持的任何数据源导入数据和从其中导出数据。

> [!IMPORTANT]
> 本主题仅介绍如何 **启动** 向导。 如需其他信息，请参阅[相关任务和内容](#related)。

可以启动向导：
-   如果要将向导导入或导出任何支持的数据源，可使用 [“开始”菜单](#startStart)。
-   如果要将向导导入或导出任何支持的数据源，可使用 [命令提示符](#startCmd)。 
-   如果要将向导导入或导出 SQL Server，可使用 [SQL Server Management Studio (SSMS)](#startSSMS)。
-   如果要将向导导入或导出 SQL Server，可使用 [具有 SQL Server Data Tools (SSDT) 的 Visual Studio](#startVS)。

## <a name="prerequisite---is-the-wizard-installed-on-your-computer"></a>先决条件 — 计算机上是否安装了向导？
如果想要运行向导，但是尚未在计算机上安装 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，则可以通过安装 SQL Server Data Tools (SSDT) 来安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导。 有关详细信息，请参阅 [下载 SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx)。

> [!NOTE]
> 若要使用 64 位版本的 SQL Server 导入和导出向导，必须安装 SQL Server。 SQL Server Data Tools (SSDT) 和 SQL Server Management Studio (SSMS) 是 32 位应用程序且仅安装 32 位文件，包括 32 位版本的向导。

## <a name="startStart"></a> “开始”菜单  
### <a name="start-the-sql-server-import-and-export-wizard-from-the-start-menu"></a>从“开始”菜单启动 SQL Server 导入和导出向导
1.  在“开始”菜单上，查找和展开“Microsoft SQL Server 2016”。
3.  单击以下选项之一。
  
    -   **SQL Server 2016 导入和导出数据(64 位)**
          
    -   **SQL Server 2016 导入和导出数据(32 位)**  
  
    运行 64 位版本的向导，除非你知道数据源需要 32 位数据访问接口。
 
    ![启动向导“开始”](../../integration-services/import-export-data/media/start-wizard-start.jpg)
  
## <a name="startCmd"></a> Command prompt
### <a name="start-the-sql-server-import-and-export-wizard-from-the-command-prompt"></a>从命令提示符启动 SQL Server 导入和导出向导  
在命令提示符窗口中，从以下位置之一运行 **DTSWizard.exe** 。  
  
-   **C:\Program Files\Microsoft SQL Server\130\DTS\Binn** （对于 64 位版本）。  
  
-   **C:\Program Files (x86)\Microsoft SQL Server\130\DTS\Binn** （对于 32 位版本）。  
  
运行 64 位版本的向导，除非你知道数据源需要 32 位数据访问接口。

![启动向导 cmd](../../integration-services/import-export-data/media/start-wizard-cmd.jpg)  
  
## <a name="startSSMS"></a> SQL Server Management Studio (SSMS)
### <a name="start-the-sql-server-import-and-export-wizard-from-sql-server-management-studio-ssms"></a>从 SQL Server Management Studio (SSMS) 启动 SQL Server 导入和导出向导    
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例。
    
2.  展开“数据库”。
3.  右键单击某个数据库。
4.  指向“任务” 。
5.  单击以下选项之一。
  
    -   **导入数据**
      
    -   **导出数据**  

    ![启动向导 SSMS](../../integration-services/import-export-data/media/start-wizard-ssms.jpg) 

如果尚未安装 SQL Server，或已具有 SQL Server 但未安装 SQL Server Management Studio，请参阅 [下载 SQL Server Management Studio (SSMS)](../../ssms/download-sql-server-management-studio-ssms.md)。
  
## <a name="startVS"></a> Visual Studio
### <a name="start-the-sql-server-import-and-export-wizard-from-visual-studio-with-sql-server-data-tools-ssdt"></a>从具有 SQL Server Data Tools (SSDT) 的 Visual Studio 启动 SQL Server 导入和导出向导 
 在具有 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]的 Visual Studio 中，在 Integration Services 项目打开的情况下，执行以下列操作之一。 
  
-   在“项目”  菜单上，单击“SSIS 导入和导出向导” 。 

    ![启动向导项目](../../integration-services/import-export-data/media/start-wizard-project.jpg) 
    
    \- 或 -
    
-   在解决方案资源管理器中，右键单击“SSIS 包”  文件夹，再单击“SSIS 导入和导出向导” 。

    ![启动向导包](../../integration-services/import-export-data/media/start-wizard-packages.jpg)

如果尚未安装 Visual Studio，或已具有 Visual Studio 但未安装 SQL Server Data Tools，请参阅 [下载 SQL Server Data Tools (SSDT)](../../ssdt/download-sql-server-data-tools-ssdt.md)。

## <a name="get-the-wizard"></a>获取向导
如果想要运行向导，但是尚未在计算机上安装 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，则可以通过安装 SQL Server Data Tools (SSDT) 来安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导。 有关详细信息，请参阅 [下载 SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx)。

## <a name="get-help-while-the-wizard-is-running"></a>在向导运行期间获得帮助
> [!TIP]
> 从向导的任何页面或对话框中点击 F1 键，可查看当前页的相关文档。   

 ## <a name="whats-next"></a>下一步是什么？  
 当你启动向导时，第一页是“欢迎使用 SQL Server 导入和导出向导” 。 不必在此页上执行任何操作。 有关详细信息，请参阅 [欢迎使用 SQL Server 导入和导出向导](../../integration-services/import-export-data/welcome-to-sql-server-import-and-export-wizard.md)。  
  
## <a name="related"></a>相关任务和内容  
 以下是一些其他的基本任务。
-   **查看有关向导工作原理的简短示例。**

    -   **如果想查看屏幕快照。** 查看此仅占用一页的简单端对端示例 — [开始使用这一简单的导入和导出向导示例](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)。

    -   **如果想观看视频。** 观看这个来自 YouTube 的四分钟视频，该视频演示了此向导，并清晰简明地说明了将数据导出到 Excel 的方法：[使用 SQL Server 导入和导出向导导出到 Excel](https://go.microsoft.com/fwlink/?linkid=829049)。

-   **了解有关向导工作原理的详细信息。**

    -   **了解有关向导的详细信息。** 如果正在寻找有关该向导的概述，请参阅 [使用 SQL Server 导入和导出向导来导入和导出数据](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)。

    -   **了解有关向导中的步骤的信息。** 如需有关向导中的各个步骤的信息，请参阅 [SQL Server 导入和导出向导中的步骤](../../integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard.md)。 还为向导的每一页专门设有一页文档信息页。

    -   **了解如何连接到数据源和目标。** 如需有关如何连接到数据的信息，请从此处列表中选择所需的页面：[使用 SQL Server 导入和导出向导连接到数据源](../../integration-services/import-export-data/connect-to-data-sources-with-the-sql-server-import-and-export-wizard.md)。 其中为几个常用数据源中的每一个数据源专门设有一页文档信息页。


