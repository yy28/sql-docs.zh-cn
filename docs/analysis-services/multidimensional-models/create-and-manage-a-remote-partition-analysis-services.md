---
title: "创建和管理远程分区 (Analysis Services) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- partitions [Analysis Services], remote
- remote partitions [Analysis Services]
ms.assetid: 4322b5cb-af07-4e79-8ecb-59e1121a9eb8
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: bbcff2fe14716ebb2af74430538573706f8c2475
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="create-and-manage-a-remote-partition-analysis-services"></a>创建和管理远程分区 (Analysis Services)
  对度量值组进行分区时，可将远程 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例上的辅助数据库配置为分区存储。  
  
 多维数据集（称作主数据库）的远程分区存储于 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的远程实例上的专用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库（称作辅助数据库）中。  
  
 专用辅助数据库可存储一个（且仅一个）主数据库的远程分区，但主数据库可使用多个辅助数据库，条件是所有辅助数据库都在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的同一个远程实例上。 数据库中专用于远程分区的维度作为链接维度创建。  
  
## <a name="prerequisites"></a>先决条件  
 在创建远程分区之前，必须满足以下条件：  
  
-   您必须有第二个 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例和专用数据库才能存储分区。 辅助数据库只有一个用途：它提供主数据库的远程分区存储。  
  
-   两个服务器实例必须是相同版本。 两个数据库应该具有相同功能级别。  
  
-   两个实例都必须配置为进行 TCP 连接。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 不支持通过使用 HTTP 协议创建远程分区。  
  
-   两个计算机上的防火墙设置都必须设置为接受外部连接。 有关设置防火墙的详细信息，请参阅 [将 Windows 防火墙配置为允许 Analysis Services 访问](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)。  
  
-   运行主数据库的实例的服务帐户必须具有对 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的远程实例的管理访问权限。 如果该服务帐户更改，您必须更新对服务器和数据库的权限。  
  
-   您必须是两个计算机上的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 管理员。  
  
-   您必须确保灾难恢复计划适合远程分区的备份和还原。 使用远程分区可能使备份和还原操作变得复杂。 请确保仔细测试您的计划，以确保能够还原必需的数据。  
  
## <a name="configure-remote-partitions"></a>配置远程分区  
 运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的两个单独的计算机都是创建远程分区所必需的，需将一个计算机指定为主服务器，将另一个计算机指定为从属服务器。  
  
 以下过程假定您有两个服务器实例，且在主服务器上部署了多维数据集数据库。 为了实现此过程的目的，我们将多维数据集数据库称为 db-master。 将包含远程分区的存储数据库称为 db-storage。  
  
 您将使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 和 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 来完成此过程。  
  
> [!NOTE]  
>  远程分区只能与其他远程分区进行合并。 如果您在结合使用本地和远程分区，则也可以创建包括组合数据的新分区，删除不再使用的分区。  
  
#### <a name="specify-valid-server-names-for-cube-deployment-in-ssdt"></a>为多维数据集部署指定有效服务器名称（在 SSDT 中）。  
  
1.  在主服务器上：在解决方案资源管理器中，右键单击解决方案名称，然后选择“属性”。 在 **“属性”** 对话框中，单击 **“配置属性”**，然后依次单击 **“部署”**和 **“服务器”** ，并设置主服务器名称。  
  
2.  在从属服务器上：在解决方案资源管理器中，右键单击解决方案名称，然后选择“属性”。 在 **“属性”** 对话框中，单击 **“配置属性”**，然后依次单击 **“部署”**和 **“服务器”** ，并设置从属服务器名称。  
  
#### <a name="create-and-deploy-a-secondary-database-in-ssdt"></a>创建并部署辅助数据库（在 SSDT 中）  
  
1.  在从属服务器上：为存储数据库创建一个新 Analysis Services 项目。  
  
2.  在从属服务器上：在解决方案资源管理器中创建一个指向多维数据集数据库 db-master 的新数据源。 使用访问接口“本机 OLE DB\Microsoft OLE DB Provider for Analysis Services 11.0”。  
  
3.  在从属服务器上：部署解决方案。  
  
#### <a name="enable-features-in-ssms"></a>启用功能（在 SSMS 中）  
  
1.  在从属服务器上：在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，右键单击对象资源管理器中已连接的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例，然后选择“属性”。 将“功能\LinkToOtherInstanceEnabled”和“功能\LinkFromOtherInstanceEnabled”都设置为 **True**。  
  
