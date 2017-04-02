---
title: "连接到 Excel 工作簿 | Microsoft Docs"
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Excel [Integration Services]"
ms.assetid: d9746318-3669-4ce2-bbb0-4a1bd471c9dd
caps.latest.revision: 22
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 22
---
# 连接到 Excel 工作簿
  若要将 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包连接到 Microsoft Office Excel 工作簿，需要 Excel 连接管理器。  
  
 您可以从 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器的“连接管理器”区域或从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导，创建这些连接管理器。  
  
 **Microsoft Excel 和 Access 文件的提供程序和驱动程序**  
  
 你可能需要下载 Microsoft Office 文件的的 OLE DB 提供程序和驱动程序（如果它们尚未安装）。 更高版本的提供程序可以打开 Excel 的早期版本所创建的文件。  
  
 如果计算机有 32 位版本的 Office，则必须安装 32 位版本的驱动程序，并且你还必须确保运行向导或它在 32 位模式下创建的 Integration Services 包。  
  
|Microsoft Office 版本|下载|  
|------------------------------|--------------|  
|2007|[2007 Office System Driver: Data Connectivity Components（Office 2007 系统驱动程序：数据连接组件）](https://www.microsoft.com/en-us/download/details.aspx?id=23734)|  
|2010|[Microsoft Access 2010 Runtime](https://www.microsoft.com/en-us/download/details.aspx?id=10910)|  
|2013|[Microsoft Access 2013 Runtime](http://www.microsoft.com/en-us/download/details.aspx?id=39358)|  
  
### 从“连接管理器”区域创建 Excel 连接管理器  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开该包。  
  
2.  在“连接管理器”区域中，右键单击该区域中的任意位置，然后选择“新建连接”。  
  
3.  在 **“添加 SSIS 连接管理器”** 对话框中，选择 **Excel**，然后配置该连接管理器。  
  
     有关适用于此连接管理器的配置选项的信息，请参阅 [Excel Connection Manager Editor](../../integration-services/connection-manager/excel-connection-manager-editor.md)。  
  
### 从 SQL Server 导入和导出向导创建 Excel 连接  
  
1.  启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导的 32 位版本。  
  
2.  在 **“选择数据源”** 页上，选择 **Microsoft Excel**作为 **“数据源”**，然后配置该 Excel 连接。  
  
     有关适用于此连接类型的配置选项的信息，请参阅 [Excel Connection Manager Editor](../../integration-services/connection-manager/excel-connection-manager-editor.md)。  
  
## 另请参阅  
 [连接到 Access 数据库](../../integration-services/connection-manager/connect-to-an-access-database.md)  
  
  