---
title: "同步 Analysis Services 数据库 |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Analysis Services deployments, Synchronize Database Wizard
- deploying [Analysis Services], Synchronize Database Wizard
- Synchronize Database Wizard
- synchronization [Analysis Services]
ms.assetid: 6aeff68d-8470-43fb-a3ed-a4b9685332c2
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ad1667e587056d10fd1b30b0b804366dbd5dfa14
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="synchronize-analysis-services-databases"></a>同步 Analysis Services 数据库
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 包括一个数据同步功能，该功能通过将数据和元数据从源服务器上的数据库复制到目标服务器上的数据库，使两个 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库等同。 使用“同步数据库”功能可完成以下任务之一：  
  
-   将数据库从临时服务器部署到生产服务器。  
  
-   更新生产服务器上的数据库，使其包含对临时服务器上数据库中数据和元数据的更改。  
  
-   生成 XMLA 脚本，您以后可运行该脚本来同步数据库。  
  
-   对于在多个服务器上处理多维数据集和维度的分布式工作负荷，使用数据库同步可将更改合并到单个数据库中。  
  
 数据库同步在目标服务器上启动，将数据和元数据提取到源服务器上的数据库副本中。 如果该数据库不存在，将创建一个。 同步是单向的一次性操作，在数据库复制之后立即结束。 它不在数据库之间提供实时奇偶校验。  
  
 可以重新同步源服务器和目标服务器上已存在的数据库，将最新更改从临时服务器提取到生产数据库中。 两个服务器上的文件将进行比较以检查是否存在更改，发生更改的文件将更新。 在后台进行同步期间，目标服务器上的现有数据库保持可用状态。 同步进行过程中，用户可以继续查询目标数据库。 同步完成之后， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 自动使用户切换到新复制的数据和元数据，并从目标数据库删除旧数据。  
  
 若要同步数据库，请运行同步数据库向导以立即同步数据库，或使用该向导生成可以在以后运行的同步脚本。 任一方法都可以用于提高 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库和多维数据集的可用性和可伸缩性。  
  
