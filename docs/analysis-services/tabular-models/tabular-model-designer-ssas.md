---
title: SQL Server Data Tools 中的表格模型设计器 |Microsoft 文档
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 98c836650ef00b283718ddf22834f7e4d4a56e0f
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="tabular-model-designer"></a>表格模型设计器
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
表格模型设计器是 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]的一部分（与 Microsoft [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]集成），它具有专用于开发专业表格模型解决方案的附加项目类型模板。  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 作为免费 Web 下载内容安装。 有关详细信息，请参阅[下载 SQL Server Data Tools (SSDT)](../../ssdt/download-sql-server-data-tools-ssdt.md)。    
  
##  <a name="bkmk_benefits"></a> 优点  
 在您安装 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]时，用于创建表格模型的新项目模板将添加到可用项目类型中。 在使用这些模板之一创建了新的表格模型项目后，您可以通过使用表格模型设计器工具和向导开始创建模型。  
  
 除了用于创建专业多维和表格模型解决方案的新模板和工具外， [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 环境还提供调试和项目生命周期功能，确保您可以为组织创建功能最强大的 BI 解决方案。 有关 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]的详细信息，请参阅 [Getting Started with Visual Studio](http://go.microsoft.com/fwlink/?LinkId=206389)（Visual Studio 入门）。  
  
##  <a name="bkmk_proj_temp"></a> 项目模板  
 在您安装 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]时，以下表格模型项目模板将添加到商业智能项目类型中：  
  
 **Analysis Services 表格项目**  
 此模板可用于创建新的空白表格模型项目。 兼容性级别是在你创建项目时进行指定。
  
 **从服务器导入（表格）**  
 此模板可用于通过从 Analysis Services 中的现有表格模型提取元数据，创建新的表格模型项目。  
  
 旧模型的兼容性级别也较旧。 你可以通过在导入模型定义后更改兼容性级别的属性进行升级。  
  
 **导入自 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]**  
 此模板用于通过从 [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)] 文件提取元数据和数据，创建新的表格模型项目。  
  
##  <a name="bkmk_wind_men"></a> 窗口和菜单  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 表格模型创建环境包含以下内容：  
  
### <a name="designer-window"></a>设计器窗口  
 通过提供模型的直观表示形式，设计器窗口用于创建表格模型。 当您打开 Model.bim 文件时，该模型将在设计器窗口中打开。 您可以使用两种不同的视图模式在设计器窗口中创建模型：  
  
 **数据视图**  
 数据视图以表格网格格式显示表。 您还可以使用度量值网格（仅为“数据视图”中的每个表显示）定义度量值。  
  
 **图示视图**  
 关系图视图以图形格式显示表以及表之间的关系。 可以筛选列、度量值、层次结构和 KPI，并且可以选择使用定义的透视查看模型。  
  
 可以在这两个视图中的任何一个执行大多数模型创建任务。  
  
### <a name="view-code-window"></a>查看代码窗口  
 可以在解决方案资源管理器中右键单击文件并选择“查看代码”，查看 Model.bim 文件的后台代码。 对于在兼容级别 1200年或更高版本的表格模型，模型定义是 JSON 表示方式。  
  
 请注意，你需要包含 JSON 编辑器的完整版 Visual Studio。 如果你不需要商业版中的附加功能，可以下载并安装 [免费版 Visual Studio Community](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx) 。  
  
### <a name="solution-explorer"></a>解决方案资源管理器  
 “解决方案资源管理器”窗口将该活动解决方案显示为表格模型项目及其关联项的逻辑容器。 模型项目 (.smproj) 只包含一个 References 对象（空）和 Model.bim 文件。 您可以直接从该视图打开项目项进行修改及执行其他管理任务。  
  
 表格模型解决方案通常只包含一个项目，但是，一个解决方案也可以包含其他项目，例如 Integration Services 或 Reporting Services 项目。 您可以添加任意数目的文件，只要这些文件不是表格模型项目文件所属的类型，并且将“生成操作”属性设置为“无”或将“复制到输出”属性设置为“不复制”。  
  
 若要查看解决方案资源管理器，请单击 **“视图”** 菜单，然后单击 **“解决方案资源管理器”**。  

