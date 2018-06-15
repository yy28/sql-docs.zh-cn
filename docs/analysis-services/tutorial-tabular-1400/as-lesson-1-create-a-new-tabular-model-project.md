---
title: Analysis Services 教程第 1 课： 创建新的表格模型项目 |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 403e6d04d339e3126afe964bd919304d04295c0b
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34044191"
---
# <a name="create-a-tabular-model-project"></a>创建表格模型项目

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

在本课程中，你使用 Visual Studio 与 SQL Server Data Tools (SSDT) 或与 Microsoft Analysis Services 项目 VSIX 的 Visual Studio 2017 1400年兼容性级别创建新的表格模型项目。 创建新项目后，你可以开始添加数据和创作您的模型。 本课还为你提供了创作环境 Visual Studio 中的表格模型的简要介绍。  
  
学完本课的估计时间：**10 分钟**  
  
## <a name="prerequisites"></a>必要條件

本文是第一课中表格模型创作教程。 若要完成本课程中，有一些你必须具备的就地的几个先决条件。 若要了解详细信息，请参阅[Analysis Services-Adventure Works 教程](../tutorial-tabular-1400/as-adventure-works-tutorial.md)。  
  
## <a name="create-a-new-tabular-model-project"></a>创建新的表格模型项目  
  
#### <a name="to-create-a-new-tabular-model-project"></a>创建新的表格模型项目  
  
1.  在 Visual Studio 中，在**文件**菜单上，单击**新建** > **项目**。  
  
2.  在**新项目**对话框框中，展开**已安装** > **Business Intelligence** > **Analysis Services**，然后单击**Analysis Services 表格项目**。  
  
3.  在**名称**，类型**AW Internet Sales**，然后指定项目文件的位置。  
  
    默认情况下，**解决方案名称**等同于项目名称中; 但是，可以键入不同的解决方案名称。  
  
4.  单击 **“确定”**。  
  
5.  在**表格模型设计器**对话框中，选择**集成的工作区**。  
  
    工作区可容纳在模型创作期间具有与项目相同的名称的表格模型数据库。 集成的工作区意味着 Visual Studio 将使用内置的实例，不再需要安装单独的 Analysis Services 服务器实例只是为了模型创作。
      
6.  在**兼容性级别**，选择**SQL Server 2017 / Azure Analysis Services (1400)**。   
 
    ![as-lesson1-tmd](../tutorial-tabular-1400/media/as-lesson1-tmd.png)
      
    如果看不到 SQL Server 2017 / Azure Analysis Services (1400) 兼容性级别列表框中的，你在不使用最新版本的 SQL Server Data Tools。 若要获取最新版本，请参阅 [安装 SQL Server Data Tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)。  
      
  
## <a name="understanding-the-ssdt-tabular-model-authoring-environment"></a>了解 SSDT 表格模型创作环境  

现在，你已创建新的表格模型项目，让我们花一些时间来浏览表格模型创建 Visual Studio 中的环境。  
  
创建你的项目后，它将在 Visual Studio 中打开。 在右侧，在**表格模型资源管理器**，您的模型中查看对象的树视图。 因为尚未尚未导入数据，则文件夹为空。 您可以右键单击要执行的操作，类似于菜单栏的对象文件夹。 如你逐步完成本教程，你使用表格模型资源管理器模型项目中导航的不同对象。

![as-lesson1-tme](../tutorial-tabular-1400/media/as-lesson1-tme.png)

单击**解决方案资源管理器**选项卡。在这里，你看到你**Model.bim**文件。 如果你看不到左 （与 Model.bim 选项卡的空窗口），设计器窗口中**解决方案资源管理器**下**AW Internet 销售项目**，双击**Model.bim**文件。 Model.bim 文件包含您的模型项目的元数据。 

![作为 lesson1 se](../tutorial-tabular-1400/media/as-lesson1-se.png)
  
单击**Model.bim**。 在**属性**窗口中，您可以看到模型属性，最重要的是**DirectQuery 模式下**属性。 此属性指定是否在内存中模式 （关闭） 或 (On) 的 DirectQuery 模式下部署模型。 对于本教程，你创作和部署的模型中的 In-memory 模式。

![作为 lesson1 属性](../tutorial-tabular-1400/media/as-lesson1-properties.png)
  
当创建模型项目时，可以在中指定的数据建模的设置根据相应某些模型属性自动设置**工具**菜单 >**选项**对话框。 “数据备份”、“工作区保持期”和“工作区服务器”属性指定备份、在内存中保留以及构建工作区数据库（模型创作数据库）的方式和位置。 您可以稍后更改这些设置，如有必要，但现在，因为它们是保留这些属性。  

在**解决方案资源管理器**，右键单击**AW Internet Sales** （项目），然后单击**属性**。 **AW Internet 销售属性页**对话框随即出现。 其中一些属性更高版本时设置部署你的模型。  
  
当安装 SSDT 后时，几个新的菜单项目已添加到 Visual Studio 环境。 单击**模型**菜单。 从这里，你可以导入数据，刷新工作区中数据、 浏览您的模型在 Excel 中，创建透视和角色、 选择模型视图中，并设置计算选项。 单击**表**菜单。 从这里，你可以创建和管理关系、 指定日期表设置、 创建分区，并编辑表属性。 如果你单击**列**菜单上，你可以添加和删除表中的列、 冻结的列，并指定排序顺序。 SSDT 还将一些按钮添加到栏。 最有用，则是自动求和功能，可创建所选列的标准聚合度量值。 其他工具栏按钮可提供对常用功能和命令的快速访问。  
  
了解特定于创作表格模型的不同功能的某些对话框和位置。 在某些项目未尚未处于活动状态，您可以更创作环境的表格模型的一个好主意。  
  

## <a name="whats-next"></a>下一步是什么？

[第 2 课： 获取数据](../tutorial-tabular-1400/as-lesson-2-get-data.md)。

  
  
  
