---
title: "工作区数据库 (SSAS 表格) |Microsoft 文档"
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 662daf08-a514-44a7-8675-44644aa454a2
caps.latest.revision: 24
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f9a2bcb97d74089651e4c9d1df92561fa298d397
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="workspace-database-ssas-tabular"></a>工作区数据库（SSAS 表格）
  当您在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中创建新的表格模型项目时，将创建在模型创作期间使用的表格模型工作区数据库。
  
## <a name="specifying-a-workspace-instance"></a>指定工作区实例  
  在 SSDT 中创建新的表格模型项目时，可以指定一个 Analysis Services 实例，以便在创作项目时使用。 从 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]的 2016 年 9 月版 (14.0.60918.0) 开始，将引入用于在创建新的表格模型项目时指定工作区实例的两种模式。 

**集成工作区** - 利用 SSDT 自身内部的 Analysis Services 实例。

**工作区服务器** - 在显式 Analysis Services 实例中创建工作区数据库，通常在 SSDT 所在的同一台计算机或同一网络中的另一台计算机上。


  
### <a name="integrated-workspace"></a>集成工作区
通过集成工作区，使用 SSDT 自身的隐式 Analysis Services 实例在内存中创建工作数据库。 集成工作区模式显著降低了在 SSDT 中创作表格项目的复杂性，因为无需单独显式安装 SQL Server Analysis Services。

通过使用集成工作区模式，SSDT 表格在后台动态启动其自身的内部 SSAS 实例，并加载数据库。 可以在模型设计器中添加并查看表、列和数据。 如果添加其他表、列和关系等，则你是在修改工作区数据库。 集成工作区模式不会更改 SSDT 表格与工作区服务器和数据库配合工作的方式。 更改的是 SSDT 表格托管工作区数据库的位置。

在 SSDT 中创建新的表格模型项目时，可以选择集成工作区模式。

![SSAS 集成工作区模式](../../analysis-services/tabular-models/media/ssas-integrated-workspace-mode.png)

通过使用 model.bim 的“工作区数据库”和“工作区服务器”属性，可以在 SSDT 表格托管数据库的位置发现临时数据库的名称和内部 SSAS 实例的 TCP 端口。 只要 SSDT 表格加载了数据库，你就可以使用 SSMS 连接到工作区数据库。 “工作区保持期”设置指定 SSDT 表格将工作区数据库保留在磁盘上，但在关闭模型项目后将不再保留在内存中。 这可确保与始终将模型保留在内存中相比，消耗较少的内存。 如果想要控制这些设置，将“集成工作区模式”属性设置为 False，然后提供显式工作区服务器。 如果导入模型的数据超出了 SSDT 工作站的内存容量，则显式工作区服务器也很合理。

> [!NOTE]  
>  使用集成的工作区模式时，本地的 Analysis Services 实例将为 64 位，SSDT Visual Studio 的 32 位环境中运行时。 如果正连接到特殊数据源，请确保工作站上同时安装了相应数据提供程序的 32 位和 64 位版本。 64 位 Analysis Services 实例需要 64 位提供程序和 32 位版本，才能使用 SSDT 中的表导入向导。

###  <a name="bkmk_overview"></a> 工作区服务器  
 当您在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中使用某个表格模型项目模板创建新的 Business Intelligence 项目时，在“工作区服务器”属性中所指定的 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]实例上创建工作区数据库。 每个表格模型项目将有自己的工作区数据库。 可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 查看 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务器上的工作区数据库。 工作区数据库名称包含项目名称，后跟下划线和用户名、然后是下划线和 GUID。  
  
 在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中打开表格模型项目时，工作区数据库驻留在内存中。 关闭项目时，工作区数据库可能保存在内存中、存储到磁盘并从内存中删除（默认值）或从内存中删除且不存储到磁盘，这由“工作区保持期”属性决定。 有关“工作区保持期”属性的详细信息，请参阅本主题后面的 [工作区数据库属性](#bkmk_ws_prop) 。  
  
 使用表导入向导或使用“复制/粘贴”功能将数据添加到模型项目后，在模型设计器中查看表、列和数据时，即在查看工作区数据库。 如果添加其他表、列和关系等，将更改工作区数据库。  
  
 部署表格模型项目时，在“部署服务器”属性中指定的 Analysis Services 服务器实例上创建部署的模型数据库（基本上是工作区数据库的副本）。 有关“部署服务器”属性的详细信息，请参阅[项目属性（SSAS 表格）](../../analysis-services/tabular-models/project-properties-ssas-tabular.md)。  
  
 模型工作区数据库通常驻留在 localhost 或 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务器的本地命名实例上。 您可以使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的远程实例来承载工作区数据库，但是由于数据查询滞后和其他限制，不推荐使用此配置。 承载工作区数据库的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例最好与 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]在同一计算机上。 创建模型项目的计算机与承载工作区数据库的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的计算机相同可以提高性能。  
  
 远程工作区数据库具有下列限制：  
  
-   查询时可能滞后。  
  
-   “数据备份”属性不能设置为 **“备份到磁盘”**。  
  