### <a name="tabular-model-explorer"></a>表格模型资源管理器
  第一个可用在 2016 年 8 月版本 (14.0.60812.0) 的[SQL Server Data Tools](https://msdn.microsoft.com/mt186501)，表格模型资源管理器可帮助你导航表格模型中的元数据对象。

 若要显示表格模型资源管理器，请单击“视图” > “其他窗口”，然后单击“表格模型资源管理器”。
   
  ![表格模型资源管理器](../../analysis-services/tabular-models/media/tabular-model-explorer.png) 
  
 表格模型资源管理器将元数据对象组织到树状结构非常相似的表格模型的架构。 数据源、透视、关系、角色、表和转换对应于顶层架构对象。 有一些例外情况，尤其是 KPI 和度量值，从技术上讲它们不是顶层对象，而是模型中各个表的子对象。 但是，具有所有 KPI 和度量值的合并的顶级容器可以更轻松地使用这些对象，尤其当模型包含大量表的时候。 度量值也在其相应的父表下面列出，因此具有实际父子关系的清晰视图。 如果在顶级的度量值容器中选择一个度量值，则在子集合中其表下面也会选中同一个度量值，反之亦然。  
 
 表格模型资源管理器中的对象节点链接到相应的菜单选项，到目前为止这些菜单选项隐藏在 Visual Studio 中的模型、表和列菜单下。 可以右键单击对象浏览该对象类型的选项。 并非所有对象节点类型都有上下文菜单，但是将在后续版本中推出其他选项和改进。 

 表格模型资源管理器还具有方便的搜索功能。 只需在搜索框中键入部分名称，表格模型资源管理器就会将树视图缩小至匹配项范围。 
  
### <a name="properties-window"></a>屬性視窗  
 “属性”窗口列出所选对象的属性。 下列对象具有可以在“属性”窗口中查看和编辑的属性：  
  
-   Model.bim  
  
-   表  
  
-   列  
  
-   度量值  
  
 项目属性在属性窗口中显示的项目名称和项目文件夹。 项目还具有您可以使用模式属性对话框设置的其他部署选项和部署服务器设置。 若要查看这些属性，请在 **“解决方案资源管理器”**中右键单击相应的项目，然后单击 **“属性”**。  
  
 “属性”窗口的字段中嵌入了控件，单击这些控件便可将其打开。 编辑控件的类型取决于具体属性。 控件包括编辑框、下拉列表和指向自定义对话框的链接。 灰显的属性为只读属性。  
  
 若要查看 **“属性”** 窗口，请单击 **“视图”** 菜单，然后单击 **“属性窗口”**。  
  
### <a name="error-list"></a>错误列表  
 “错误列表”窗口包含有关模型状态的消息：  
  
-   有关安全最佳实践的通知  
  
-   数据处理要求。  
  
-   有关角色的计算列、度量值和行筛选器的语义错误信息。 对于计算列，可以双击该错误消息来导航到错误的源。  
  
-   DirectQuery 验证错误。  
  
 默认情况下，将不显示 **“错误列表”** ，除非返回一个错误。 不过可以随时查看 **“错误列表”** 窗口。 若要查看 **“错误列表”** 窗口，请单击 **“视图”** 菜单，然后单击 **“错误列表”**。  
  
### <a name="output"></a>输出  
 生成和部署信息显示在“输出”窗口中（还显示在模式进度对话框中）。 若要查看 **“输出”** 窗口，请单击 **“视图”** 菜单，然后单击“输出”。  
  
### <a name="menu-items"></a>菜单项  
 在您安装 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]时，专用于创建表格模型的附加菜单项将添加到 Visual Studio 菜单栏中。 **“模型”** 菜单可用于启动数据导入向导、查看现有连接、处理工作区数据以及在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel 中浏览模型工作区。 **“表”** 菜单用于创建和管理表之间的关系、创建和管理度量值、指定数据表设置、指定计算选项以及指定其他表属性。 使用 **“列”** 菜单，您可以添加和删除表中的列、隐藏和取消隐藏列以及指定其他列属性（例如数据类型和筛选器）。 可以在 **“生成”** 菜单上生成和部署表格模型解决方案。 “复制/粘贴”功能包含在“编辑”菜单中。  
  
 除了这些菜单项之外，还有一些设置添加到了“工具”菜单项上的 Analysis Services 选项中。  
  
### <a name="toolbar"></a>工具栏  
 Analysis Services 工具栏提供了快速轻松访问最常用的模型创建命令的方式。  
  
##  <a name="bkmk_vsint"></a> Visual Studio 集成  
 **源代码管理**  
 Analysis Services 项目与所选的源代码管理插件集成。 如果您将 Visual Studio 配置为使用源代码管理，可以使用解决方案资源管理器中的“签入”/“签出”。 若要配置为使用 Team Foundation Server，请参阅 [为 Visual Studio 配置 Team Foundation 版本控制](http://msdn.microsoft.com/library/ms253064.aspx)。 还支持很多第三方源代码管理插件。  
  
 **字体**  
 表格模型使用 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 环境字体来控制显示的字体。 如果默认 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 字体未能包含您语言所需的所有 Unicode 字符，可能需要更改此字体。 若要更改字体，请单击 **“工具”** 菜单，单击 **“选项”**，然后单击 **“字体和颜色”**。  
  
 **键盘快捷键**  
 Analysis Services 键盘快捷键可以通过“工具”->“选项”->“键盘”对话框进行配置/重新映射。 一些全局 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 快捷方式（如生成、保存、调试、新建项目等）在表格模型设计器上下文中受支持。 Analysis Services 上下文中支持其他表格模型设计器的特定快捷键。  
  
## <a name="see-also"></a>另请参阅  
 [表格模型项目](../../analysis-services/tabular-models/tabular-model-projects-ssas-tabular.md)   
  
  
