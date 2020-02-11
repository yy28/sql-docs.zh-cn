---
title: 表格模型设计器（SSAS 表格） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- SQL12.ASVS.BIDTOOLSET.TOPLEVSEMMODUIENTRY.F1
ms.assetid: 45735c57-2a95-4e45-8994-7242df6c9c5f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 223a8a300a4f3000512f8d75dfb7595cb52abc08
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66067829"
---
# <a name="tabular-model-designer-ssas-tabular"></a>表格模型设计器（SSAS 表格）
  表格模型设计器是与 Microsoft [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 2010 或更高版本集成的一部分，它具有专用于开发专业表格模型解决方案的附加项目类型模板。  
  
 本主题的内容：  
  
-   [便利](#bkmk_benefits)  
  
-   [项目模板](#bkmk_proj_temp)  
  
-   [窗口和菜单](#bkmk_wind_men)  
  
-   [Visual Studio 集成](#bkmk_vsint)  
  
##  <a name="bkmk_benefits"></a> 优势  
 在您安装 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]时，用于创建表格模型的新项目模板将添加到可用项目类型中。 在使用这些模板之一创建了新的表格模型项目后，您可以通过使用表格模型设计器工具和向导开始创建模型。  
  
 除了用于创建专业多维和表格模型解决方案的新模板和工具外， [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 环境还提供调试和项目生命周期功能，确保您可以为组织创建功能最强大的 BI 解决方案。 有关 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]的详细信息，请参阅 [Getting Started with Visual Studio](https://go.microsoft.com/fwlink/?LinkId=206389)（Visual Studio 入门）。  
  
##  <a name="bkmk_proj_temp"></a>项目模板  
 在您安装 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]时，以下表格模型项目模板将添加到商业智能项目类型中：  
  
 **Analysis Services 表格项目**  
 此模板可用于创建新的空白表格模型项目。  
  
 **从服务器导入（表格）**  
 此模板可用于通过从 Analysis Services 中的现有表格模型提取元数据，创建新的表格模型项目。  
  
 **从 PowerPivot 导入**  
 此模板用于通过从 [!INCLUDE[ssGeminiClient](../includes/ssgeminiclient-md.md)] 文件提取元数据和数据，创建新的表格模型项目。  
  
> [!NOTE]  
>  表格模型项目要求处于表格模式的 Analysis Services 服务器实例正在本地或网络上运行。  
  
##  <a name="bkmk_wind_men"></a>窗口和菜单  
 
  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 表格模型创建环境包含以下内容：  
  
### <a name="designer-window"></a>设计器窗口  
 通过提供模型的直观表示形式，设计器窗口用于创建表格模型。 当您打开 Model.bim 文件时，该模型将在设计器窗口中打开。 您可以使用两种不同的视图模式在设计器窗口中创建模型：  
  
 **数据视图**  
 数据视图以表格网格格式显示表。 您还可以使用度量值网格（仅为“数据视图”中的每个表显示）定义度量值。  
  
 **图示视图**  
 关系图视图以图形格式显示表以及表之间的关系。 可以筛选列、度量值、层次结构和 KPI，并且可以选择使用定义的透视查看模型。  
  
 可以在这两个视图中的任何一个执行大多数模型创建任务。  
  
### <a name="solution-explorer"></a>解决方案资源管理器  
 “解决方案资源管理器”窗口将该活动解决方案显示为表格模型项目及其关联项的逻辑容器。 模型项目 (.smproj) 只包含一个 References 对象（空）和 Model.bim 文件。 您可以直接从该视图打开项目项进行修改及执行其他管理任务。  
  
 表格模型解决方案通常只包含一个项目，但是，一个解决方案也可以包含其他项目，例如 Integration Services 或 Reporting Services 项目。 您可以添加任意数目的文件，只要这些文件不是表格模型项目文件所属的类型，并且将“生成操作”属性设置为“无”或将“复制到输出”属性设置为“不复制”。  
  
 若要查看解决方案资源管理器，请单击 **“视图”** 菜单，然后单击 **“解决方案资源管理器”**。  
  
### <a name="properties-window"></a>“属性”窗口  
 “属性”窗口列出所选对象的属性。 下列对象具有可以在“属性”窗口中查看和编辑的属性：  
  
-   Model.bim  
  
-   表  
  
-   列  
  
-   度量  
  
 项目属性在“属性”窗口中只显示项目名称和项目文件夹。 项目还具有您可以使用模式属性对话框设置的其他部署选项和部署服务器设置。 若要查看这些属性，请在 **“解决方案资源管理器”** 中右键单击相应的项目，然后单击 **“属性”**。  
  
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
 生成和部署信息显示在“输出”**** 窗口中（还显示在模式进度对话框中）。 若要查看 **“输出”** 窗口，请单击 **“视图”** 菜单，然后单击“输出”。  
  
### <a name="menu-items"></a>菜单项  
 在您安装 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]时，专用于创建表格模型的附加菜单项将添加到 Visual Studio 菜单栏中。 
  **“模型”** 菜单可用于启动数据导入向导、查看现有连接、处理工作区数据以及在 [!INCLUDE[msCoName](../includes/msconame-md.md)] Excel 中浏览模型工作区。 
  **“表”** 菜单用于创建和管理表之间的关系、创建和管理度量值、指定数据表设置、指定计算选项以及指定其他表属性。 使用 **“列”** 菜单，您可以添加和删除表中的列、隐藏和取消隐藏列以及指定其他列属性（例如数据类型和筛选器）。 可以在 **“生成”** 菜单上生成和部署表格模型解决方案。 “复制/粘贴”功能包含在“编辑”**** 菜单中。  
  
 除了这些菜单项之外，还有一些设置添加到了“工具”菜单项上的 Analysis Services 选项中。  
  
### <a name="toolbar"></a>工具栏  
 Analysis Services 工具栏提供了快速轻松访问最常用的模型创建命令的方式。  
  
##  <a name="bkmk_vsint"></a>Visual Studio 集成  
 **源代码管理**  
 Analysis Services 项目与所选的源代码管理插件集成。 如果您将 Visual Studio 配置为使用源代码管理，可以使用解决方案资源管理器中的“签入”/“签出”。 若要配置为使用 Team Foundation Server，请参阅 [为 Visual Studio 配置 Team Foundation 版本控制](https://msdn.microsoft.com/library/ms253064.aspx)。 还支持很多第三方源代码管理插件。  
  
 **字体**  
 表格模型使用 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 环境字体来控制显示的字体。 如果默认 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 字体未能包含您语言所需的所有 Unicode 字符，可能需要更改此字体。 若要更改字体，请单击 **“工具”** 菜单，单击 **“选项”**，然后单击 **“字体和颜色”**。  
  
 **键盘快捷方式**  
 Analysis Services 键盘快捷键可以通过“工具”->“选项”->“键盘”对话框进行配置/重新映射。 一些全局 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 快捷方式（如生成、保存、调试、新建项目等）在表格模型设计器上下文中受支持。 Analysis Services 上下文中支持其他表格模型设计器的特定快捷键。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;SSAS 表格&#41;的表格模型项目](tabular-models/tabular-model-projects-ssas-tabular.md)   
 [SSAS 表格&#41;&#40;属性](tabular-models/properties-ssas-tabular.md)  
  
  
