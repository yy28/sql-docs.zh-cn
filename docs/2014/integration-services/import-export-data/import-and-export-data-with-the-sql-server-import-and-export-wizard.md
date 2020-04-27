---
title: SQL Server 导入和导出向导 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
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
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2f3ce90e2670357d0842b0a6ac7838f396465bab
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62768159"
---
# <a name="sql-server-import-and-export-wizard"></a>SQL Server 导入和导出向导
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]导入和导出向导提供了最简单的方法， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]可用于创建将数据从源复制到目标的包。  
  
> [!NOTE]  
>  在 64 位计算机上，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 会安装 64 位版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导 (DTSWizard.exe)。 但是，有些数据源（如 Access 或 Excel）只提供 32 位提供程序。 若要使用这些数据源，您可能需要安装并运行 32 位版本的向导。 若要安装 32 位版本的向导，必须在安装过程中选择“客户端工具”或 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]。  
  
 可以从“开始”菜单、从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、从 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或使用命令提示符启动 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 导入和导出向导。 有关详细信息，请参阅[运行 SQL Server 导入和导出向导](start-the-sql-server-import-and-export-wizard.md)。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导可以将数据复制到提供托管 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 数据访问接口或本机 OLE DB 访问接口的任何数据源，也可以从这些数据源复制数据。 可用访问接口的列表包括下列数据源：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   平面文件  
  
-   Microsoft Office Access  
  
-   Microsoft Office Excel  
  
 启动向导的环境不同，某些向导功能的工作方式也会有所不同：  
  
-   如果在中[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]启动[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]导入和导出向导，则可以通过选中 "**立即执行**" 复选框来立即运行包。 默认情况下，此复选框处于选中状态，包会立即运行。  
  
     还可以决定是将包保存到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 还是保存到文件系统。 如果选择保存包，还必须指定包保护级别。 有关包保护级别的详细信息，请参阅[对包中敏感数据的访问控制](../security/access-control-for-sensitive-data-in-packages.md)。  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导创建包并复制数据之后，可以使用 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器通过添加任务、转换和事件驱动的逻辑，打开和更改保存的包。  
  
    > [!NOTE]  
    >  在 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 中，未提供用来保存该向导所创建的包的选项。  
  
-   如果从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目启动 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 导入和导出向导，则无法将包作为完成向导的步骤来运行。 相反，该包将添加到启动该向导的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目中。 然后可以运行包，或者使用 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器添加任务、转换和事件驱动逻辑从而扩展包。  
  
 有关详细信息，请参阅[运行 SQL Server 导入和导出向导](start-the-sql-server-import-and-export-wizard.md)。  
  
## <a name="permissions-required-by-the-import-and-export-wizard"></a>导入和导出向导所需的权限  
 若要成功完成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导，您必须至少具有下列权限：  
  
-   连接到源数据库和目标数据库或文件共享的权限。 在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中，这需要服务器和数据库的登录权限。  
  
-   从源数据库或文件中读取数据的权限。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，这需要对源表和视图具有 SELECT 权限。  
  
-   向目标数据库或文件写入数据的权限。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，这需要对目标表具有 INSERT 权限。  
  
-   如果希望创建新的目标数据库、表或文件，则需要具有创建新的数据库、表或文件的足够权限。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，这需要具有 CREATE DATABASE 或 CREATE TABLE 权限。  
  
-   如果希望保存向导创建的包，则需要具有向 msdb 数据库或文件系统进行写入操作的足够权限。 在[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]中，这需要对 msdb 数据库具有 INSERT 权限。  
  
## <a name="mapping-data-types-in-the-import-and-export-wizard"></a>在导入和导出向导中映射数据类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导提供了最低限度的转换功能。 除了支持在新的目标表和目标文件中设置列的名称、数据类型和数据类型属性之外，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导不支持任何列级转换。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供的映射文件来将数据类型从一个数据库版本或系统映射到另一个数据库版本或系统。 例如，它可以从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 映射到 Oracle。 默认情况下，XML 格式的映射文件安装在 C:\Program Files\Microsoft SQL Server\100\DTS\MappingFiles 中。 如果业务需要在数据类型之间进行不同的映射，则可以更新映射以影响向导所执行的映射。 例如[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，如果想要在将数据从[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]传输到 db2 时将**nchar**数据类型映射到 db2**图形**数据类型而不是 db2 **VARGRAPHIC**数据类型，则可以更改 sqlclienttoibmdb2.xml 映射文件中的**nchar**映射，以使用**图形**而不是**VARGRAPHIC。**  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包括很多常用源和目标组合之间的映射，您可以在映射文件目录中添加新的映射文件，以支持其他源和目标。 新的映射文件必须遵守所发布的 XSD 架构，并在源和目标的唯一组合之间进行映射。  
  
> [!NOTE]  
>  如果编辑现有映射文件，或者向文件夹中添加新的映射文件，则必须关闭并重新打开 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导或 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]，以便识别新的或更改过的文件。  
  
## <a name="external-resources"></a>外部资源  
  
-   Technet.microsoft.com 上的视频[将 SQL Server 数据导出到 Excel （SQL Server 视频）](https://go.microsoft.com/fwlink/?LinkID=200975)  
  
-   CodePlex 示例，[使用向导从 ODBC 导出到平面文件教程：课程包](https://go.microsoft.com/fwlink/?LinkId=217657)，在 msftisprodsamples.codeplex.com 上  
  
  
