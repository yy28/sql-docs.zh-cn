---
title: "使用 SQL Server 导入和导出向导导入和导出数据 | Microsoft Docs"
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
  - "导出数据"
  - "映射文件 [Integration Services]"
  - "SQL Server 导入和导出向导"
  - "SSIS 包，创建"
  - "包 [Integration Services]，复制"
  - "Integration Services 包，创建"
  - "包 [Integration Services]，创建"
  - "SQL Server Integration Services 包，创建"
  - "导入和导出向导"
  - "复制数据 [Integration Services]"
  - "导入数据，SSIS 包"
  - "源 [Integration Services]，复制数据"
ms.assetid: c0e4d867-b2a9-4b2a-844b-2fe45be88f81
caps.latest.revision: 160
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 134
---
# 使用 SQL Server 导入和导出向导导入和导出数据
 利用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导，可轻松将数据从源复制到目标。 不必安装 SQL Server 即可运行此向导。 本概述介绍可使用此向导从其中导出数据或向其导入数据的数据源，以及运行该向导所需的权限。

本主题仅提供向导的**概述**。
-   如果已准备好运行向导，并且只想知道如何启动向导，请参阅[启动 SQL Server 导入和导出向导](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md)。
-   如果正在寻找有关向导中的步骤的信息，请在内容导航菜单中选择所需的页面。 有一个单独页是关于向导的各个页的文档信息。 从向导的任何页面或对话框中点击 F1，可查看当前页的相关文档。

