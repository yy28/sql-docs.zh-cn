---
title: "Start the SQL Server Import and Export Wizard | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "SQL Server 导入和导出向导"
  - "启动 SQL Server 导入和导出向导"
  - "导入和导出向导"
  - "开始导入和导出向导"
ms.assetid: 5fc4f6d1-1f6f-444e-9aeb-827f85e1c405
caps.latest.revision: 130
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 112
---
# Start the SQL Server Import and Export Wizard
可使用以下一种方法启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导。
-   如果要将向导导入或导出任何支持的数据源，可使用[“开始”菜单](#startStart)或[命令提示符](#startCmd)。
-   如果要将向导导入或导出 SQL Server，可使用 [SQL Server Management Studio (SSMS)](#startSSMS)。
-   如果已打开一个 SQL Server Integration Services 项目，可使用[具有 SQL Server Data Tools (SSDT) 的 Visual Studio](#startVS)。

本主题仅介绍如何**启动**向导。
-   如果正在寻找有关该向导的概述，请参阅[使用 SQL Server 导入和导出向导来导入和导出数据](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)。
-   如果正在寻找有关向导中的步骤的信息，请在内容导航菜单中选择所需的页面。 有一个单独页是关于向导的各个页的文档信息。 从向导的任何页面或对话框中点击 F1，可查看当前页的相关文档。

**获取向导。** 如果想要运行向导，但是尚未在计算机上安装 [!INCLUDE[msCoName] (../Token/msCoName_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，则可以通过安装 SQL Server Data Tools (SSDT) 来安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导。 有关详细信息，请参阅[下载 SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx)。  

## <a name="a-namestartstarta-start-the-wizard-from-the-start-menu"></a><a name="startStart"></a>从“开始”菜单启动向导  
1.  在“开始”菜单上，单击“所有应用”。
2.  找到并展开“Microsoft SQL Server 2016”。
3.  单击以下选项之一。
  
    -   **SQL Server 2016 导入和导出数据(64 位)**
          
    -   **SQL Server 2016 导入和导出数据(32 位)**  
  
运行 64 位版本的向导，除非你知道数据源需要 32 位数据访问接口。
 
![启动向导“开始”](../../integration-services/import-export-data/media/start-wizard-start.jpg)
  
## <a name="a-namestartcmda-start-the-wizard-from-the-command-prompt"></a><a name="startCmd"></a>从命令提示符启动向导  
在命令提示符窗口中，从以下位置之一运行 **DTSWizard.exe**。  
  
-   **C:\Program Files\Microsoft SQL Server\130\DTS\Binn**（对于 64 位版本）。  
  
-   **C:\Program Files (x86)\Microsoft SQL Server\130\DTS\Binn**（对于 32 位版本）。  
  
运行 64 位版本的向导，除非你知道数据源需要 32 位数据访问接口。

![启动向导 cmd](../../integration-services/import-export-data/media/start-wizard-cmd.jpg)  
  
## <a name="a-namestartssmsa-start-the-wizard-from-sql-server-management-studio-ssms"></a><a name="startSSMS"></a>从 SQL Server Management Studio (SSMS) 启动向导  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的实例。
2.  展开“数据库”。
3.  右键单击某个数据库。
4.  指向“任务”。
5.  单击以下选项之一。
  
    -   **导入数据**
      
    -   **导出数据**  

![启动向导 SSMS](../../integration-services/import-export-data/media/start-wizard-ssms.jpg) 

如果尚未安装 SQL Server，或已具有 SQL Server 但未安装 SQL Server Management Studio，请参阅[下载 SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx)。
    
## <a name="a-namestartvsa-start-the-wizard-from-visual-studio-with-sql-server-data-tools-ssdt"></a><a name="startVS"></a>从具有 SQL Server Data Tools (SSDT) 的 Visual Studio 启动向导  
 在具有 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 的 Visual Studio 中，在 Integration Services 项目打开的情况下，执行以下列操作之一。  
  
-   在“项目”菜单上，单击“SSIS 导入和导出向导”。 

    ![启动向导项目](../../integration-services/import-export-data/media/start-wizard-project.jpg) 
    
    \- 或 -
    
-   在解决方案资源管理器中，右键单击“SSIS 包”文件夹，再单击“SSIS 导入和导出向导”。

    ![启动向导包](../../integration-services/import-export-data/media/start-wizard-packages.jpg)

如果尚未安装 Visual Studio，或已具有 Visual Studio 但未安装 SQL Server Data Tools，请参阅[下载 SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx)。 

## <a name="get-help-while-the-wizard-is-running"></a>在向导运行期间获得帮助
> [!TIP] 从向导的任何页面或对话框中点击 F1 键，可查看当前页的相关文档。   

 ## <a name="whats-next"></a>下一步是什么？  
 当你启动向导时，第一页是“欢迎使用 SQL Server 导入和导出向导”。 不必在此页上执行任何操作。 有关详细信息，请参阅[欢迎使用 SQL Server 导入和导出向导](../../integration-services/import-export-data/welcome-to-sql-server-import-and-export-wizard.md)。  
  
  