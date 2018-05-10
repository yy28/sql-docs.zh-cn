---
title: 表格模型解决方案部署 |Microsoft 文档
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 14b8cb7202785ab0ca4eea1f55de1781d2aca120
ms.sourcegitcommit: 1aedef909f91dc88dc741748f36eabce3a04b2b1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2018
---
# <a name="tabular-model-solution-deployment"></a>表格模型解决方案部署 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  在创作某一表格模型项目后，您必须部署此项目，以便用户通过使用报表客户端应用程序浏览该模型。 本文介绍各种属性和部署你的环境中的表格模型解决方案时，可以使用的方法。  
  
##  <a name="bkmk_benefits"></a> 优点  
 部署表格模型将在测试、临时或生产环境中创建模型数据库。 然后，用户可以通过 Sharepoint 中的 .bism 连接文件或通过直接使用来自报表客户端应用程序（例如 Microsoft Excel、 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]或自定义应用程序）的数据连接，来连接到已部署的模型。 你在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中创建新的表格模型项目时创建并用于创作模型的模型工作区数据库将保留在工作区服务器实例上，这允许你对该模型项目进行更改，然后在需要时重新部署到测试、临时或生产环境中。  
  
##  <a name="bkmk_deploying_bism"></a> 部署表格模型从 SQL Server Data Tools (SSDT)  
 部署是一个较为简单的过程；但是，必须执行某些步骤，以便确保您的模型部署到正确的 Analysis Services 实例上并且具有正确的配置选项。  
  
 表格模型被定义的多个特定于部署的属性。 在您部署时，将建立与在 **“服务器”** 属性中指定的 Analysis Services 实例的连接。 然后在该实例上创建具有在 **“数据库”** 属性中指定的名称的新模型数据库（如果此数据库尚不存在）。 使用来自该模型项目的 Model.bim 文件的元数据在部署服务器上的模型数据库中配置对象。 使用“处理选项”，你可以指定是否仅部署模型元数据，并且创建模型数据库；或者，如果指定了“默认”或“完全”，则用于连接到数据源的模拟凭据将从模型工作区数据库的内存中传递到已部署的模型数据库中。 Analysis Services 然后运行处理以便将数据填充到已部署的模型中。 一旦完成部署进程后，就可以通过使用数据连接或 SharePoint 中的 .bism 连接文件，将该模型连接到客户端应用程序。  
  
##  <a name="bkmk_deploy_props"></a> 部署属性  
 项目部署选项和部署服务器属性指定如何以及在何处模型部署到过渡或生产 Analysis Services 环境。 在根据您的特定部署要求为所有模型项目定义默认属性设置时，可为每个项目更改这些属性设置。 有关设置部署属性的默认值的详细信息，请参阅[配置默认数据建模和部署属性](../../analysis-services/tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md)。  
  
### <a name="deployment-options-properties"></a>部署选项属性  
 部署选项属性包括：  
  
|属性|默认设置|Description|  
|--------------|---------------------|-----------------|  
|**“处理选项”**|**默认**|此属性指定在部署对对象所做的更改时所需的处理类型。 此属性具有以下选项：<br /><br /> **默认** – 此设置指定 Analysis Services 将确定所需的处理类型。 将处理未处理的对象，如果需要，将重新计算属性关系、属性层次结构、用户层次结构和计算列。 此设置通常会导致比使用“完全”处理选项更快的部署时间。<br /><br /> **不处理** – 此设置指定将仅部署元数据。 在部署后，可能需要对已部署的模型运行处理操作，以便更新和重新计算数据。<br /><br /> **完全** – 此设置指定既部署元数据，又执行“处理全部”操作。 这确保已部署的模型对元数据和数据都具有最新更新。|  
|**事务性部署**|**False**|此属性指定部署是否为事务性的。 默认情况下，在处理这些已部署的对象时，所有对象或已更改对象的部署并不是事务性部署。 即使在处理失败时，部署也会成功并且一直保留。 您可以将此默认设置更改为在单个事务中合并部署和处理。|  
|**查询模式**|**内存中**|此属性指定从其返回查询结果的源是在内存中（缓存）模式下运行还是在 DirectQuery 模式下运行。 此属性具有以下选项：<br /><br /> **DirectQuery** – 此设置指定模型的所有查询都应该仅使用关系数据源。<br /><br /> **DirectQuery 以及内存中** - 此设置指定默认情况下应通过使用关系数据源响应查询，除非在客户端的连接字符串中指定了其他项。<br /><br /> **内存中** - 此设置指定应仅通过使用缓存响应查询。<br /><br /> **内存中以及 DirectQuery** - 此设置指定默认情况下 应该通过使用缓存来响应查询，除非在客户端的连接字符串中指定了其他项。<br /><br /> <br /><br /> 有关详细信息，请参阅[DirectQuery 模式下](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)。|  
  