**获取向导。** 如果想要运行向导，但是尚未在计算机上安装 [!INCLUDE[msCoName] (../Token/msCoName_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，则可以通过安装 SQL Server Data Tools (SSDT) 来安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导。 有关详细信息，请参阅[下载 SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx)。

> [!TIP] 如果必须复制多个数据库或数据库对象（而非表和视图），请使用复制数据库向导，而不是使用导入和导出向导。 有关详细信息，请参阅[使用复制数据库向导](../../relational-databases/databases/use-the-copy-database-wizard.md)。

## <a name="example-of-a-common-use-case---exporting-data-to-excel-video"></a>常见用例示例 - 将数据导出到 Excel（视频）  
该向导的常见用途之一是将数据导出到 Excel。 以下是来自 YouTube 的一个四分钟视频，该视频通过清晰、简单的说明演示了该向导，并介绍了执行此操作的方法：[Using the SQL Server Import and Export Wizard to Export to Excel](https://go.microsoft.com/fwlink/?linkid=829049)（使用 SQL Server 导入和导出向导导出到 Excel）

##  <a name="a-namewizardsourcesa-what-data-sources-and-destinations-can-i-use"></a><a name="wizardSources"></a>我可以使用哪些数据源和目标？  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导可以将数据复制到以下数据源以及从中复制数据。 若要使用其中某些数据源，可能需要下载并安装其他文件。

| 数据源 | 是否必须下载其他文件？ |
|-------------|-----------------------------------------|
|**企业数据库**<br/>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、Oracle 等等。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 会安装连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Oracle 所需的文件，但不会安装连接到 IBM DB2 或 Informix 等其他企业数据库所需的文件。<br/>- 如果已经为企业数据库系统安装了客户端软件，则通常会有建立连接所需的文件。<br/>- 如果尚未安装客户端软件，请询问数据库管理员如何安装获得许可的副本。|
|**打开源数据库**<br/>MySql、PostgreSQL、SQLite 等等。|必须下载其他文件才能连接到这些数据源。<br/><br/>- 对于 **MySql**，请参阅 [MySQL Connectors](http://dev.mysql.com/downloads/connector/)（MySQL 连接器）。<br/>- 对于 **PostgreSQL**，请参阅 [psqlODBC - PostgreSQL ODBC driver](https://odbc.postgresql.org/)（psqlODBC - PostgreSQL ODBC 驱动程序）和第三方产品（如 [Npgsql - 用于 PostgreSQL 的 .NET 数据提供程序](http://www.npgsql.org/)）。<br/>- 对于 **SQLite**，请从在线提供的多个开源提供程序和驱动程序中进行选择。|
|**文本文件**（平面文件）。|无需任何其他文件。|
|**Microsoft Excel 和 Microsoft Access 文件**|Microsoft Office 并不会安装连接到作为数据源的 Excel 和 Access 文件所需的所有文件。 获取以下下载 — [Microsoft Access 2016 Runtime](https://www.microsoft.com/download/details.aspx?id=50040)。|
|**Azure 数据源**<br/>目前仅限 Azure Blob 存储。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不会安装连接到作为数据源的 Azure Blob 存储所需的文件。 获取以下下载 — [用于 Azure 的 Microsoft SQL Server 2016 Integration Services 功能包](https://www.microsoft.com/download/details.aspx?id=49492)。|
|**提供连接器的任何其他数据源**。|通常必须下载其他文件才能连接到以下类型的数据源。<br/><br/>- 提供 **ODBC 驱动程序**的任何源。 建立 ODBC（开放式数据库连接）连接，方法如下：在向导的“选择数据源”或“选择目标”页上选择用于 Odbc 的 .Net Framework 提供程序，然后提供一个连接字符串或一个引用 ODBC 驱动程序的现有 DSN（数据源名称）。<br/>- 提供 **OLE DB 提供程序**的任何源。<br/>- 提供 **.Net Framework 数据提供程序**的任何源。<br/>- 由**第三方组件**提供源和目标功能的其他数据源。 这些第三方产品通常作为 SQL Server Integration Services (SSIS) 的附加产品销售。|
  
> [!TIP] 如果数据源需要连接字符串，可以在第三方站点 [The Connection Strings Reference](https://www.connectionstrings.com/)（连接字符串参考）上查找示例。  
  
## <a name="what-permissions-do-i-need-to-run-the-wizard"></a>需要哪些权限才能运行向导？  
 若要成功运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导，必须至少具有下列权限。 如果已使用数据源和目标，则可能已具有所需的权限。
  
|执行这些操作时需要权限|如果要连接到 SQL Server，则需要这些权限 |  
|-------------------------|----------------------------------------------------|  
|连接到源数据库和目标数据库或文件共享。|服务器和数据库的登录权限。|  
|从源数据库或文件中导出或读取数据。|对源表和源视图具有 SELECT 权限。|  
|向目标数据库或文件导入或写入数据。|对目标表具有 INSERT 权限。|  
|创建目标数据库或文件（如果适用）。|CREATE DATABASE 或 CREATE TABLE 权限。|  
|保存向导创建的 SSIS 包（如果适用）。|如果要将包保存到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，需要有将包保存到 **msdb** 数据库的权限。|  
  
##  <a name="a-namewizardssisa-the-wizard-uses-sql-server-integration-services-ssis"></a><a name="wizardSSIS"></a>向导使用 SQL Server Integration Services (SSIS)  
 向导使用 SQL Server Integration Services (SSIS) 复制数据。 SSIS 是一种用于提取、转换和加载数据 (ETL) 的工具。 向导页面会使用某些 SSIS 语言。
  
 在 SSIS 中，基本单位是**包**。 当你在向导的各个页面之间移动并指定选项时，向导会在内存中创建 SSIS 包。    
  
如果安装了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 标准版或更高版本，那么在向导结束时，可以选择保存 SSIS 包。 之后可以重新使用包，或者通过使用 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器添加任务、转换和事件驱动逻辑来扩展包。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导为创建从源向目标复制数据的基本 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包提供了最简便的方法。

有关 SSIS 的详细信息，请参阅 [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)。

## <a name="get-help-while-the-wizard-is-running"></a>在向导运行期间获得帮助
> [!TIP] 从向导的任何页面或对话框中点击 F1 键，可查看当前页的相关文档。   
  
## <a name="whats-next"></a>下一步是什么？  
 启动向导。 有关详细信息，请参阅[启动 SQL Server 导入和导出向导](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md)。  
  
## <a name="see-also"></a>另请参阅
[SQL Server 导入和导出向导中的数据类型映射](../../integration-services/import-export-data/data-type-mapping-in-the-sql-server-import-and-export-wizard.md)
