---
title: MDX 查询编辑器 (Analysis Services-多维数据) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.startpage.mdx.f1
helpviewer_keywords:
- Query Editor [MDX]
- MDX Query Editor
ms.assetid: 777f2c23-1c1c-4b72-9d19-48a4866551f8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f9c47ca70b7637096a18332866ba42561e2dd729
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62727993"
---
# <a name="mdx-query-editor-analysis-services---multidimensional-data"></a>MDX 查询编辑器（Analysis Services - 多维数据）
  可以使用 MDX 查询编辑器，设计和执行使用多维表达式 (MDX) 语言编写的语句和脚本。  
  
## <a name="features"></a>功能  
  
-   在 MDX 查询编辑器的查询编辑器窗格中键入脚本。  
  
-   若要执行脚本，请按 **F5**，或者在工具栏上单击 **“执行”** ，也可以在 **“查询”** 菜单上单击 **“执行”**。 如果选择了一部分代码，则只执行该部分代码。 如果没有选择任何代码，则执行 MDX 查询编辑器的全部内容。  
  
-   在元数据窗格中查看 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库中所包含的多维数据集和其他对象的元数据。  
  
-   有关 MDX 语法的帮助，请在 MDX 查询编辑器中选择关键字，再按 **F1**。  
  
-   有关 MDX 语法的动态帮助，请在 **“帮助”** 菜单上单击 **“动态帮助”**，打开动态帮助组件。 如果使用动态帮助，当在查询编辑器中键入关键字时，帮助主题将显示在 **“动态帮助”** 窗口中。  
  
## <a name="sql-server-analysis-services-editors-toolbar"></a>SQL Server Analysis Services 编辑器工具栏  
 在打开 MDX 查询编辑器时，会出现 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 编辑器工具栏，此工具栏包含下表所列按钮。  
  
|术语|定义|  
|----------|----------------|  
|**“连接”**|打开 **“连接到服务器”** 对话框，以便与 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例建立连接。|  
|**断开连接**|断开 MDX 查询编辑器与 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例之间的连接。|  
|**更改连接**|打开 **“连接到服务器”** 对话框，以便与其他 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例建立连接。|  
|**使用当前连接新建查询**|使用当前“MDX 查询编辑器”窗口的连接信息，打开新的“MDX 查询编辑器”窗口。|  
|**可用数据库**|将连接更改到同一实例上的其他 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库。|  
|**执行**|执行所选的代码，如果没有选择任何代码，则执行 MDX 查询编辑器中的全部代码。|  
|**分析**|检查所选代码的语法。 如果没有选择任何代码，则检查整个“MDX 查询编辑器”窗口的语法。|  
|**取消执行查询**|向服务器发送取消请求。 有些查询不能立即取消，而必须等待适当的取消条件。 如果取消查询，在回滚事务时可能发生延迟。|  
  
## <a name="mdx-query-editor-window"></a>MDX 查询编辑器窗口  
 在 MDX 查询编辑器中可以使用下表所列选项。  
  
|术语|定义|  
|----------|----------------|  
|**查询编辑器窗口**|键入要由 MDX 查询编辑器执行的 MDX 语句和脚本。<br /><br /> 查询编辑器的上下文菜单提供有以下选项：<br /><br /> **剪切**：将当前选定内容复制到剪贴板，并从查询编辑器窗口中删除该选定内容。<br /><br /> **复制**：将当前选定内容复制到剪贴板。<br /><br /> **粘贴**：将剪贴板的内容粘贴到当前选定区域。<br /><br /> **连接**：打开 **“连接到服务器”** 对话框，以便与 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例建立连接。<br /><br /> **断开连接**：断开当前查询编辑器与 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例之间的连接。<br /><br /> **断开所有查询**：断开当前打开的所有查询编辑器。<br /><br /> **更改连接**：打开 **“连接到服务器”** 对话框，以便与其他 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例建立连接。<br /><br /> **在对象资源管理器中打开服务器**：在“对象资源管理器”中打开当前查询编辑器连接到的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例。<br /><br /> **执行**：执行所选代码，如果没有选定任何代码，则执行当前查询编辑器中的全部代码。<br /><br /> **属性窗口**：在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中显示当前查询窗口的“属性”窗口。<br /><br /> **查询选项**：显示“查询选项”对话框。|  
|**元数据窗口**|显示当前连接的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库的元数据。|  
|**Cube**|在当前连接的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库中选择一个多维数据集，以显示与 **“元数据”** 选项卡中的多维数据集关联的元数据。|  
|**元数据**|显示在 **“多维数据集”** 中选定的多维数据集的元数据，包括度量值组和度量值、关键绩效指标 (KPI)、维度、层次结构、级别、成员和成员属性。 若要检索对象的完全限定键，请执行下列操作之一：<br /><br /> 将该对象从 **“元数据”** 选项卡拖到查询窗格。<br /><br /> 右键单击该对象并选择“复制”，再右键单击查询窗格并选择“粘贴”。|  
|**函数**|显示可用于 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库的 MDX 函数的元数据，从 MDSCHEMA_FUNCTIONS 架构行集中检索。 若要检索函数的语法，请执行下列操作之一：<br /><br /> 将该对象从 **“函数”** 选项卡拖到查询窗格。<br /><br /> 右键单击该函数并选择 **“复制”**，再右键单击该查询窗格并选择 **“粘贴”**。|  
|**结果窗口**|在网格中显示 MDX 语句或脚本的结果。|  
|**消息窗口**|显示有关如何执行 MDX 语句或脚本的信息。 例如，此窗口可显示执行过程中遇到的所有错误，或执行完成后检索到的单元数。|  
  
  
