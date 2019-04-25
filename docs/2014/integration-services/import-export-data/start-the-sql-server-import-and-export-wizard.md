---
title: 运行 SQL Server 导入和导出向导 |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Import and Export Wizard
- starting SQL Server Import and Export Wizard
- Import and Export Wizard
- starting Import and Export Wizard
ms.assetid: 5fc4f6d1-1f6f-444e-9aeb-827f85e1c405
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 824642cf50923aa7ec879bfedbbb8f4ceaa6d9f3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62768020"
---
# <a name="run-the-sql-server-import-and-export-wizard"></a>运行 SQL Server 导入和导出向导
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导为在数据源之间复制数据和构造基本包提供了一种最为简单的方法。 有关向导的详细信息，请参阅[SQL Server 导入和导出向导](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)。  
  
 有关演示如何使用 SQL Server 导入和导出向导来创建将数据从 SQL Server 数据库导出到 Microsoft Excel 电子表格的包的视频，请参阅[SQL Server 数据导出到 Excel （SQL Server 视频）](https://go.microsoft.com/fwlink/?LinkId=131024)。  
  
### <a name="to-start-the-sql-server-import-and-export-wizard"></a>启动 SQL Server 导入和导出向导  
  
-   上**启动**菜单，依次指向**所有程序**，指向**Microsoft SQL Server** ，然后单击**导入和导出数据**。  
  
     -或-  
  
     在中[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]，右键单击**SSIS 包**文件夹，，然后单击**SSISImport 和导出向导**。  
  
     -或-  
  
     在中[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]，然后在**项目**菜单中，单击**SSISImport 和导出向导**。  
  
     -或-  
  
     在中[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，连接到[!INCLUDE[ssDE](../../includes/ssde-md.md)]服务器类型，展开数据库，右键单击某个数据库，指向**任务**，然后单击**导入数据**或**导出数据**.  
  
     -或-  
  
     在命令提示符窗口中运行 DTSWizard.exe（位于 C:\Program Files\Microsoft SQL Server\100\DTS\Binn）。  
  
    > [!NOTE]  
    >  在 64 位计算机上，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 会安装 64 位版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导 (DTSWizard.exe)。 但是，有些数据源（如 Access 或 Excel）只提供 32 位提供程序。 若要使用这些数据源，您可能需要安装并运行 32 位版本的向导。 若要安装 32 位版本的向导，必须在安装过程中选择“客户端工具”或 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]。  
  
### <a name="to-import-or-export-data-by-using-the-sql-server-import-and-export-wizard"></a>使用 SQL Server 导入和导出向导导入或导出数据  
  
1.  启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导。  
  
2.  在相应的向导页面上，选择数据源和数据目标。  
  
     可用数据源包括 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 数据访问接口、OLE DB 访问接口、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 提供程序、[!INCLUDE[vstecado](../../includes/vstecado-md.md)] 提供程序、Microsoft Office Excel、Microsoft Office Access 和平面文件源。 根据源的不同，需要设置身份验证模式、服务器名称、数据库名称和文件格式之类的选项。  
  
    > [!NOTE]  
    >  [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider for Oracle 不支持 Oracle BLOB、CLOB、NCLOB、BFILE 和 UROWID 数据类型。 因此，OLE DB 源无法从包含具有上述数据类型的列的表中提取数据。  
  
     可用数据目标包括 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]数据访问接口、OLE DB 访问接口、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client、Excel、Access 和平面文件目标。  
  
3.  为选定的目标类型设置选项。  
  
     如果目标为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库，则可以指定下列内容：  
  
    -   指示是否创建新的数据库并设置数据库属性。 下列属性无法配置，因此向导使用指定的默认值：  
  
        |属性|ReplTest1|  
        |--------------|-----------|  
        |排序规则|Latin1_General_CS_AS_KS_WS|  
        |恢复模式|完全|  
        |使用全文索引|True|  
  
    -   选择是复制表或视图中的数据，还是复制查询结果。  
  
         如果要查询源数据并复制结果，则可以构造 Transact-SQL 查询。 可以手动输入 Transact-SQL 查询，也可以使用保存到文件的查询。 向导包含用于查找文件的浏览功能，当您选定文件后，向导会自动打开文件，并将其内容粘贴到向导页中。  
  
         如果源是 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 提供程序，则还可以使用该选项复制查询结果，并提供 DBCommand 字符串作为查询。  
  
         如果源数据是视图，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导自动将该视图转换为目标中的表。  
  
    -   指示是否删除目标表然后重新创建，以及是否启用标识插入。  
  
    -   指示在现有目标表中是删除行，还是追加行。 如果该表不存在，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导会自动创建该表。  
  
     如果目标是平面文件目标，则可以指定下列内容：  
  
    -   指定目标文件中的行分隔符。  
  
    -   指定目标文件中的列分隔符。  
  
4.  （可选）选择一个表并更改源列和目标列之间的映射，或更改目标列的元数据：  
  
    -   将源列映射到其他目标列。  
  
    -   更改目标列中的数据类型。  
  
    -   设置字符数据类型的列的长度。  
  
    -   设置数值数据类型的列的精度和小数位数。  
  
    -   指定该列可否包含 Null 值。  
  
5.  （可选）选择多个表并更新应用于这些表的元数据和选项：  
  
    -   选择现有的目标架构或提供要为其分配表的新架构。  
  
    -   指定是否在目标表中启用标识插入。  
  
    -   指定是否删除并重新创建目标表。  
  
    -   指定是否截断现有的目标表。  
  
6.  保存并运行包。  
  
     如果向导从 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或命令提示符启动，则包可以立即运行。 您还可以保存到包[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **msdb**数据库或文件系统。 有关详细信息**msdb**数据库，请参阅[包管理&#40;SSIS 服务&#41;](../service/package-management-ssis-service.md)。  
  
     保存包时，可以设置包保护级别，如果该保护级别使用密码，请提供密码。 有关包保护级别的详细信息，请参阅[包中敏感数据的访问控制](../security/access-control-for-sensitive-data-in-packages.md)。  
  
     如果向导从 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中的 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 项目启动，则无法从向导运行包。 相反，该包将添加到启动该向导的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目中。 然后您可以在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中运行包。  
  
    > [!NOTE]  
    >  在 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 中，未提供用来保存该向导所创建的包的选项。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 导入和导出向导](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)   
 [在 SQL Server Data Tools 中创建包](../create-packages-in-sql-server-data-tools.md)  
  
  
