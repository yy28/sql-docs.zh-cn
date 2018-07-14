---
title: DMX 查询编辑器 (Analysis Services-数据挖掘) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.startpage.dmx.f1
ms.assetid: 7ac877a1-0f29-46b9-9a51-73b02172bef1
caps.latest.revision: 21
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1c1efcb4ecef6c311882b471a56535543bcc25b1
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37236057"
---
# <a name="dmx-query-editor-analysis-services---data-mining"></a>DMX 查询编辑器（Analysis Services - 数据挖掘）
  可以使用 DMX 查询编辑器，设计和执行使用数据挖掘扩展插件 (DMX) 语言编写的语句。  
  
## <a name="features"></a>功能  
  
-   在 DMX 查询编辑器中的查询编辑窗格键入脚本。  
  
-   若要执行脚本，请按 **F5**，或单击工具栏上或 **“查询”** 菜单上的 **“执行”** 。 如果选择了一部分代码，则只执行该部分代码。 如果没有选择任何代码，则会执行 DMX 查询编辑器的全部内容。  
  
-   查看多维数据集的元数据以及多维数据集窗格中 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库所包含的其他对象。  
  
-   有关 DMX 语法的帮助，请在 DMX 查询编辑器中选择关键字，再按 **F1**。  
  
-   有关 DMX 语法的动态帮助，请在 **“帮助”** 菜单上单击 **“动态帮助”** ，以打开动态帮助组件。 如果使用动态帮助，当在查询编辑器中键入关键字时，帮助主题将显示在 **“动态帮助”** 窗口中。  
  
## <a name="sql-server-analysis-services-editors-toolbar"></a>SQL Server Analysis Services 编辑器工具栏  
 在 DMX 查询编辑器处于打开状态时， **“SQL Server Analysis Services 编辑器”** 工具栏将显示下表中所列的按钮：  
  
|术语|定义|  
|----------|----------------|  
|**“连接”**|打开 **“连接到服务器”** 对话框，以便与 Analysis Services 实例建立连接。|  
|**断开连接**|断开 DMX 查询编辑器与 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例之间的连接。|  
|**更改连接**|打开 **“连接到服务器”** 对话框，以便与其他 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例建立连接。|  
|**使用当前连接新建查询**|使用当前“DMX 查询编辑器”窗口中的连接信息，打开一个新的“DMX 查询编辑器”窗口。|  
|**可用数据库**|将连接更改到同一实例的其他 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库。|  
|**执行**|执行所选的代码；如果没有选择任何代码，则执行 DMX 查询编辑器中的全部代码。|  
|**分析**|检查所选代码的语法。 如果没有选择任何代码，则检查整个“DMX 查询编辑器”窗口的语法。|  
|**取消执行查询**|向服务器发送取消请求。 有些查询不能立即取消，而必须等待适当的取消条件。 如果进行取消，在回滚事务时可能会发生延迟。|  
  
## <a name="dmx-query-editor-window"></a>“DMX 查询编辑器”窗口  
 DMX 查询编辑器中提供下表中所列的选项：  
  
|术语|定义|  
|----------|----------------|  
|**查询编辑器窗口**|使用 DMX 查询编辑器键入要执行的 DMX 语句和脚本。<br /><br /> 查询编辑器的上下文菜单提供有以下选项：<br /><br /> **剪切**： 将当前选定内容复制到剪贴板，并从查询编辑器窗口中删除所选内容。<br /><br /> **复制**：将当前选定内容复制到剪贴板。<br /><br /> **粘贴**： 粘贴到当前所选内容剪贴板的内容。<br /><br /> **连接**：打开“连接到服务器”  对话框，以便与 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例建立连接。<br /><br /> **断开**： 断开当前查询编辑器与[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]实例。<br /><br /> **断开所有查询**： 断开所有打开的查询编辑器。<br /><br /> **更改连接**： 将打开**连接到服务器**对话框中，来为另一种连接[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]实例。<br /><br /> **在对象资源管理器中打开服务器**： 将打开[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]实例中当前查询编辑器连接到**对象资源管理器**。<br /><br /> **执行**： 执行所选的代码，或如果没有选择任何代码，在当前查询编辑器中执行的全部代码。<br /><br /> **属性窗口**： 显示**属性**中的窗口[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]当前查询窗口。<br /><br /> **查询选项**： 显示**查询选项**对话框。|  
|**元数据窗口**|显示当前连接的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库的元数据。|  
|**Cube**|在当前连接的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库中选择一个多维数据集，以显示与 **“元数据”** 选项卡中的多维数据集关联的元数据。|  
|**元数据**|显示在 **“多维数据集”** 中选定的多维数据集的元数据，包括度量值组和度量值、关键绩效指标 (KPI)、维度、层次结构、级别、成员和成员属性。 若要检索对象的完全限定键，请执行下列操作之一：<br /><br /> 将该对象从 **“元数据”** 选项卡拖到查询窗格。<br /><br /> 或：<br /><br /> 右键单击该对象并选择 **“复制”**，再右键单击查询窗格并选择 **“粘贴”**。|  
|**函数**|按照从 DMSCHEMA_MINING_FUNCTIONS 架构行集的检索结果，显示对 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库可用的 DMX 函数的元数据。<br /><br /> 若要检索函数的语法，请执行下列操作之一：<br /><br /> 将该对象从 **“函数”** 选项卡拖到查询窗格。<br /><br /> 或：<br /><br /> 右键单击该函数并选择 **“复制”**，再右键单击该查询窗格并选择 **“粘贴”**。|  
|**结果窗口**|在一个网格中显示 DMX 语句的结果。|  
|**消息窗口**|显示有关 DMX 语句执行情况的信息。 例如，此窗口可显示执行过程中遇到的所有错误，或执行完成后检索到的单元数。|  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 设计器和对话框&#40;多维数据&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [数据挖掘扩展插件&#40;DMX&#41;引用](/sql/dmx/data-mining-extensions-dmx-reference)   
 [MDX 查询编辑器&#40;Analysis Services-多维数据&#41;](mdx-query-editor-analysis-services-multidimensional-data.md)   
 [XMLA 查询编辑器&#40;Analysis Services-多维数据&#41;](xmla-query-editor-analysis-services-multidimensional-data.md)   
 [查询和文本编辑器&#40;SQL Server Management Studio&#41;](../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md)   
 [SQL Server Management Studio 键盘快捷键](../ssms/sql-server-management-studio-keyboard-shortcuts.md)   
 [自定义菜单和键盘快捷方式](../ssms/customize-menus-and-shortcut-keys.md)   
 [查询编辑器中的颜色编码](../relational-databases/scripting/color-coding-in-query-editors.md)  
  
  
