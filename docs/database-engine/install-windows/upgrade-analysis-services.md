---
title: "升级 Analysis Services | Microsoft Docs"
ms.custom: 
ms.date: 07/17/2017
ms.prod:
- sql-server-2016
- sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- upgrading databases
- databases [Analysis Services], upgrading
- installing Analysis Services, side-by-side installations
- Analysis Services upgrades
- Analysis Services upgrades, about upgrading Analysis Services
- SSAS, database migration
- upgrading Analysis Services
- installing Analysis Services, upgrading
- SSAS, upgrading
ms.assetid: a131d329-386e-4470-aaa9-ffcde4e5ec0c
caps.latest.revision: 79
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 3b3ad4ecf62f3a30882720140f2f362007f8428b
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="upgrade-analysis-services"></a>升级 Analysis Services
  可以将 Analysis Services 实例升级到具有相同服务器模式的 SQL Server 版本，以充分利用当前版本中引入的功能，如 [Analysis Services 中的新增功能](../../analysis-services/what-s-new-in-analysis-services.md)中所述。  
  
 你可以就地升级独立于在同一硬件上运行的其他实例的每个实例。 但是，大多数管理员选择在将生产工作负荷转移到新服务器上之前安装用于应用程序测试的新版本的新实例。 但对于开发或测试服务器来说，就地升级可能会更方便。  
  
 升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]之前，请先查看以下内容：  

- [SQL Server 2017 发行说明](../../sql-server/sql-server-2017-release-notes.md)描述了已知的问题和解决方法。  
- [SQL Server 2016 发行说明](../../sql-server/sql-server-2016-release-notes.md) 描述了已知的问题和解决方法。  
- [Analysis Services Backward Compatibility](../../analysis-services/analysis-services-backward-compatibility.md) 总结了不再使用、不推荐使用和改进的功能。 你应定期检查这些列表以评估模型、脚本或自定义代码产品发生更改的影响。 通常情况下，会在下一个主要版本的预发行期间公布功能过渡。  
  
## <a name="server-upgrade"></a>服务器升级  
 有两种升级服务器和数据库的基本方法：  
  
-   **就地升级** 将使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 程序文件替换现有的程序文件。 数据库保持在相同的位置中。 程序文件夹将更新以反映新名称。  
  
-   **并行升级** 通常在同一台计算机上创建 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]新安装（除非同时升级硬件）。 此方法要求你将数据库移动到新的实例，然后根据需要卸载以前的版本，以释放磁盘空间。  
  
 除非手动更改附加到给定服务器的数据库兼容级别，否则它们保持不变。  
  
### <a name="in-place-upgrade"></a>就地升级  
 可以将 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的现有实例升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] and, as part of the upgrade process, au的现有实例升级到matically migrate existing databases from the old instance 的现有实例升级到 the new instance. 因为元数据和二进制数据在两个版本之间兼容，因此升级之后您可以保留该数据而不必手动迁移该数据。  
  
 若要升级现有实例，请运行安装程序并将现有实例的名称指定为新实例的名称。  
  
### <a name="side-by-side-upgrade"></a>并行升级  
  
-   备份所有数据库，并验证每个可以还原的数据库。 请参阅 [Backup and Restore of Analysis Services Databases](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)。  
  
-   确定报表、电子表格或仪表板快照的子集，以在稍后用作确认升级后服务器操作的基础。 如果可能，收集性能测量值，以便你可以对在已升级的服务器上运行的相同的工作负载进行比较。  
  
-   安装 Analysis Services 的新实例，选择相同的服务器模式（表格或多维）作为你想要替换的服务器。 请参阅 [Install Analysis Services](../../analysis-services/instances/install-windows/install-analysis-services.md)。  
  
     执行配置端口和添加服务器管理员的安装后的任务。 请参阅[安装后配置 (Analysis Services)](../../analysis-services/instances/post-install-configuration-analysis-services.md)。  
  
-   附加或还原每个数据库。  
  
