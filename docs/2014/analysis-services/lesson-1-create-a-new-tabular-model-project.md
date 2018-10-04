---
title: 第 1 课： 创建新的表格模型项目 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 0d2eb34d-78c8-41ff-b92d-49b62c16b2ac
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 873b4cce7a2bd72c74bb7aff3147351b0062eb07
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48124917"
---
# <a name="lesson-1-create-a-new-tabular-model-project"></a>第 1 课：创建新的表格模型项目
  在本课中，您将在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中创建一个新的空白表格模型项目。 创建新项目之后，您可以使用表导入向导开始添加数据。 除了创建新项目之外，本课还简要介绍了 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中的表格模型创作环境。  
  
 若要了解有关不同类型的表格模型项目的详细信息，请参阅[表格模型项目（SSAS 表格）](tabular-models/tabular-model-projects-ssas-tabular.md)。 若要了解有关表格模型创作环境的详细信息，请参阅[表格模型设计器&#40;SSAS 表格&#41;](tabular-model-designer-ssas-tabular.md)。  
  
 学完本课的估计时间： **10 分钟**  
  
## <a name="prerequisites"></a>必要條件  
 本主题是表格模型创作教程中的第一课。 若要完成本课程，您必须在 SQL Server 实例上安装了 AdventureWorksDW 数据库。 有关详细信息，请参阅[表格建模（Adventure Works 教程）](tabular-modeling-adventure-works-tutorial.md)。  
  
## <a name="create-a-new-tabular-model-project"></a>创建新的表格模型项目  
  
#### <a name="to-create-a-new-tabular-model-project"></a>创建新的表格模型项目  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中，在 **“文件”** 菜单上，单击 **“新建”**，然后单击 **“项目”**。  
  
2.  在中**新的项目**对话框中的**已安装的模板**，单击**商业智能**，然后单击**Analysis Services**，和然后单击**Analysis Services 表格项目**。  
  
3.  在中**名称**，类型`AW Internet Sales Tabular Model`，然后指定项目文件的位置。  
  
     默认情况下，“解决方案名称”将与项目名称相同；但可以键入其他解决方案名称。  
  
4.  单击“确定” 。  
  
## <a name="understanding-the-sql-server-data-tools-tabular-model-authoring-environment"></a>了解 SQL Server Data Tools 表格模型创作环境  
 既然您已创建了新的表格模型项目，那么我们花点时间来了解 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]（Visual Studio 2010 或更高版本）中的表格模型创作环境。  
  
 创建了项目后，该项目将在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中打开。 空模型将出现在模型设计器中，并且将在“解决方案资源管理器”窗口中选中“Model.bim”文件。 当您添加数据时，表和列将出现在设计器中。 如果您看不到设计器 （包含 Model.bim 选项卡的空窗口），在**解决方案资源管理器**下`AW Internet Sales Tabular Model`，双击**Model.bim**文件。  
  
 可以在“属性”窗口中查看基本项目属性。 在中**解决方案资源管理器**，单击`AW Internet Sales Tabular Model`。 请注意，在“属性”窗口的“项目文件”中，将看到“AW Internet Sales Tabular Model.smproj”。 这是项目文件名称，并且在“项目文件夹”中，将看到项目文件位置。  
  
 在中**解决方案资源管理器**，右键单击`AW Internet Sales Tabular Model`项目，然后依次**属性**。 “AW Internet Sales Tabular Model Property Pages”对话框将出现。 这些是高级项目属性。 稍后，当您准备好部署模型时，将设置其中一些属性。  
  
 现在，让我们看看模型属性。 在“解决方案资源管理器”中，单击“Model.bim”。 在“属性”窗口中，现在将看到模型属性，其中最重要的是“DirectQuery 模式”属性。 此属性指定是在内存中模式（关闭）还是在 DirectQuery 模式（打开）下部署模型。 对于本教程，您将在内存中模式下创作和部署模型。  
  
 当您创建新模型时，将根据可在“工具\选项”对话框中指定的数据建模设置，自动设置某些模型属性。 “数据备份”、“工作区保持期”和“工作区服务器”属性指定备份、在内存中保留以及构建工作区数据库（模型创作数据库）的方式和位置。 如有必要，您可以稍后更改这些设置，但目前保留这些属性不变。  
  
 当您安装 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 后，将向 Visual Studio 环境中添加若干新菜单项。 让我们看看是特定于创作表格模型的新菜单项。 单击“模型”菜单。 在此，您可以启动表导入向导，查看和编辑现有连接，刷新工作区数据，在 [!INCLUDE[msCoName](../includes/msconame-md.md)] Excel 中使用“在 Excel 中分析”功能浏览模型，创建透视和角色，选择模型视图和设置计算选项。  
  
 单击“表”菜单。 在此，您可以创建和管理表之间的关系，创建、管理和指定日期表设置，创建分区以及编辑表属性。  
  
 单击“列”菜单。 在此，您可以在表中添加和删除列、冻结列以及指定排序顺序。 还可以使用“自动求和”功能为选定列创建标准聚合度量值。 其他工具栏按钮可提供对常用功能和命令的快速访问。  
  
 了解特定于创作表格模型的不同功能的某些对话框和位置。 尽管某些项尚未处于活动状态，但您可以很好地了解表格模型创作环境。  
  
## <a name="next-steps"></a>后续步骤  
 若要继续学习本教程，请转到下一课：[第 2 课：添加数据](lesson-2-add-data.md)。  
  
  
