---
title: "Analysis Services 数据库的备份和还原 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.asvs.ssmsimbi.Restore.f1
- sql13.asvs.ssmsimbi.Backup.f1
helpviewer_keywords:
- backing up databases [Analysis Services]
- encryption [Analysis Services]
- databases [Analysis Services], restoring
- cryptography [Analysis Services]
- databases [Analysis Services], backing up
- restoring databases [Analysis Services]
- recovery [Analysis Services]
ms.assetid: 947eebd2-3622-479e-8aa6-57c11836e4ec
caps.latest.revision: "54"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: f750fc5c1c991b8cf4392d427855f583c478c028
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="backup-and-restore-of-analysis-services-databases"></a>备份和还原 Analysis Services 数据库
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]包括备份和还原，以便你可以恢复数据库及其对象从某个特定点时间。 此外，备份和还原是一项用于将数据库迁移到升级后的服务器、在服务器之间移动数据库或将数据库部署到生产服务器的有效方法。 出于数据恢复目的，如果您还没有制定备份计划并且您的数据十分重要，则应尽快设计和实施备份计划。  
  
 对已部署的 Analysis Services 数据库执行备份和还原命令。 对于 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中的项目和解决方案，您应该使用源控制来确保可以还原特定版本的源文件，然后为您所使用的源控制系统的存储库创建数据恢复计划。  
  
 若要进行包括源数据在内的完整备份，则必须备份包含详细数据的数据库。 具体而言，如果使用的是 ROLAP 或 DirectQuery 数据库存储，则详细信息数据存储在与 Analysis Services 数据库分开的外部 SQL Server 关系数据库中。 否则，如果所有对象都是表格或多维对象，Analysis Services 备份将既包含元数据又包含源数据。  
  
 自动备份的一个显著优点是：数据快照将按照自动备份频率所规定的时间或间隔始终保持最新状态。 自动计划程序可确保备份不会被忘记。 此外，还原数据库也可以自动进行，并且是一种复制数据的好方法，但务必要备份所复制实例的加密密钥文件。 同步功能专门用于复制 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库，但仅限过期数据。 此处提及的所有功能都可以通过用户界面、XML/A 命令实现或通过 AMO 以编程方式运行。 有关备份策略的详细信息，请参阅 [Backup Strategies with SQL Server 2005 Analysis Services](http://go.microsoft.com/fwlink/?LinkId=81888)（SQL Server 2005 Analysis Services 的备份策略）。  
  
 本主题包含以下各节：  
  
-   [准备备份](#bkmk_prep)  
  
-   [备份多维或表格数据库](#bkmk_cube)  
  
-   [还原 Analysis Services 数据库](#bkmk_restore)  
  
##  <a name="bkmk_prereq"></a> 先决条件  
 您必须对 Analysis Services 实例具有管理权限，或对要备份的数据库拥有完全控制（管理员）权限。  
  
 还原位置所在的 Analysis Services 实例版本必须与执行备份的实例版本相同或比它更高的版本。 尽管你不能将数据库从 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 实例还原到更低版本的 Analysis Services，但是通常可在更高的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 实例上还原更低版本的数据库（如 SQL Server 2012）。  
  
 还原位置必须是相同的服务器类型。 表格数据库只能还原到在表格模式下运行的 Analysis Services。 多维数据库需要在多维模式下运行的实例。  
  
##  <a name="bkmk_prep"></a> 准备备份  
 使用以下核对清单来准备备份：  
  
-   检查要存储备份文件的位置。 如果使用远程位置，您必须将其指定为 UNC 文件夹。 确认您可以访问该 UNC 路径。  
  
-   检查针对该文件夹的权限，确保 Analysis Services 服务帐户对该文件夹具有读/写权限。  
  
-   检查目标服务器上是否有足够的磁盘空间。  
  
-   检查是否有同名的现有文件。 如果已存在同名文件，则备份将失败，除非您指定用于覆盖此文件的选项。  
  
##  <a name="bkmk_cube"></a> 备份多维或表格数据库  
 管理员可以将 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库备份到单个 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 备份文件 (.abf)，这与数据库的大小无关。 有关分步说明，请参阅 [如何备份 Analysis Services 数据库 (TechMantra)](http://www.mytechmantra.com/LearnSQLServer/Backup_an_Analysis_Services_Database.html) 和 [自动备份 Analysis Services 数据库 (TechMantra)](http://www.mytechmantra.com/LearnSQLServer/Automate_Backup_of_Analysis_Services_Database.html)。  
  
> [!NOTE]  
>  [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]用于加载和查询[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]数据模型在 SharePoint 环境中，从 SharePoint 内容数据库加载其模型。 这些内容数据库是相关的且运行于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 关系数据库引擎上。 同样，没有针对 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据模型的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 备份和还原策略。 如果你有针对 SharePoint 内容的灾难恢复计划，则该计划包含存储在内容数据库中的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据模型。  
  
 **远程分区**  
  
 如果 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库包含远程分区，则还应备份这些远程分区。 在备份包含远程分区的数据库时，每台远程服务器上的所有远程分区将分别备份到该远程服务器上的单个文件中。 因此，如果脱离各自主机创建这些远程备份，则必须手动将这些文件复制到指定的存储区域。  
  
 **备份文件的内容**  
  
 备份 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库时会生成一个备份文件，其内容因数据库对象所使用的存储模式而异。 之所以出现备份内容差异，原因在于每个存储模式实际上都存储了 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库中的不同信息集。 例如，多维混合 OLAP (HOLAP) 分区和维度存储 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库中的聚合和元数据，而关系 OLAP (ROLAP) 分区和维度则只存储 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库中的元数据。 由于 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库的实际内容因每个分区的存储模式而异，所以备份文件的内容也会有所不同。 下表将备份文件的内容与对象所使用的存储模式关联起来。  
  
|存储模式|备份文件的内容|  
|------------------|-----------------------------|  
|多维 MOLAP 分区和维度|元数据、源数据和聚合|  
|多维 HOLAP 分区和维度|元数据和聚合|  
|多维 ROLAP 分区和维度|元数据|  
|表格内存中模型|元数据和源数据|  
|表格 DirectQuery 模型|仅元数据|  
  
> [!NOTE]  
>  备份 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库时不备份任何基础数据源（如关系数据库）中的数据。 只备份 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库的内容。  
  
 备份 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库时，可做出如下选择：  
  
-   是否压缩所有数据库备份。 默认情况下压缩备份。  
  
-   是否加密备份文件内容并需要密码才能解密和还原文件。 默认情况下，不加密备份数据。  
  
    > [!IMPORTANT]  
    >  对于每个备份文件，运行备份命令的用户必须对每个文件的指定备份位置拥有写入权限。 此外，用户必须具有以下角色之一：针对 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的服务器角色成员，或对要备份的数据库拥有完全控制（管理员）权限的数据库角色成员。  
  
 有关备份 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库的详细信息，请参阅 [备份选项](../../analysis-services/multidimensional-models/backup-options.md)。  
  
##  <a name="bkmk_restore"></a> 还原 Analysis Services 数据库  
 管理员可以从一个或多个备份文件中还原 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库。  
  
> [!NOTE]  
>  如果备份文件已加密，则必须提供在备份期间指定的密码，才能使用该文件还原 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库。  
  
 在还原期间，您有如下选择：  
  
-   可以使用原始数据库名还原数据库，也可以指定一个新数据库名。  
  
-   可以覆盖现有数据库。 如果选择覆盖数据库，必须明确指定要覆盖现有数据库。  
  
-   可以选择是还原现有安全信息还是跳过安全成员身份信息。  
  
-   可以选择使用还原命令为所还原的每个分区更改还原文件夹。 本地分区可以还原到数据库所还原到的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的任意本地文件夹位置。 远程分区可以还原到除本地服务器之外的任意服务器上的任意文件夹；远程分区不能还原到本地。  
  
    > [!IMPORTANT]  
    >  对于每个备份文件，运行还原命令的用户必须对每个文件的指定备份位置具有读取权限。 若要还原未在服务器上安装的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库，用户还必须是此 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的服务器角色成员。 若要覆盖 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库，用户必须具有以下角色之一： [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的服务器角色成员，或对要还原的数据库拥有完全控制（管理员）权限的数据库角色成员。  
  
    > [!NOTE]  
    >  还原现有数据库之后，还原了此数据库的用户可能会失去对还原后的数据库的访问权限。 如果在执行备份时用户不是服务器角色成员或者不是拥有完全控制（管理员）权限的数据库角色成员，则会出现这种失去访问权限的情形。  
  
 有关还原 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库的详细信息，请参阅 [还原选项](../../analysis-services/multidimensional-models/restore-options.md)。  
  
## <a name="see-also"></a>另请参阅  
 [备份、还原和同步数据库 (XMLA)](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)   

  
  
