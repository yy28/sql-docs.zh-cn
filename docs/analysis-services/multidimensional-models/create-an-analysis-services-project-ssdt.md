---
title: "创建 Analysis Services 项目 (SSDT) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- templates [Analysis Services]
- templates [Analysis Services], projects
- projects [Analysis Services], creating
- projects [Analysis Services], Business Intelligence Development Studio
- Business Intelligence Development Studio, defining projects [Analysis Services]
- items [Analysis Services]
ms.assetid: d00913b0-cd6d-4de0-a1e7-4ce86fcc078d
caps.latest.revision: "37"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 366c0e4f2a3238ac9e2552553f1492b9a41b46e7
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="create-an-analysis-services-project-ssdt"></a>创建 Analysis Services 项目 (SSDT)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]你可以定义[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]项目中[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]通过使用[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]项目模板或通过使用导入[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]数据库向导可以读取的内容[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]数据库。 如果 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中当前未加载解决方案，则创建新的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目的同时将自动创建一个新的解决方案。 否则，新的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目将添加到现有的解决方案中。 针对解决方案开发的最佳做法要求为不同类型的应用程序数据创建单独的项目，并且在项目相关时使用单个解决方案。 例如，您可能具有单个解决方案，该解决方案为 Integration Services 包、Analysis Services 数据库和 Reporting Services 报表包含不同的项目，它们全都由相同的业务应用程序使用。  
  
 Analysis Services 项目包含在单个 Analysis Services 数据库中使用的对象。 项目的部署属性指定服务器以及项目元数据部署为实例化对象时采用的数据库名称。  
  
 本主题包含以下各节：  
  
 [使用 Analysis Services 项目模板创建新项目](#bkmk_NewUsingTemplate)  
  
 [使用现有的 Analysis Services 数据库创建新项目](#bkmk_NewUsingWizard)  
  
 [将 Analysis Services 项目添加到现有解决方案中](#bkmk_AddtoExistingSolution)  
  
 [生成和部署场解决方案](#bkmk_buildDeploy)  
  
 [Analysis Services 项目文件夹](#bkmk_ProjectFolders)  
  
 [Analysis Services 文件类型](#bkmk_FileTypes)  
  
 [Analysis Services 项模板](#bkmk_ItemTemplates)  
  
##  <a name="bkmk_NewUsingTemplate"></a> 使用 Analysis Services 项目模板创建新项目  
 使用这些说明可以创建一个空的项目，您可在其中定义 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象，然后将它们作为新的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库部署。  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，单击 **“文件”**，指向 **“新建”**，然后单击 **“项目”**。 在 **“新建项目”** 对话框的 **“项目类型”** 窗格中，选择 **“商业智能项目”**。  
  
2.  在 **“新建项目”** 对话框的 **“Visual Studio 已安装的模板”** 类别中，选择 **“Analysis Services 项目”**。  
  
3.  在 **“名称”** 文本框中，键入项目的名称。 您输入的名称将用作默认数据库名称。  
  
4.  在“位置”下拉列表中，键入或选择用于存储项目文件的文件夹，或单击“浏览”选择一个文件夹。  
  
5.  若要将新项目添加到现有解决方案，请在“解决方案”下拉列表中选择“添加到解决方案”。  
  
     — 或 —  
  
     若要创建新的解决方案，请在“解决方案”下拉列表中选择“创建新解决方案”。 若要为新解决方案创建新的文件夹，请选择 **“创建解决方案的目录”**。 在 **“解决方案名称”**中，键入新解决方案的名称。  
  
6.  单击“确定” 。  
  
##  <a name="bkmk_NewUsingWizard"></a> 使用现有的 Analysis Services 数据库创建新项目  
 使用导入 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库向导可以基于现有 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库中的对象创建项目。 在基于现有的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库定义 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目时，此数据库的元数据将在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]项目中打开。 可以在项目中修改这些对象，而不会影响原始对象，然后可以将这些对象部署到相同的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库（如果部署属性指定该数据库）或部署到新创建的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库以进行比较测试。 直到部署更改之后，所做的更改才会影响现有的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库。  
  
 还可以使用导入 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库模板从生产数据库创建项目，自部署完原始 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目后已直接对此生产数据库进行了更改。  
  
 在您处理或部署项目之前，可能需要更改在数据源中指定的数据访问接口。 如果您所使用的 SQL Server 软件比用于创建数据库的软件更新，则在您的项目中指定的数据访问接口可能未安装在您的计算机上。 在处理过程中，将使用服务帐户检索您的 Analysis Services 数据库中的数据。 如果该数据库位于远程服务器上，则检查本地服务是否对该服务器具有处理和读取权限。  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，单击 **“文件”**，指向 **“新建”**，然后单击 **“项目”**。 在 **“新建项目”** 对话框的 **“项目类型”** 窗格中，选择 **“商业智能项目”**。  
  
2.  在 **“新建项目”** 对话框的 **“Visual Studio 已安装的模板”** 类别中，选择 **“导入 Analysis Services 数据库”**。  
  
3.  为项目和解决方案输入属性信息，包括文件的名称和位置。 单击“确定” 。  
  
4.  在 **“欢迎使用导入 Analysis Services 数据库向导”** 页上，单击 **“下一步”**。  
  
5.  在 **“源数据库”** 页上，指定向导将从中提取内容并创建 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目的服务器和数据库，再单击 **“下一步”**。  
  
     支持的数据库包括在以下版本的 Analysis Services 中创建的那些数据库： [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]、 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]和 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]。  
  
     可以键入数据库名称，也可以查询服务器以查看服务器上的现有数据库。 如果该数据库位于远程服务器或生产服务器上，则您可能需要请求用于读取数据库的权限。 防火墙配置设置可以进一步限制对数据库的访问。 如果在尝试连接到数据库时遇到了错误，则首先检查权限和防火墙设置。  
  
6.  当向导完成 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库的内容提取后，在 **“完成向导”** 页上单击 **“完成”** 。  
  
7.  打开“解决方案资源管理器”窗口查看项目内容。  
  
##  <a name="bkmk_AddtoExistingSolution"></a> 将 Analysis Services 项目添加到现有解决方案中  
 如果您已具有包含某一业务应用程序的所有源文件的解决方案，则可以将新的 Analysis Services 项目添加到该解决方案。  
  
 将现有项目添加到某一解决方案会将该项目与该解决方案相关联，但不是复制。 如果该 Analysis Services 项目已在其他解决方案中创建，则项目文件将与用于创建它的原始解决方案一起保留。 这意味着，您通过任何一个解决方案对项目进行的任何更改都将作用于同一组源文件。 如果此行为并非您的预期行为，则应该首先将项目文件复制或移动到新的解决方案文件夹，然后将项目添加到该解决方案。  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中打开该解决方案。 在解决方案资源管理器中，右键单击该解决方案，指向“添加”，然后单击“现有项目”以选择要添加的项目。  
  
2.  选择要添加到解决方案的 .dwproj 文件。  
  
##  <a name="bkmk_buildDeploy"></a> 生成和部署场解决方案  
 默认情况下， [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 将项目部署到本地计算机上的默认 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例。 您可以使用 **项目的** “属性页” [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对话框更改此部署目标，进而更改 **“服务器”** 配置属性。  
  
> [!NOTE]  
>  默认情况下，在部署解决方案时， [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 仅处理由部署脚本更改的对象以及相关对象。 您可以使用 **项目的** “属性页” [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对话框更改此功能，进而更改“处理选项”配置属性。  
  
 生成解决方案并将它部署到一个 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例以进行测试。 生成解决方案将验证项目中的对象定义和依赖关系并生成一个部署脚本。 部署解决方案将使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署引擎将该部署脚本发送到一个指定的实例。  
  
 在部署项目后，查看和测试已部署的数据库。 然后，您可以修改对象定义，生成并再次部署，直至项目完成。  
  
 在项目完成后，您可以使用部署向导来将生成解决方案时生成的部署脚本部署到目标实例以进行测试、临时处理和部署。  
  
##  <a name="bkmk_ProjectFolders"></a> Analysis Services 项目文件夹  
 每个 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目都包含下列文件夹，这些文件夹用于组织项目中的项。  
  
|文件夹|Description|  
|------------|-----------------|  
|“数据源”|包含了 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目的数据源。 您可以使用数据源向导创建这些对象并可在数据源设计器中对其进行编辑。|  
|数据源视图|包含了 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目的数据源视图。 您可以使用数据源视图向导创建这些对象并可在数据源视图设计器中对其进行编辑。|  
|多维数据集|包含了 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目的多维数据集。 您可以使用多维数据集向导创建这些对象并可在多维数据集设计器中对其进行编辑。|  
|维度|包含了 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目的维度。 您可以使用维度向导创建这些对象并可在维度设计器中对其进行编辑。|  
|挖掘结构|包含了 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目的挖掘结构。 您可以使用挖掘模型向导创建这些对象并可在挖掘模型设计器中对其进行编辑。|  
|角色|包含了 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目的数据库角色。 您可以在角色设计器中创建和管理角色。|  
|程序集|包含了 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 项目对 COM 库和 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .NET Framework 程序集的引用。 您可以使用 **“添加引用”** 对话框来创建引用。|  
|杂项|包含了 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 文件类型以外的任何其他类型文件。 使用此文件夹可以添加所有杂项文件，例如包含项目注释的文本文件。|  
  
##  <a name="bkmk_FileTypes"></a> Analysis Services 文件类型  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 解决方案可以包含多种文件类型，具体取决于解决方案中包括的项目以及解决方案的各个项目中包括的项。 通常， [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 解决方案中各项目的文件都存储在解决方案文件夹中，每个项目各有单独的文件夹。  
  
> [!NOTE]  
>  将某个对象的文件复制到一个项目文件夹不会将该对象添加到该项目。 您必须在 **中使用项目的上下文菜单中的** “添加” [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 命令来将现有的对象定义添加到项目中。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目的项目文件夹可以包含下表中列出的文件类型。  
  
|文件类型|Description|  
|---------------|-----------------|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目定义文件 (.dwproj)|包含了有关 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目中定义和包含的项、配置和程序集引用的元数据。|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目用户设置 (.dwproj.user)|包含了特定用户的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目配置信息。|  
|数据源文件 (.ds)|包含了用于定义数据源的元数据的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 脚本语言 (ASSL) 元素。|  
|数据源视图文件 (.dsv)|包含了用于定义数据源视图的元数据的 ASSL 元素。|  
|多维数据集文件 (.cube)|包含了用于定义多维数据集（包括度量值组、度量值和多维数据集维度）的元数据的 ASSL 元素。|  
|分区文件 (.partitions)|包含了用于定义特定多维数据集的分区的元数据的 ASSL 元素。|  
|维度文件 (.dim)|包含了用于定义数据库维度的元数据的 ASSL 元素。|  
|挖掘结构文件 (.dmm)|包含了用于定义挖掘结构和相关挖掘模型的元数据的 ASSL 元素。|  
|数据库文件 (.database)|包含了用于定义数据库的元数据（包括帐户类型、翻译和数据库权限）的 ASSL 元素。|  
|数据库角色文件 (.role)|包含了用于定义数据库角色（包括角色成员）的元数据的 ASSL 元素。|  
  
##  <a name="bkmk_ItemTemplates"></a> Analysis Services 项模板  
 在使用 **“添加新项”** 对话框向 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目添加新项时，您可以选择使用项模板，项模板是演示如何执行指定操作的一个预定义脚本或语句。  
  
 下表中列出的项模板可从 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] “添加新项” **对话框的** 项目项类别中获得。  
  
|类别|项模板|Description|  
|--------------|-------------------|-----------------|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目项|多维数据集|启动多维数据集向导以向 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目添加一个新的多维数据集。|  
||数据源|启动数据源向导以向 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目添加一个新的数据源。|  
||数据源视图|启动数据源视图向导以向 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目添加一个新的数据源视图。|  
||数据库角色|向 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目添加一个新数据库角色，然后为此新数据库角色显示角色设计器。|  
||维度|启动维度向导以向 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目添加一个新的数据库维度。|  
||挖掘结构|启动数据挖掘向导以向 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目添加一个新挖掘结构及关联的挖掘模型。|  
  
## <a name="see-also"></a>另请参阅  
 [配置 Analysis Services 项目属性 (SSDT)](../../analysis-services/multidimensional-models/configure-analysis-services-project-properties-ssdt.md)   
 [生成 Analysis Services 项目 (SSDT)](../../analysis-services/multidimensional-models/build-analysis-services-projects-ssdt.md)   
 [部署 Analysis Services 项目 (SSDT)](../../analysis-services/multidimensional-models/deploy-analysis-services-projects-ssdt.md)  
  
  
