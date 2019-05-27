---
title: 添加引用对话框 (Analysis Services-多维数据) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.addreference.f1
- sql12.asvs.bidevstudio.assembly.addassembly.f1
helpviewer_keywords:
- Add Reference dialog box
ms.assetid: 457958c4-6baa-474d-99a0-34c195ceba09
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 541b7371cdc05ee316e9fb9de9f50affc4f14fc7
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66062861"
---
# <a name="add-reference-dialog-box-analysis-services---multidimensional-data"></a>“添加引用”对话框（Analysis Services - 多维数据）
  可以使用 **中的** “添加引用” [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 对话框，在开发项目中添加对 [!INCLUDE[msCoName](../includes/msconame-md.md)] .NET Framework 程序集或其他项目的引用。 通过在**解决方案资源管理器**中右键单击 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 项目的“程序集”文件夹，并从上下文菜单中选择“新建程序集引用”，可以显示“添加引用”对话框。  
  
## <a name="options"></a>选项  
  
|术语|定义|  
|----------|----------------|  
|**.NET**|选择此选项卡可以添加对注册组件的引用。 此选项卡显示一个网格，其中包含已注册的 .NET Framework 组件的列表。 从网格中选择一个或多个项，再单击 **“添加”** ，即可将所选 .NET 组件添加到 **“选定的产品和组件”** 中。 该网格包含以下列：<br /><br /> **组件名称**：组件的全名或“友好”名称。 选择该标题以按组件名称排序。<br /><br /> **版本**：所列的组件版本号。 选择该标题以按版本排序。<br /><br /> **运行时**：组件所基于的 .NET Framework 版本。 选择该标题以按运行时版本排序。<br /><br /> **路径**：组件的文件名及其所在的路径。 选择该标题以按路径排序。|  
|**“浏览”**|单击此选项卡可以在文件系统中浏览未在 **.NET** 或 **“最近”** 选项卡上列出的程序集。 此选项卡显示以下选项：<br /><br /> **查找范围**：从此下拉列表中选择文件夹。 如果在此列表中选择了一个文件夹，则此文件夹的内容将显示在主窗格中。<br /><br /> **转到访问的上一个文件夹**：将“查找范围”返回之前的位置。<br /><br /> **向上一级**：定位到层次结构中下一更高级别的文件夹。<br /><br /> **创建新文件夹**：选择此选项可以在“查找范围”中选择的文件夹下创建新的子文件夹。<br /><br /> **视图菜单**：选择此选项可以更改主窗格中内容的视图。  有关 **“‘视图’菜单”** 中的选项的详细信息，请参阅 [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows 文档中的“查看文件和文件夹概述”主题。 可用选项包括：<br />缩略图<br />平铺<br />图标<br />列表<br />详细信息<br /><br /> **主窗格**:显示中选择的文件夹的内容**查找**。 选择一个或多个项，然后单击**外**若要添加到所选的文件**选定的产品和组件**。 有关主窗格中的选项和上下文菜单的详细信息，请参阅 Windows 文档中的“查看文件和文件夹概述”主题。<br /><br /> **文件名**:使用此选项可以筛选所显示的文件和文件夹。 键入作为筛选依据的完整或部分文件名。 可以使用星号 (\*) 作为通配符。 键入多个文件名（每个文件名用双引号 (") 引起来，并以空格分隔）可以选择多个文件。 通过从下拉列表中选择文件名，还可以选择以前查看过的文件。 提示：可以通过输入 URL 或网络路径中的找到 Web 服务器和网络计算机**文件名**。 例如，输入“http://mywebsite”可显示“mywebsite”Web 位置中可用的文件，输入“\\\myserver\myshare”可显示“myserver”上的“myshare”位置中可用的文件。<br /><br /> **文件类型**:使用此选项以筛选的文件夹或目录中选择的内容**查找**某一特定文件类型。|  
|**最新**|显示在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中最近向项目中添加的组件引用列表。 从网格中选择一个或多个项，再单击 **“添加”** ，即可将选定的 .NET Framework 程序集添加到 **“选定的产品和组件”** 中。 该网格包含以下列：<br /><br /> **组件名称**：组件的全名或“友好”名称。 选择该标题以按组件名称排序。<br /><br /> **版本**：所列的组件版本号。 选择该标题以按版本排序。<br /><br /> **运行时**：组件所基于的 .NET Framework 版本。 选择该标题以按运行时版本排序。<br /><br /> **路径**：组件的文件名及其所在的路径。 选择该标题以按路径排序。|  
|**“添加”**|单击该按钮可以将在 **.NET**、 **“浏览”** 或 **“最近”** 选项卡中选择的组件添加到 **“选定的项目和组件”**。|  
|**删除**|单击该按钮可以删除在 **“选定的项目和组件”** 中选定的组件。|  
|**选定的项目和组件**|显示在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中要添加到 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]项目中的组件引用的列表。 从网格中选择一个或多个项，再单击 **“删除”** ，即可从网格中删除所选组件。 该网格包含以下列：<br /><br /> **组件名称**：组件的全名或“友好”名称。 选择该标题以按组件名称排序。<br /><br /> **版本**：所列的组件版本号。 选择该标题以按版本排序。<br /><br /> **运行时**：组件所基于的 .NET Framework 版本。 选择该标题以按运行时版本排序。<br /><br /> **路径**：组件的文件名及其所在的路径。 选择该标题以按路径排序。|  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 设计器和对话框&#40;多维数据&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [多维模型程序集管理](multidimensional-models/multidimensional-model-assemblies-management.md)  
  
  
