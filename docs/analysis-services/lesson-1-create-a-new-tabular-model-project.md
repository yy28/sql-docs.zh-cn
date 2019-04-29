---
title: 第 1 课：创建新的表格模型项目 |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 988a091fa7d536386cadd2ed3412213a2e608564
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63052877"
---
# <a name="lesson-1-create-a-new-tabular-model-project"></a>第 1 课：创建新的表格模型项目
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

在本课中，您将在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中创建一个新的空白表格模型项目。 创建新项目之后，您可以使用表导入向导开始添加数据。 本课程还提供了创作环境，在 SSDT 中的表格模型的简要介绍。  
  
估计的时间才能完成本课程中：**10 分钟**  
  
## <a name="prerequisites"></a>先决条件  
本主题是表格模型创作教程中的第一课。 若要完成本课程中，您必须安装 SQL Server 实例上的 AdventureWorksDW 示例数据库。 若要了解详细信息，请参阅[表格建模&#40;Adventure Works 教程&#41;](../analysis-services/tabular-modeling-adventure-works-tutorial.md)。  
  
## <a name="create-a-new-tabular-model-project"></a>创建新的表格模型项目  
  
#### <a name="to-create-a-new-tabular-model-project"></a>创建新的表格模型项目  
  
1.  在 SSDT 中，在**文件**菜单上，单击**新建** > **项目**。  
  
2.  在中**新的项目**对话框框中，展开**已安装** > **商业智能** > **Analysis Services**，然后依次**Analysis Services 表格项目**。  
  
3.  在中**名称**，类型**AW Internet Sales**，然后指定项目文件的位置。  
  
    默认情况下，“解决方案名称”将与项目名称相同；但可以键入其他解决方案名称。  
  
4.  单击“确定” 。  
  
5.  在中**表格模型设计器**对话框中，选择**集成工作区**。  
  
    在工作区将在模型创作期间托管与项目同名的表格模型数据库。 集成工作区表示 SSDT 将使用内置实例，无需单独安装一个 Analysis Services 服务器实例仅仅出于模型创作。 若要了解详细信息，请参阅[工作区数据库](../analysis-services/tabular-models/workspace-database-ssas-tabular.md)。
      
6.  在“兼容级别”中，确认已选中“SQL Server 2016 (1200)”，然后单击“确定”。   
 
    ![as-tabular-lesson1-tmd](../analysis-services/media/as-tabular-lesson1-tmd.png)
      
    如果未在兼容级别列表框中看到 SQL Server 2016 RTM (1200)，则表示使用的不 SQL Server Data Tools 的最新版本。 若要获取最新版本，请参阅 [安装 SQL Server Data Tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)。  

    如果你使用最新版本的 SSDT，你还可以选择 SQL Server 2017 (1400)。 不过，若要完成第 13 课：部署，你将需要将部署到的 SQL Server 2017 或 Azure 服务器。
      
    如果你想将已完成的表格模型部署到运行早期版本的 SQL Server 的不同 Analysis Services 实例，仅建议选择较早的兼容性级别。 更低的兼容性级别不支持集成工作区。 若要了解详细信息，请参阅 [兼容级别](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)。   
  
## <a name="understanding-the-ssdt-tabular-model-authoring-environment"></a>了解 SSDT 表格模型创作环境  
创建新的表格模型项目后，让我们花点时间了解表格模型创作环境在 SSDT 中。  
  
创建项目后，它将在 SSDT 中打开。 在右侧，在**表格模型资源管理器**，将在模型中看到的对象的树视图。 由于你尚未导入数据，因此文件夹是空的。 您可以右键单击某个对象文件夹来执行操作，类似于菜单栏。 在学习本教程中，将使用表格模型资源管理器来浏览模型项目中的不同对象。

![as-tabular-lesson1-tme](../analysis-services/media/as-tabular-lesson1-tme.png)

单击**解决方案资源管理器**选项卡。这里，您将看到你**Model.bim**文件。 如果您看不到左 （包含 Model.bim 选项卡的空窗口），在设计器窗口中**解决方案资源管理器**下**AW Internet Sales 项目**，双击**Model.bim**文件。 Model.bim 文件包含所有模型项目的元数据。 

![as-tabular-lesson1-se](../analysis-services/media/as-tabular-lesson1-se.png)
  
让我们看看模型属性。 单击**Model.bim**。 在中**属性**窗口中，您将看到[模型属性](../analysis-services/tabular-models/model-properties-ssas-tabular.md)，最重要的是**DirectQuery 模式下**属性。 此属性指定是在内存中模式（关闭）还是在 DirectQuery 模式（打开）下部署模型。 对于本教程，您将在内存中模式下创作和部署模型。

![as-tabular-lesson1-properties](../analysis-services/media/as-tabular-lesson1-properties.png)
  
创建新模型时，可以在指定的数据建模设置根据相应某些模型属性自动设置**工具** > **选项**对话框。 “数据备份”、“工作区保持期”和“工作区服务器”属性指定备份、在内存中保留以及构建工作区数据库（模型创作数据库）的方式和位置。 如有必要，您可以稍后更改这些设置，但目前保留这些属性不变。  

在中**解决方案资源管理器**，右键单击**AW Internet Sales** （项目），然后单击**属性**。 **AW Internet Sales 属性页**对话框随即出现。 这些是高级[项目属性](../analysis-services/tabular-models/project-properties-ssas-tabular.md)。 稍后，当您准备好部署模型时，将设置其中一些属性。  
  
安装 SSDT 后，向 Visual Studio 环境中添加若干新菜单项。 让我们看一下专门用于创作表格模型。 单击“模型”菜单。 在这里，您可以启动表导入向导、 查看和编辑现有连接、 刷新工作区数据、 浏览模型中与在 Excel 功能中分析 Excel、 创建透视图和角色、 选择模型视图和设置计算选项。  
  
单击“表”菜单。 在此，您可以创建和管理表之间的关系，创建、管理和指定日期表设置，创建分区以及编辑表属性。  
  
单击“列”菜单。 在此，您可以在表中添加和删除列、冻结列以及指定排序顺序。 还可以使用“自动求和”功能为选定列创建标准聚合度量值。 其他工具栏按钮可提供对常用功能和命令的快速访问。  
  
了解特定于创作表格模型的不同功能的某些对话框和位置。 尽管某些项尚未处于活动状态，但您可以很好地了解表格模型创作环境。  


## <a name="additional-resources"></a>其他资源
若要了解有关不同类型的表格模型项目的详细信息，请参阅[表格模型项目](../analysis-services/tabular-models/tabular-model-projects-ssas-tabular.md)。 若要了解有关表格模型创作环境的详细信息，请参阅[表格模型设计器](../analysis-services/tabular-models/tabular-model-designer-ssas.md)。  
  

## <a name="whats-next"></a>下一步是什么？
请转到下一课：[第 2 课：将数据添加](../analysis-services/lesson-2-add-data.md)。

  
  
  
