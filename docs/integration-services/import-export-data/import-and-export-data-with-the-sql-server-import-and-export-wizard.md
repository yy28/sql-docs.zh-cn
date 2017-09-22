---
title: "导入和导出数据与 SQL Server 导入和导出向导 |Microsoft 文档"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- exporting data
- mapping files [Integration Services]
- SQL Server Import and Export Wizard
- SSIS packages, creating
- packages [Integration Services], copying
- Integration Services packages, creating
- packages [Integration Services], creating
- SQL Server Integration Services packages, creating
- Import and Export Wizard
- copying data [Integration Services]
- importing data, SSIS packages
- sources [Integration Services], copying data
ms.assetid: c0e4d867-b2a9-4b2a-844b-2fe45be88f81
caps.latest.revision: 160
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: a6aeda8e785fcaabef253a8256b5f6f7a842a324
ms.openlocfilehash: 58908fc8a7b18cff36a41ee26e7a3eab8e84a5d0
ms.contentlocale: zh-cn
ms.lasthandoff: 09/21/2017

---
# <a name="import-and-export-data-with-the-sql-server-import-and-export-wizard"></a>使用 SQL Server 导入和导出向导导入和导出数据

 > 与以前版本的 SQL Server 相关的内容，请参阅[运行 SQL Server 导入和导出向导](https://msdn.microsoft.com/en-US/library/ms140052(SQL.120).aspx)。

 利用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导，可轻松将数据从源复制到目标。 本概述介绍该向导可以将源和目标，用作数据源，以及你要运行该向导所需的权限。

## <a name="get-the-wizard"></a>获得向导
如果你想要运行向导，但不会获得 [！包括[msCoName](/sql-docs/docs/ssdt/download-sql-server-data-tools-ssdt)。

## <a name="what-happens-when-i-run-the-wizard"></a>在运行向导时，会发生什么情况？
-    **请参阅步骤的列表。** 有关向导中的步骤的说明，请参阅[的 SQL Server 导入和导出向导中的步骤](../../integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard.md)。 此外没有单独的页的向导的每一页的文档。  
    \-或\-
-   **请参阅一个简单的示例。** 快速查看你在典型的会话中看到多个屏幕，看一看这个简单的端到端示例在一页-[开始导入和导出向导的这个简单的示例使用](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)。  

##  <a name="wizardSources"></a>我可以使用哪些源和目标？  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]导入和导出向导可以将数据复制到和从下表中列出的数据源。 若要连接到的某些这些数据源，你可能必须下载并安装其他文件。
 
| 数据源 | 是否必须下载其他文件？ |
|-------------|-----------------------------------------|
|**企业数据库**<br/>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Oracle、 DB2，及其他类型。|SQL Server 或 SQL Server Data Tools (SSDT) 安装文件，你需要连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 但 SSDT 不安装需要连接到其他企业数据库，例如 Oracle 或 IBM DB2 的所有文件。<br/><br/>若要连接到企业数据库，你通常需要具有以下两项操作：<br/><br/>1.**客户端软件**。 如果已经为企业数据库系统安装了客户端软件，则通常会有建立连接所需的文件。 如果尚未安装客户端软件，请询问数据库管理员如何安装获得许可的副本。<br/><br/>2.**驱动程序或提供程序**。 Microsoft 安装驱动程序和提供程序连接到 Oracle。 要连接到 IBM DB2，获取 Microsoft® OLEDB Provider for DB2 5.0 版 for Microsoft SQL Server 从[Microsoft SQL Server 2016 功能包](https://www.microsoft.com/download/details.aspx?id=52676)。|
|**文本文件**（平面文件）|无需任何其他文件。|
|**Microsoft Excel 和 Microsoft Access 文件**|Microsoft Office 并不会安装连接到作为数据源的 Excel 和 Access 文件所需的所有文件。 获取以下下载- [Microsoft Access 数据库引擎 2016年可再发行组件](https://www.microsoft.com/download/details.aspx?id=54920)。<br/><br/>有关详细信息，请参阅[连接到 Excel 数据源](../../integration-services/import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md)或[连接到 Access 数据源](../../integration-services/import-export-data/connect-to-an-access-data-source-sql-server-import-and-export-wizard.md)。|
|**Azure 数据源**<br/>目前仅限 Azure Blob 存储。|SQL Server Data Tools 不安装你需要连接到 Azure Blob 存储作为数据源的文件。 获取以下下载 — [用于 Azure 的 Microsoft SQL Server 2016 Integration Services 功能包](https://www.microsoft.com/download/details.aspx?id=49492)。<br/><br/>有关详细信息，请参阅[连接到 Azure Blog 存储](../../integration-services/import-export-data/connect-to-azure-blob-storage-sql-server-import-and-export-wizard.md)。|
|**打开源数据库**<br/>PostgreSQL、 MySql 和其他人。|必须下载其他文件才能连接到这些数据源。<br/><br/>-为**PostgreSQL**，请参阅[连接 PostgreSQL 数据源](../../integration-services/import-export-data/connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard.md)。<br/>-为**MySql**，请参阅[连接到 MySQL 数据源](../../integration-services/import-export-data/connect-to-a-mysql-data-source-sql-server-import-and-export-wizard.md)。|
|**为其任何其他数据源驱动程序或提供商时可用**|通常必须下载其他文件才能连接到以下类型的数据源。<br/><br/>- 提供 **ODBC 驱动程序** 的任何源。 有关详细信息，请参阅[连接到 ODBC 数据源](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)。<br/>- 提供 **.Net Framework 数据提供程序** 的任何源。<br/>- 提供 **OLE DB 提供程序** 的任何源。<br/><br/>对于其他数据源提供源和目标的功能的第三方组件是有时销售作为附加产品的 SQL Server Integration Services (SSIS)。|

## <a name="how-do-i-connect-to-my-data"></a>如何连接到我的数据？
有关如何连接到常用的数据源的信息，请参阅以下页面之一。
-   [连接到 SQL Server](../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md)
-   [连接到 Oracle](../../integration-services/import-export-data/connect-to-an-oracle-data-source-sql-server-import-and-export-wizard.md)
-   [连接到平面文件 （文本文件）](../../integration-services/import-export-data/connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard.md)
-   [连接到 Excel](../../integration-services/import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md)
-   [连接到 Access](../../integration-services/import-export-data/connect-to-an-access-data-source-sql-server-import-and-export-wizard.md)
-   [连接到 Azure Blob 存储](../../integration-services/import-export-data/connect-to-azure-blob-storage-sql-server-import-and-export-wizard.md)
-   [使用 ODBC 连接](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)
-   [连接到 PostgreSQL](../../integration-services/import-export-data/connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard.md)
-   [连接到 MySQL](../../integration-services/import-export-data/connect-to-a-mysql-data-source-sql-server-import-and-export-wizard.md)


有关如何连接到未在此处列出的数据源的信息，请参阅[该连接字符串引用](https://www.connectionstrings.com/)。 此第三方站点包含示例连接字符串以及有关数据提供程序的详细信息和它们需要的连接信息。

## <a name="what-permissions-do-i-need"></a>我需要什么权限？  
 若要成功运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导，必须至少具有下列权限。 如果已使用数据源和目标，则可能已具有所需的权限。
  
|执行这些操作时需要权限|如果您正在连接到 SQL Server，则需要这些特定的权限 |  
|-------------------------|----------------------------------------------------|  
|连接到源数据库和目标数据库或文件共享。|服务器和数据库的登录权限。|  
|从源数据库或文件中导出或读取数据。|对源表和源视图具有 SELECT 权限。|  
|向目标数据库或文件导入或写入数据。|对目标表具有 INSERT 权限。|  
|创建目标数据库或文件（如果适用）。|CREATE DATABASE 或 CREATE TABLE 权限。|  
|保存向导创建的 SSIS 包（如果适用）。|如果要将包保存到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，需要有将包保存到 **msdb** 数据库的权限。|  
  
## <a name="get-help-while-the-wizard-is-running"></a>在向导运行期间获得帮助
> [!TIP]
> 从向导的任何页面或对话框中点击 F1 键，可查看当前页的相关文档。   
  
##  <a name="wizardSSIS"></a> 向导使用 SQL Server Integration Services (SSIS)  
 向导使用 SQL Server Integration Services (SSIS) 复制数据。 SSIS 是一种用于提取、转换和加载数据 (ETL) 的工具。 向导页面会使用某些 SSIS 语言。
  
 在 SSIS 中，基本单位是 **包**。 当你在向导的各个页面之间移动并指定选项时，向导会在内存中创建 SSIS 包。    
  
如果安装了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 标准版或更高版本，那么在向导结束时，可以选择保存 SSIS 包。 之后可以重新使用包，或者通过使用 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器添加任务、转换和事件驱动逻辑来扩展包。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导为创建从源向目标复制数据的基本 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包提供了最简便的方法。

有关 SSIS 的详细信息，请参阅 [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)。

## <a name="whats-next"></a>下一步是什么？  
 启动向导。 有关详细信息，请参阅 [启动 SQL Server 导入和导出向导](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md)。  

## <a name="see-also"></a>另请参阅
[导入和导出向导的简单示例入门](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)  
[SQL Server 导入和导出向导中的数据类型映射](../../integration-services/import-export-data/data-type-mapping-in-the-sql-server-import-and-export-wizard.md)