-   运行 DBCC 以检查数据库完整性。 与对整个模型层次结构中的孤立对象的测试相比，表格模型经历的检查更彻底。 对于多维模型而言，只会检查分区索引。 请参阅[适用于 Analysis Services 表格数据库和多维数据库的数据库一致性检查器 (DBCC)](../../analysis-services/instances/database-consistency-checker-dbcc-for-analysis-services.md)。  
  
-   测试报表、电子表格和仪表板，以确认行为或计算没有任何负面更改。 你应看到针对多维和表格工作负荷更快的性能。  
  
-   测试处理操作，更正任何登录或权限问题。 如果使用默认服务帐户进行连接，则新的服务将在不同的帐户下运行。 有关 Analysis Services 的启动帐户的详细信息，请参阅[配置服务帐户 (Analysis Services)](../../analysis-services/instances/configure-service-accounts-analysis-services.md)。  
  
-   在已升级服务器上测试备份和还原操作，调整脚本以使用新的服务器名称。  
  
## <a name="database-upgrade"></a>数据库升级  
 在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的之前版本中创建的数据库基于较旧的数据库兼容性级别设置在升级的服务器上运行。 通常情况下，你可以升级数据库或模型以使用更高的兼容性级别获得访问新功能的权限，但请注意，这样做可能将你绑定到特定的服务器版本。  
  
 若要升级数据库，通常应先升级 SQL Server Data Tools (SSDT) 中的模型，然后再将解决方案部署到已升级的服务器实例。 请参阅 [Download SQL Server Data Tools（下载 SQL Server Data Tools）](https://msdn.microsoft.com/library/mt204009.aspx) 获取最新版本。  
  
 表格和多维数据库遵循不同的路径版本。 巧合的是多维和表格模型都具有 1100 的兼容级别。  如果功能更改只影响一个模式，则其将以不同的速率前进。  
  
 出于背景目的，下表总结了兼容性级别，但你应查看详细信息主题，以了解每个级别提供的内容。  
  
||||  
|-|-|-|  
|表格|1200|SQL Server 2016|  
|表格|1103|SQL Server 2014|  
|表格|1100|SQL Server 2012|  
|多维|1100|SQL Server 2012 和更高版本|  
|多维|1050|SQL Server 2005、2008、2008 R2|  
  
 有关详细信息，请参阅[多维数据库的兼容级别 (Analysis Services)](../../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md) 和 [Analysis Services 中表格模型的兼容级别](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)。  
  
## <a name="tabular-model-upgrade-to-1200-compatibility-level"></a>表格模型升级到 1200 兼容级别  
 表格模型和数据库中从 SQL Server 2016 中获益最大。 此版本为位于 1200 兼容级别的表格模型提供了修改后的 DirectQuery 模式，通过删除混合模式对该模式进行了简化、添加了用于设计时检索数据子集的查询语句，并通过 DAX（而不是后端数据库中的行权限）添加了行级安全性。  
  
 升级的第二个原因是该模型中的新表格元数据构造。 新兼容级别 1200 的表格模型（无论是在该级别创建的还是升级到该级别的表格模型）使用为对象定义的本机术语（如模型、表、关系和列）来描述其主要元素。  
  
 若要升级表格模型，请使用为此版本生成的 [SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx)的版本，以将“兼容级别”属性更改为 **SQL Server 2016 RTM (1200)**。  
  
 不要使用 SSMS、代码或脚本更改 **CompatibilityLevel**。 就其本身而言，更改属性没有任何影响。 作为对属性更新的响应将在 SSDT 中发生元数据转换，之后将重新打开项目。  
  
 与往常一样，在更新前要确保已保存模型的备份，以防需要还原回升级前的版本。  
  
1.  在“SSDT”>“解决方案资源管理器”中，右键单击“model.bim”，选择“查看代码”，确认将关闭该模型并在新窗口（代码窗口）中重新打开。  
  
2.  该模型将作为 XMLA 文档打开。 为了便于与转换后进行比较，请将内容复制到另一个文件（可以在 SSDT 中打开新的 XML 文件）。  
  
3.  右键单击“model.bim”并将其更改回“视图设计器”。  
  
4.  将“兼容级别”设置为 **SQL Server 2016 RTM (1200)**。  
  
5.  此步骤无法撤消，因此需要确认该操作。 单击“是”  继续。 将刷新该项目。  
  
6.  右键单击“model.bim”并将其更改回“查看代码”。  
  
     请注意，模型定义现在采用的是使用表格元数据的 JSON 进行的。  
  
 **元数据转换**  
  
 比较转换前后的元数据，你会发现该元数据已经转换为 JSON，并剪裁了冗余定义。  
  
 模型将保留所有功能：数据绑定、分区切片、表达式、对象标识符、对象名称、说明、描述、翻译和注释都将保持不变。 但如果代码或脚本引用了特定对象，则代码重写的一部分将包括删除对不再存在的对象的引用。 例如，1050 或 1103 模型将包含多维数据集外部的维度部分，而 1200 模型会将表定义为单个对象。  
  
> [!NOTE]  
>  支持但不推荐使用早期版本的兼容级别 1050 和 1103。 在以后的某些 SQL Server 更高版本中，将不再支持将表格模型强制转换为多维对象。 请参阅 [Deprecated Analysis Services Features in SQL Server 2016](../../analysis-services/deprecated-analysis-services-features-in-sql-server-2016.md) 了解相关公告。  
  
## <a name="post-upgrade-for-tabular-models-at-1200-compatibilitylevel"></a>升级后处于 1200 兼容级别的表格模型  
 转换该模型后，将使用 [表格模型脚本语言 (TMSL) 参考](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)，而不是 XMLA 编写数据库操作脚本。 当模型为 1200 时，将在 SSMS 中自动生成 TMSL。 以 1200 表格数据库为目标的自定义代码应使用 Microsoft.AnalysisServces.Tabular 命名空间中定义的 API。 脚本和代码必须从头开始编写；没有内置转换机制。 有关开始使用的帮助信息，请参阅 [Analysis Services 开发人员文档](../../analysis-services/analysis-services-developer-documentation.md) 。  
  
 还可以向表格模型添加以下功能，此操作仅支持 1200 兼容级别：  
  
-   DirectQuery 实现，此实现支持表格模型中通过 DAX 的行级安全性、用于建模的更多数据源、数据集以及简单配置。  
  
-   计算列  
  
-   显示文件夹  
  
## <a name="upgrade-tabular-models-in-directquery-mode"></a>使用 DirectQuery 模式升级表格模型  
 不能对配置为 DirectQuery 的较旧表格模型执行就地升级。 DirectQuery 的新实现具有较小的配置需求量且并非所有设置都可以移植。  
  
1.  在 SSDT 中，关闭 **DirectQuery** 模式，以使该模型使用内存中存储。 有关说明，请参阅[启用 DirectQuery 设计模式（SSAS 表格）](https://msdn.microsoft.com/library/hh270245.aspx)。  
  
2.  将“兼容级别”设置为 SQL Server 2016 RTM (1200)。  
  
3.  保存并重新生成或部署模型。  
  
4.  重新打开 **DirectQuery** 。 请参阅 [DirectQuery for Tabular 1200 models](http://msdn.microsoft.com/library/4227977e-7368-4d45-b78f-24076882e7a8) 获取更多指导。  
  
## <a name="see-also"></a>另请参阅  
 [DirectQuery 模式（SSAS 表格）](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)   
 [Analysis Services 中的新增功能](../../analysis-services/what-s-new-in-analysis-services.md)   
 [SQL Server 2016 各个版本支持的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)   
 [计划 SQL Server 安装](../../sql-server/install/planning-a-sql-server-installation.md)   
 [升级 Power Pivot for SharePoint](../../database-engine/install-windows/upgrade-power-pivot-for-sharepoint.md)   
 [在多维和数据挖掘模式下安装 Analysis Services](http://msdn.microsoft.com/library/8a1f33e8-2bd6-4fb8-bd46-c86f2a067f60)   
 [使用安装向导（安装程序）升级到 SQL Server 2016](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)  
  
  