2.  在从属服务器上：在对象资源管理器中右键单击服务器名称并选择“重新启动”，以重启服务器。  
  
3.  在主服务器上：在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，右键单击对象资源管理器中已连接的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例，然后选择“属性”。 将“功能\LinkToOtherInstanceEnabled”和“功能\LinkFromOtherInstanceEnabled”都设置为 **True**。  
  
4.  在主服务器上：在对象资源管理器中右键单击服务器名称并选择“重新启动”，以重新启动服务器。  
  
#### <a name="set-the-masterdatasourceid-database-property-on-the-remote-server-in-ssms"></a>设置远程服务器上的 MasterDataSourceID 数据库属性（在 SSMS 中）  
  
1.  在从属服务器上：右键单击存储数据库 db-storage，指向“编写数据库脚本为” | “ALTER 到” | “新建查询编辑器窗口”。  
  
2.  将 **MasterDataSourceID** 添加到 XMLA，然后将多维数据集数据库 db-master 的 ID 指定为值。 XMLA 应类似以下示例。  
  
    ```  
    <Alter ObjectExpansion="ExpandFull" xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
    <Object>  
       <DatabaseID>DB-Storage</DatabaseID>  
    </Object>  
    <ObjectDefinition>  
       <Database xmlns:xsd="http://www.w3.org/2001/XMLSchema" 400"   
          <ID>DB-Storage</ID>  
          <Name>DB-StorageB</Name>  
          <ddl200:CompatibilityLevel>1100</ddl200:CompatibilityLevel>  
          <Language>1033</Language>  
          <Collation>Latin1_General_CI_AS</Collation>  
          <DataSourceImpersonationInfo>  
    <ImpersonationMode>ImpersonateAccount</ImpersonationMode>  
             <Account>*********</Account>  
          </DataSourceImpersonationInfo>  
          <MasterDataSourceID>DB-Master</MasterDataSourceID>  
       </Database>  
    </ObjectDefinition>  
    </Alter>  
    ```  
  
3.  按 F5 执行该脚本。  
  
#### <a name="set-up-the-remote-partition-in-ssdt"></a>设置远程分区（在 SSDT 中）  
  
1.  在主服务器上：在多维数据集设计器中打开多维数据集，然后单击 **“分区”** 选项卡。展开度量值组。 如果已为多个分区配置了度量值组，则单击“新建分区”，或单击“源”列中的浏览 (. 。 .) 按钮编辑现有分区。  
  
2.  在分区向导的 **“指定源信息”**中，选择初始数据源视图和事实数据表。  
  
3.  如果正在使用查询绑定，请提供将要创建的新分区的数据进行分段的 WHERE 子句。  
  
4.  在“处理和存储位置”中，在“处理位置”下选择“远程 Analysis Services 数据源”，并单击“新建”以创建指向从属数据库 db-storage 的新数据源。  
  
    > [!NOTE]  
    >  如果收到错误，指示数据源在集合中不存在，则必须打开存储数据库 db-storage 的项目，并创建指向主数据库 db-master 的数据源。  
  
5.  在主服务器上：在解决方案资源管理器中右键单击多维数据集名称，选择“处理”，全面处理该多维数据集。  
  
## <a name="administering-remote-partitions"></a>管理远程分区  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支持远程分区的并行处理和顺序处理。 定义了分区的主数据库将在参与多维数据集分区处理的所有实例之间协调事务。 然后，将处理报表发送给处理了某一分区的所有实例。  
  
 包含远程分区的多维数据集可与其在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的单个实例上的分区一起管理。 但是，只能在定义了分区及其父多维数据集的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例上查看和更新远程分区的元数据。 无法在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的远程实例上查看或更新远程分区。  
  
> [!NOTE]  
>  尽管不向架构行集公开专用于存储远程分区的数据库，但使用分析管理对象 (AMO) 的应用程序仍可以通过使用 XML for Analysis Discover 命令来发现专用数据库。 通过使用 TCP 或 HTTP 客户端直接发送到专用数据库的所有 CREATE 或 DELETE 命令都将成功，但服务器将返回一个警告，指示该操作可能会损害这一紧密管理的数据库。  
  
## <a name="see-also"></a>另请参阅  
 [分区（Analysis Services - 多维数据）](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)  
  
  