### <a name="deployment-server-properties"></a>部署服务器属性  
 部署服务器属性包括以下项：  
  
|属性|默认设置|Description|  
|--------------|---------------------|-----------------|  
|**“服务器”**<br /><br /> 在创建项目时设置。|**localhost**|此属性（在创建项目时设置）按名称指定模型将部署到的 Analysis Services 实例。 默认情况下，模型将部署到本地计算机上 Analysis Services 的默认实例。 但是，您可以更改此设置以便指定本地计算机上的命名实例，或指定您有权创建 Analysis Services 对象的任何远程计算机上的任何实例。|  
|**版本**|与工作区服务器所在是实例的版本相同。|此属性指定模型将部署到的 Analysis Services 服务器的版本。 该服务器版本定义可纳入项目中的不同功能。 默认情况下，该版本将为本地 Analysis Services 服务器。 如果您指定其他 Analysis Services 服务器，例如生产 Analysis Services 服务器，则请确保指定该 Analysis Services 服务器的版本。|  
|**数据库**|**\<projectname>**|此属性指定在部署时将实例化的模型对象所处的 Analysis Services 数据库的名称。 该名称也将在报表客户端数据连接或 .bism 数据连接文件中指定。<br /><br /> 您可以在创作模型时随时更改该名称。 如果您在部署了模型后更改该名称，则在部署后进行的更改将不会影响以前已部署的模型。 例如，如果你打开一个名为 **TestDB** 的解决方案并且使用默认的模型数据库名称 Model 部署你的解决方案，然后修改该解决方案并且将模型数据库重命名为 **Sales**，则这些解决方案部署到的 Analysis Services 实例将显示两个单独的数据库，分别命名为 Model 和 Sales。|  
|**多维数据集名称**|**Model**|此属性指定在客户端工具（如 Excel）和 AMO（分析管理对象）中显示的多维数据集名称。|  
  
### <a name="directquery-options-properties"></a>DirectQuery 选项属性  
 部署选项属性包括以下项：  
  
|属性|默认设置|Description|  
|--------------|---------------------|-----------------|  
|**模拟设置**|**默认**|此设置指定在 DirectQuery 模式下运行的模型连接到数据源时使用的模拟设置。 在查询内存中缓存时，将不使用模拟凭据。 此属性设置具有以下选项：<br /><br /> **默认** – 此设置指定 Analysis Services 将使用在通过使用表导入向导创建数据源连接时在模拟信息页上指定的选项。<br /><br /> **ImpersonateCurrentUser** – 此设置指定在连接到所有数据源时当前登录的用户将使用的用户帐户。|  
  
##  <a name="bkmk_meth"></a> 部署方法  
 可使用多种方法来部署表格模型项目。 可用于其他 Analysis Services 项目（如多维）的大多数部署方法也可用于部署表格模型项目。  
  
