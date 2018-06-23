---
title: SQL Server 导入和导出向导 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
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
caps.latest.revision: 87
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 3e320ff0fdb834ca242739a76fb9e0b1242e3579
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36127343"
---
# <a name="sql-server-import-and-export-wizard"></a>SQL Server 导入和导出向导
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]导入和导出向导提供了要创建的最简单方法[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]将数据从源复制到目标的包。  
  
> [!NOTE]  
>  在 64 位计算机上，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 会安装 64 位版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导 (DTSWizard.exe)。 但是，有些数据源（如 Access 或 Excel）只提供 32 位提供程序。 若要使用这些数据源，您可能需要安装并运行 32 位版本的向导。 若要安装 32 位版本的向导，选择任一客户端工具或[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]在安装过程。  
  
 可以从“开始”菜单、从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、从 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或使用命令提示符启动 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 导入和导出向导。 有关详细信息，请参阅[运行 SQL Server 导入和导出向导](start-the-sql-server-import-and-export-wizard.md)。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]导入和导出向导可以将数据复制到和来自任何数据源为其托管[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]数据访问接口或本机 OLE DB 提供程序是可用。 可用访问接口的列表包括下列数据源：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   平面文件  
  
-   Microsoft Office Access  
  
-   Microsoft Office Excel  
  
 启动向导的环境不同，某些向导功能的工作方式也会有所不同：  
  
-   如果你启动[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]导入和导出向导[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，你立即运行包通过选择**立即执行**复选框。 默认情况下，此复选框处于选中状态，包会立即运行。  
  
     还可以决定是将包保存到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 还是保存到文件系统。 如果选择保存包，还必须指定包保护级别。 有关包保护级别的详细信息，请参阅[Access Control for Sensitive Data in Packages](../security/access-control-for-sensitive-data-in-packages.md)。  
  
     后[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]导入和导出向导创建包和将数据复制，则可以使用[!INCLUDE[ssIS](../../includes/ssis-md.md)]设计器打开并通过添加任务、 转换和事件驱动的逻辑来更改已保存的包。  
  
    > [!NOTE]  
    >  在[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]，以保存由向导创建的包的选项不可用。  
  
-   如果你启动[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]导入和导出向导从[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]项目中[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]，作为完成向导中的步骤无法运行包。 相反，该包将添加到启动该向导的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目中。 然后可以运行包，或者使用 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器添加任务、转换和事件驱动逻辑从而扩展包。  
  
 有关详细信息，请参阅[运行 SQL Server 导入和导出向导](start-the-sql-server-import-and-export-wizard.md)。  
  
## <a name="permissions-required-by-the-import-and-export-wizard"></a>导入和导出向导所需的权限  
 若要完成[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]导入和导出向导成功，您必须至少具有以下权限：  
  
-   连接到源数据库和目标数据库或文件共享的权限。 在[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]，这要求服务器和数据库登录权限。  
  
-   从源数据库或文件中读取数据的权限。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，这要求对源表和视图的 SELECT 权限。  
  
-   向目标数据库或文件写入数据的权限。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，这要求目标表的 INSERT 权限。  
  
-   如果希望创建新的目标数据库、表或文件，则需要具有创建新的数据库、表或文件的足够权限。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，这需要具有 CREATE DATABASE 或 CREATE TABLE 权限。  
  
-   如果你想要保存的向导，权限不足，无法写入 msdb 数据库或文件系统创建的包。 在[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]，这需要在 msdb 数据库上的 INSERT 权限。  
  
## <a name="mapping-data-types-in-the-import-and-export-wizard"></a>在导入和导出向导中映射数据类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]导入和导出向导提供最小转换功能。 除了支持在新的目标表和目标文件中设置列的名称、数据类型和数据类型属性之外，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导不支持任何列级转换。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]导入和导出向导使用该映射文件[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]提供映射到另一个数据库版本或系统数据类型。 例如，它可以从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 映射到 Oracle。 默认情况下，XML 格式的映射文件安装在 C:\Program Files\Microsoft SQL Server\100\DTS\MappingFiles 中。 如果业务需要在数据类型之间进行不同的映射，则可以更新映射以影响向导所执行的映射。 例如，如果你想[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **nchar**数据类型映射到 DB2**图形**数据类型，而不是 DB2 **VARGRAPHIC**时传输数据从数据类型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]到 DB2，你更改**nchar**映射中要使用的 SqlClientToIBMDB2.xml 映射文件**图形**而不是**VARGRAPHIC。**  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包括很多常用源和目标组合之间的映射，您可以在映射文件目录中添加新的映射文件，以支持其他源和目标。 新的映射文件必须遵守所发布的 XSD 架构，并在源和目标的唯一组合之间进行映射。  
  
> [!NOTE]  
>  如果你编辑一个现有的映射文件，或将新的映射文件添加到文件夹，必须关闭并重新打开[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]导入和导出向导或[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]能够识别新的或更改的文件。  
  
## <a name="external-resources"></a>外部资源  
  
-   视频，[将 SQL Server 数据导出到 Excel （SQL Server 视频）](http://go.microsoft.com/fwlink/?LinkID=200975)，technet.microsoft.com 上  
  
-   CodePlex 示例[将导出从 ODBC 到平面文件使用向导教程： 课程包](http://go.microsoft.com/fwlink/?LinkId=217657)，msftisprodsamples.codeplex.com 上  
  
  