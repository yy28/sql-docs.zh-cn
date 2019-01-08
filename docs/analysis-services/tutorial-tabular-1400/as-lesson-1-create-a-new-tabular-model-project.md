---
title: Analysis Services 教程第 1 课：创建新的表格模型项目 |Microsoft Docs
ms.date: 08/27/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9135df30afcec9bdae307d9b12aec6810baa98ec
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2018
ms.locfileid: "52417228"
---
# <a name="create-a-tabular-model-project"></a>创建表格模型项目

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

在本课中，您使用 Visual Studio 使用 SQL Server Data Tools (SSDT) 或与 Microsoft Analysis Services 项目 VSIX 的 Visual Studio 2017 在 1400年兼容级别创建新的表格模型项目。 创建新项目后，可以开始添加数据和创作模型。 本课程还提供了创作环境，在 Visual Studio 中的表格模型的简要介绍。  
  
学完本课的预计时间：**10 分钟**  
  
## <a name="prerequisites"></a>先决条件

本文是表格模型创作教程的第一课。 若要完成本课程中，有多个所需满足的先决条件。 若要了解详细信息，请参阅[Analysis Services-Adventure Works 教程](../tutorial-tabular-1400/as-adventure-works-tutorial.md)。  
  
## <a name="create-a-new-tabular-model-project"></a>创建新的表格模型项目  
  
#### <a name="to-create-a-new-tabular-model-project"></a>创建新的表格模型项目  
  
1.  在 Visual Studio 中，在**文件**菜单上，单击**新建** > **项目**。  
  
2.  在中**新的项目**对话框框中，展开**已安装** > **商业智能** > **Analysis Services**，然后依次**Analysis Services 表格项目**。  
  
3.  在中**名称**，类型**AW Internet Sales**，然后指定项目文件的位置。  
  
    默认情况下**解决方案名称**相同项目名中; 但是，可以键入不同的解决方案名称。  
  
4.  单击“确定” 。  
  
5.  在中**表格模型设计器**对话框中，选择**集成工作区**。  
  
    工作区在模型创作期间托管与项目同名的表格模型数据库。 集成工作区表示 Visual Studio 将使用内置实例，无需单独安装一个 Analysis Services 服务器实例仅仅出于模型创作。
      
6.  在中**兼容性级别**，选择**SQL Server 2017 / Azure Analysis Services (1400)**。   
 
    ![as-lesson1-tmd](../tutorial-tabular-1400/media/as-lesson1-tmd.png)
      
    如果看不到 SQL Server 2017 / Azure Analysis Services (1400) 兼容性级别列表框中的，则表示使用的不 SQL Server Data Tools 的最新版本。 若要获取最新版本，请参阅 [安装 SQL Server Data Tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)。  
      
  
## <a name="understanding-the-ssdt-tabular-model-authoring-environment"></a>了解 SSDT 表格模型创作环境  

创建新的表格模型项目后，让我们花点时间了解表格模型创作环境，在 Visual Studio 中。  
  
创建项目后，它将在 Visual Studio 中打开。 在右侧，在**表格模型资源管理器**，对象的树视图显示了模型中。 由于你尚未导入数据，因此文件夹是空的。 您可以右键单击某个对象文件夹来执行操作，类似于菜单栏。 在学习本教程中，使用表格模型资源管理器来浏览模型项目中的不同对象。

![as-lesson1-tme](../tutorial-tabular-1400/media/as-lesson1-tme.png)

单击**解决方案资源管理器**选项卡。在这里，请参阅你**Model.bim**文件。 如果您看不到左 （包含 Model.bim 选项卡的空窗口），在设计器窗口中**解决方案资源管理器**下**AW Internet Sales 项目**，双击**Model.bim**文件。 Model.bim 文件包含您的模型项目的元数据。 

![作为 lesson1 se](../tutorial-tabular-1400/media/as-lesson1-se.png)
  
单击**Model.bim**。 在中**属性**窗口中，您可以看到模型属性，最重要的是**DirectQuery 模式下**属性。 此属性指定是否在内存中模式 （关闭） 或 DirectQuery 模式 （打开） 中部署模型。 对于本教程，创作并部署在内存中模式下模型。

![作为 lesson1 属性](../tutorial-tabular-1400/media/as-lesson1-properties.png)
  
当您创建某一模型项目时，可以在指定的数据建模设置根据相应某些模型属性自动设置**工具**菜单 >**选项**对话框。 “数据备份”、“工作区保持期”和“工作区服务器”属性指定备份、在内存中保留以及构建工作区数据库（模型创作数据库）的方式和位置。 您可以稍后更改这些设置，如有必要，但现在，将这些属性保留原样。  

在中**解决方案资源管理器**，右键单击**AW Internet Sales** （项目），然后单击**属性**。 **AW Internet Sales 属性页**对话框随即出现。 稍后，设置这些属性的一些部署模型时。  
  
安装 SSDT 后，向 Visual Studio 环境中添加若干新菜单项。 单击**模型**菜单。 在这里，您可以导入数据、 刷新工作区数据、 浏览您在 Excel 中的模型、 创建透视图和角色、 选择模型视图和设置计算选项。 单击**表**菜单。 在这里，您可以创建和管理关系、 指定日期表设置、 创建分区，和编辑表属性。 如果单击**列**菜单中，可以添加和删除表中的列、 冻结列，以及指定排序顺序。 SSDT 还会在栏添加一些按钮。 最有用的是用于创建所选列的标准聚合度量值的自动求和功能。 其他工具栏按钮可提供对常用功能和命令的快速访问。  
  
了解特定于创作表格模型的不同功能的某些对话框和位置。 尽管某些项尚不活动状态，就可以清楚地了解表格模型创作环境。  
  

## <a name="whats-next"></a>下一步是什么？

[第 2 课：获取数据](../tutorial-tabular-1400/as-lesson-2-get-data.md)。

  
  
  