> [!NOTE]  
>  以下针对以前版本的 Analysis Services 撰写的白皮书仍适用于使用 SQL Server 2012 生成的可缩放多维解决方案。 有关详细信息，请参阅 [使用 Analysis Services 缩放查询](http://go.microsoft.com/fwlink/?LinkId=253136) 和 [使用只读数据库缩放 Analysis Services 查询](http://go.microsoft.com/fwlink/?LinkId=253137.)  
  
## <a name="prerequisites"></a>先决条件  
 在启动数据库同步的目标服务器上，您必须是具有 Analysis Services 服务器管理员角色的成员。 在源服务器上，您的 Windows 用户帐户必须拥有源数据库上的完全控制权限。 如果以交互方式同步数据库，请注意同步在 Windows 用户标识的安全上下文中运行。 如果帐户被拒绝访问特定对象，则操作将排除这些对象。 有关服务器管理员角色和数据库权限的详细信息，请参阅[向 Analysis Services 实例授予服务器管理员权限](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md)和[授予数据库权限 (Analysis Services)](../../analysis-services/multidimensional-models/grant-database-permissions-analysis-services.md)。  
  
 两个服务器上的 TCP 端口 2383 必须都打开，默认实例之间才能建立远程连接。 有关在 Windows 防火墙中创建例外的详细信息，请参阅 [Configure the Windows Firewall to Allow Analysis Services Access](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)。  
  
 源和目标服务器必须是相同的版本和 service pack。 因为模型元数据也同步的以确保生成的兼容性的两个服务器的数量应相同。 每个安装的版本都必须支持数据库同步。 对于 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，Enterprise、Developer 和 Business Intelligence 版本中支持数据库同步。 有关每个版本中的功能的详细信息，请参阅[版本和 SQL Server 2016 的支持的功能](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
 每个服务器上的服务器配置模式都必须相同。 如果同步的数据库是多维数据库，则必须针对多维服务器模式配置源服务器和目标服务器。 有关部署模式的详细信息，请参阅 [Determine the Server Mode of an Analysis Services Instance](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)。  
  
 如果源服务器上使用迟缓聚合处理，请关闭它。 在后台处理的聚合可能会干扰数据库同步。 有关设置此服务器属性的详细信息，请参阅 [OLAP Properties](../../analysis-services/server-properties/olap-properties.md)。  
  
> [!NOTE]  
>  要确定同步是不是合适的方法，数据库大小是要考虑的因素。 没有硬件要求，但是如果同步太慢，请考虑按以下技术文章所述并行同步多个服务器： [Analysis Services 同步最佳做法](http://go.microsoft.com/fwlink/?LinkID=253136)。  
  
## <a name="synchronize-database-wizard"></a>同步数据库向导  
 使用同步数据库向导可执行从源数据库到目标数据库的单向同步，或生成用于指定数据库同步操作的脚本。 在同步过程中，可以同步本机和远程分区并选择是否包含角色。  
  
 同步数据库向导可指引您完成以下步骤：  
  
-   选择要同步的源实例和数据库。  
  
-   在目标实例上选择本地分区的存储位置。  
  
-   在其他目标实例上选择远程分区的存储位置。  
  
-   选择安全级别以及要从源实例和数据库复制到目标实例的成员身份信息。  
  
-   选择是立即同步，还是将同步数据库向导生成的 XML for Analysis (XMLA)“同步”命令保存到脚本文件中，以便以后同步。  
  
 默认情况下，向导同步除现有安全组中的成员身份以外的所有数据和元数据。 您还可以在同步数据和元数据时复制所有安全设置或忽略所有安全设置。  
  
#### <a name="run-the-wizard"></a>运行向导  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，连接到将运行目标数据库的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例。 例如，如果要将数据库部署到生产服务器，则在生产服务器上运行该向导。  
  
2.  在对象资源管理器中，右键单击“数据库”文件夹，然后单击“同步”。  
  
3.  指定源服务器和源数据库。 在“选择要同步的数据库”页上，在 **“源服务器”** 和 **“源数据库”**中键入源服务器和源数据库的名称。 例如，如果从测试环境部署到生产服务器，则源是临时服务器上的数据库。  
  
     **“目标服务器”** 显示同步 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] “源数据库” **中所选数据库中的数据和元数据时所使用的** 实例的名称。  
  
     同步将在具有相同名称的源数据库和目标数据库上发生。 如果目标服务器已经有与源数据库共享相同名称的数据库，则使用源的元数据和数据更新目标数据库。 如果该数据库不存在，将在目标服务器上创建它。  
  
4.  或者，可以更改本地分区的位置。 使用 **“为本地分区指定位置”** 页指示本地分区是否应存储在目标服务器上。  
  
    > [!NOTE]  
    >  只有在指定的数据库中至少存在一个本地分区时，才会显示此页。  
  
     如果一组分区安装在源服务器的驱动器 C 上，则利用该向导可将这组分区复制到目标服务器上的另一个位置。 如果您不更改默认位置，向导会将源服务器上每个多维数据集中的度量值组分区部署到目标服务器上的相同位置。 同样，如果源服务器使用远程分区，则目标服务器也将使用相同的远程分区。  
  
     选择 **“位置”** 选项将显示一个网格，其中列出了将存储在目标实例上的本地分区的源文件夹、目标文件夹和估计大小。 该网格包含以下列：  
  
     **源文件夹**  
     显示包含本地分区的源 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例上的文件夹名称。 如果该列包含值“(Default)”，则源实例的默认位置应包含本地分区。  
  
     **目标文件夹**  
     显示要在其中同步本地分区的目标 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例上的文件夹名称。 如果该列包含值“(Default)”，则目标实例的默认位置应包含本地分区。  
  
     单击省略号 (**...**) 按钮可显示“查找远程文件夹”对话框，通过该对话框可以指定所选位置中存储的本地分区应同步到其中的目标实例上的文件夹。  
  
    > [!NOTE]  
    >  对于源实例的默认位置中存储的本地分区，无法更改此列。  
  
     **Size**  
     显示本地分区的估计大小。  
  
     **“所选位置中的分区”** 选项显示一个网格，对 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] “位置” **中所选行的** “源文件夹” **列中指定的源**实例所在位置存储的本地分区进行了说明。  
  
     **多维数据集**  
     显示包含该分区的多维数据集的名称。  
  
     **度量值组**  
     显示包含该分区的多维数据集中的度量值组的名称。  
  
     **分区名称**  
     显示分区的名称。  
  
     **大小 (Mb)**  
     显示该分区的大小 (MB)。  
  
5.  或者，可以更改远程分区的位置。使用 **“为远程分区指定位置”** 页可指示是否应同步源服务器上的指定数据库管理的远程分区，并指定存储所选远程分区的目标 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例和数据库。  
  
    > [!NOTE]  
    >  只有在源 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例上指定的数据库至少管理了一个远程分区时，才会显示此页。  
  
     选择 **“位置”** 选项将显示一个网格，其中列出了源数据库的远程分区所在存储位置的详细信息，包括可以从所选数据库中获取的源信息、目标信息和每个位置所使用的存储大小。 该网格包含以下列：  
  
     **Sync**  
     选择此项将在同步期间包括包含远程分区的位置。  
  
    > [!NOTE]  
    >  对于某个位置，如果未选择此选项，将不会同步该位置中包含的远程分区。  
  
     **“源服务器”**  
     显示包含远程分区的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的名称。  
  
     **源文件夹**  
     显示包含远程分区的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例上的文件夹名称。 如果该列包含值“(Default)”，则“源服务器”中显示的实例的默认位置将包含远程分区。  
  
     **“目标服务器”**  
     显示 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的名称，应在其中同步“源服务器”和“源文件夹”中指定的位置所存储的远程分区。  
  
     单击省略号 (**...**) 按钮可显示“连接管理器” 对话框，并指定应在其中同步所选位置中存储的远程分区的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例。  
  
     **目标文件夹**  
     显示要在其中同步远程分区的目标 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例上的文件夹名称。 如果该列包含值“(Default)”，则目标实例的默认位置应包含远程分区。  
  
     单击省略号 (**...**) 按钮可显示“查找远程文件夹” 对话框，通过该对话框可以指定所选位置中存储的远程分区应同步到其中的目标实例上的文件夹。  
  
     **Size**  
     显示该位置中存储的远程分区的估计大小。  
  
     **“所选位置中的分区”** 显示一个网格，对在源 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例上指定位置（在 **“位置”** 中所选行的 **“源文件夹”**列指定）存储的远程分区进行了说明。 该网格包含以下列：  
  
     **多维数据集**  
     显示包含该分区的多维数据集的名称。  
  
     **度量值组**  
     显示包含该分区的多维数据集中的度量值组的名称。  
  
     **分区名称**  
     显示分区的名称。  
  
     **大小 (Mb)**  
     显示该分区的大小 (MB)。  
  
6.  指定是否应包括用户权限信息以及是否应使用压缩。 默认情况下，向导在将文件复制到目标服务器之前压缩所有数据和元数据。 使用此选项可加快文件传输。 文件到达目标服务器后会进行解压缩。  
  
     **全部复制**  
     选择此项将在同步期间包含安全定义和成员身份信息。  
  
     **跳过成员身份**  
     选择此项将在同步期间包含安全定义，但排除成员身份信息。  
  
     **全部忽略**  
     选择忽略源数据库中的当前安全定义和成员身份信息。 如果在同步过程中创建目标数据库，则不会复制安全定义或成员身份信息。 如果目标数据库已存在并且具有角色和成员身份，则保留安全信息。  
  
7.  选择同步方法。 可以立即同步或生成保存到文件的脚本。 默认情况下，该文件使用 .xmla 扩展名保存，置于 Documents 文件夹中。  
  
8.  单击 **“完成”** 进行同步。 验证 **“完成向导”** 页上的选项后，再次单击 **“完成”** 。  
  
## <a name="next-steps"></a>后续步骤  
 如果未同步角色或成员身份，请注意立即指定对目标数据库的用户访问权限。  
  
## <a name="see-also"></a>另请参阅  
 [Synchronize 元素 (XMLA)](../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)   
 [使用 XMLA 部署模型解决方案](../../analysis-services/multidimensional-models/deploy-model-solutions-using-xmla.md)   
 [使用部署向导部署模型解决方案](../../analysis-services/multidimensional-models/deploy-model-solutions-using-the-deployment-wizard.md)  
  
  