-   在使用“从 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 导入”项目模板创建新的表格模型项目时，不能从 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿导入数据。  
  
  > [!IMPORTANT]  
>  模型的兼容级别和工作区服务器必须必须相对应。
  
> [!NOTE]  
>  如果模型中的任一表包含大量行，请考虑在模型创作期间仅导入一部分数据。 通过导入一部分数据，可减少处理时间和消耗的工作区数据库服务器资源。  
  
> [!NOTE]  
>  表导入向导的“选择表和视图”页中的预览窗口、“编辑表属性”对话框和“分区管理器”对话框在数据源级别显示表、列和行，可能不能显示与工作区数据库相同的表、列和行。  
  
  
##  <a name="bkmk_ws_prop"></a> 工作区数据库属性  
 工作区数据库属性包含在模型属性中。 若要查看模型属性，请在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]的 **“解决方案资源管理器”**中，单击 **Model.bim** 文件。 可以使用 **“属性”** 窗口配置模型属性。 工作区数据库特定属性包括：  
  
> [!NOTE]  
>  创建新模型项目时，“集成工作区模式”、“工作区服务器”、“工作区保持期”和“数据备份”属性将应用默认设置。 可以在“数据建模”页上（位于“工具\选项”对话框的“分析服务器”设置中）更改新模型项目的默认设置。 可以在 **“属性”** 窗口中为每个模型项目设置这些属性以及其他属性。 更改默认设置不会应用到已创建的模型项目。 有关详细信息，请参阅[配置默认数据建模和部署属性（SSAS 表格）](../../analysis-services/tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md)。  
  
|属性|默认设置|Description|  
|--------------|---------------------|-----------------|  
|**集成工作区模式**|True、False|如果创建项目时，为工作区数据库选择集成工作区模式，此属性将为 True。 如果创建项目时，选择“工作区服务器”模式，此属性将为 False。 | 
|**工作区数据库**|名称|工作区数据库的名称。 当“集成工作区模式”为“True”时，无法编辑此属性。|  
|**工作区保持期**|从内存中卸载|指定在关闭某一模型项目后将如何保留工作区数据库。 工作区数据库将包含模型元数据和导入的数据。 在某些情况下，工作区数据库可能会非常大并且占用大量内存。 默认情况下，关闭 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中的模型项目时，将从内存中卸载工作区数据库。 在更改此设置时，一定要考虑您的可用内存资源以及计划处理该模型项目的频繁程度。 此属性设置具有以下选项：<br /><br /> **保留在内存中** - 指定在关闭模型项目后将工作区数据库保留在内存中。 此选项将会占用较多内存；但在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中打开某一模型项目时，将会占用较少的资源并且工作区数据库将更快加载。<br /><br /> **从内存中卸载** - 指定将工作区数据库保留在磁盘上，但在关闭模型项目后将不再保留在内存中。 此选项将会占用较少内存；但在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中打开某一模型项目时，必须重新附加工作区数据库；这样会占用更多资源，并且与工作区数据库保留在内存中相比，模型项目的加载速度将更慢。 在内存中资源受到限制或在处理远程工作区数据库时，将使用此选项。<br /><br /> **删除工作区** - 指定从内存中删除工作区数据库，在关闭模型项目后不将工作区数据库保留在磁盘上。 此选项将会占用较少内存和存储空间；但在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中打开某一模型项目时，将会占用附加的资源，并且与工作区数据库保留在内存中或磁盘上相比，模型项目的加载速度将更慢。 只有在偶尔处理模型项目时，才使用此选项。<br /><br /> 可以在“数据建模”页上（位于“工具\选项”对话框的“分析服务器”设置中）更改此属性的默认设置。 当“集成工作区模式”为“True”时，无法编辑此属性。|  
|**工作区服务器**|localhost|此属性指定在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中创作模型项目时将用于承载工作区数据库的默认服务器。 在本地计算机上运行的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的所有可用实例都将包括在列表框中。<br /><br /> 若要指定其他 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务器（在表格模式下运行），请键入服务器名称。 登录的用户必须是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务器上的管理员。<br /><br /> 注意：建议你将本地 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务器指定为工作区服务器。 对于远程服务器上的工作区数据库，不支持从 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 进行导入，数据不能在本地备份，并且在查询过程中用户界面可能会遇到滞后的情况。<br /><br /> 可以在“数据建模”页上（位于“工具\选项”对话框的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 设置中）更改此属性的默认设置。 当“集成工作区模式”为“True”时，无法编辑此属性。|  
  
##  <a name="bkmk_use_ssms"></a> 使用 SSMS 管理工作区数据库  
 可以使用 SQL Server Management Studio (SSMS) 连接到托管工作区数据库的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务器。 通常，无需对工作区数据库进行管理；例外的情况是分离或删除工作区数据库，这必须从 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]执行。 在模型设计器中打开项目时，不要使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 来管理工作区数据库。 这样做可能导致数据丢失。
   
## <a name="see-also"></a>另请参阅  
[模型属性（SSAS 表格）](../../analysis-services/tabular-models/model-properties-ssas-tabular.md) 
  
  