|方法|Description|链接|  
|------------|-----------------|----------|  
|**SQL Server Data Tools 中的“部署”命令**|“部署”命令提供了一个简单且直观的方法，用于从 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 创作环境部署表格模型项目。<br /><br /> **警告：**不应使用此方法将部署到生产服务器。 使用此方法可以覆盖某些属性在已部署现有模型;例如，当使用脚本或 SSMS 修改属性。|[从 SQL Server Data Tools 进行部署](../../analysis-services/tabular-models/deploy-from-sql-server-data-tools-ssas-tabular.md)|  
|**分析管理对象 (AMO) 自动化**|AMO 提供用于 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的完整命令集的编程接口，包括可用于解决方案部署的命令。 AMO 自动化是最灵活的解决方案部署方法，但是也需要完成一些编程工作。  使用 AMO 的一个重要优势是：可以将 SQL Server 代理用于 AMO 应用程序，以便按预设的计划运行部署。|[使用分析管理对象 & #40; 进行开发AMO & #41;](../../analysis-services/multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md)|  
|**XMLA**|使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 生成现有 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库的元数据的 XMLA 脚本，然后在另一台服务器中运行该脚本以重新创建初始数据库。 通过定义部署过程，然后进行整理并将其保存在 XMLA 脚本中，可以很容易在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中形成 XMLA 脚本。 将 XMLA 脚本保存到文件中以后，即可很容易地按计划运行脚本，或将脚本嵌入直接连接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]实例的应用程序中。<br /><br /> 还可以使用 SQL Server 代理按预置的计划运行 XMLA 脚本，但使用 XMLA 脚本没有 AMO 所具备的灵活性。 AMO 通过驻留完整的管理命令提供了范围更广的功能。|[使用 XMLA 部署模型解决方案](../../analysis-services/multidimensional-models/deploy-model-solutions-using-xmla.md)|  
|**部署向导**|通过部署向导，使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目生成的 XMLA 输出文件，以将项目的元数据部署到目标服务器中。 使用部署向导，可以直接从 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 文件（该文件由项目生成按输出目录创建）进行部署。<br /><br /> 使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的主要优势是部署向导使用方便。 就像您可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中保存 XMLA 脚本以供以后使用一样，可以保存部署向导脚本。 部署向导可以交互运行，也可以通过部署实用工具在命令提示符下运行。|[使用部署向导部署模型解决方案](../../analysis-services/multidimensional-models/deploy-model-solutions-using-the-deployment-wizard.md)|  
|**部署实用工具**|可以使用部署实用工具在命令提示符下启动 Analysis Services 部署引擎。|[使用部署实用工具部署模型解决方案](../../analysis-services/multidimensional-models/deploy-model-solutions-with-the-deployment-utility.md)|  
|**同步数据库向导**|使用同步数据库向导同步任意两个 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库之间的元数据和数据。<br /><br /> 同步向导可用于将数据和元数据从源服务器复制到目标服务器。 如果目标服务器没有要部署的数据库副本，则将新数据库复制到目标服务器。 如果目标服务器已经有相同数据库的副本，则更新目标服务器上的数据库以使用源数据库的元数据和数据。|[同步 Analysis Services 数据库](../../analysis-services/multidimensional-models/synchronize-analysis-services-databases.md)|  
|**备份和还原**|备份为传输 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库提供了最简单的方式。 从 **“备份”** 对话框，可以设置配置选项，然后可以从对话框本身运行备份。 也可以创建可保存并根据需要频繁运行的脚本。<br /><br /> 与其他部署方法相比，备份和还原的使用频率较低，但它能以很小的基础结构要求快速完成部署。|[备份和还原 Analysis Services 数据库](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)|  
  
##  <a name="bkmk_connecting"></a> 配置部署服务器和连接到已部署的模型  
 在已部署某一模型后，还要考虑其他一些注意事项，例如模型数据访问的安全性、备份以及可通过使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]对 Analysis Services 服务器配置的处理操作等方面。 尽管这些属性和配置设置不在本主题的论述范畴内，但它们对于确保您部署的模型数据是安全的、保持数据最新以及为组织内的用户提供有价值的数据分析资源是非常重要的。  
  
 在已部署某一模型并且配置了可选服务器设置后，该模型可以连接到报表客户端应用程序并且可用于浏览和分析模型元数据。 从客户端应用程序连接到已部署的模型数据库不属于本主题的讨论范围。 若要了解从客户端应用程序连接到模型数据库的详细信息，请参阅 [Tabular Model Data Access](../../analysis-services/tabular-models/tabular-model-data-access.md)。  
  
##  <a name="bkmk_rt"></a> Related tasks  
  
|任务|Description|  
|----------|-----------------|  
|[从 SQL Server Data Tools 进行部署](../../analysis-services/tabular-models/deploy-from-sql-server-data-tools-ssas-tabular.md)|介绍如何使用 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中的“部署”命令来配置部署属性和部署表格模型项目。|  
|[使用部署向导部署模型解决方案](../../analysis-services/multidimensional-models/deploy-model-solutions-using-the-deployment-wizard.md)|本节中的主题说明如何使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署向导部署表格和多维模型解决方案。|  
|[使用部署实用工具部署模型解决方案](../../analysis-services/multidimensional-models/deploy-model-solutions-with-the-deployment-utility.md)|说明如何使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署实用工具部署表格和多维模型解决方案。|  
|[使用 XMLA 部署模型解决方案](../../analysis-services/multidimensional-models/deploy-model-solutions-using-xmla.md)|说明如何使用 XMLA 部署 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 表格和多维解决方案。|  
|[同步 Analysis Services 数据库](../../analysis-services/multidimensional-models/synchronize-analysis-services-databases.md)|说明如何使用同步数据库向导同步任意两个 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 表格或多维数据库之间的元数据和数据。|  
  
## <a name="see-also"></a>另请参阅  
 [连接到表格模型数据库 ](../../analysis-services/tabular-models/connect-to-a-tabular-model-database-ssas.md)  
  
  
