---
title: 创建或编辑命名的查询对话框 (Analysis Services-多维数据) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.dsvdesigner.createnamedquery.f1
helpviewer_keywords:
- Create Named Query dialog box
ms.assetid: 8e192ad6-a0b1-4e21-bb3f-087c93e62941
caps.latest.revision: 23
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: f97b06c3fb67080e7ebc3adc3c1e4d84d3fdea61
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36125044"
---
# <a name="create-or-edit-named-query-dialog-box-analysis-services---multidimensional-data"></a>“创建或编辑命名查询”对话框（Analysis Services - 多维数据）
  可以使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中的“创建/编辑命名查询”对话框，在数据源视图设计器中创建或编辑命名查询。 可以将命名查询视为表，基于该表可以建立其他 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 对象。 可以通过执行以下操作之一显示“创建/编辑命名查询”对话框：  
  
-   在 **数据源视图设计器** 的 **“工具栏”** 窗格上，单击 **“新建命名查询”**。  
  
-   右键单击数据源视图设计器的“关系图”窗格，再选择“新建命名查询”。  
  
-   在数据源视图设计器的“关系图”窗格或“表”窗格中，右键单击某个命名查询的名称，再选择“编辑命名查询”。  
  
 输入的查询必须是基本访问接口的有效查询命令。 查询将通过基本访问接口进行处理，以便进行验证，并用于标识返回的列。 该对话框可以显示两个视图：  
  
-   Visual Database Tools (VDT) 查询生成器  
  
     对于所有用户，VDT 查询生成器视图提供了一组用户界面工具，用于以可视方式构造和测试 SQL 查询。  
  
-   一般查询生成器  
  
     对于高级用户，一般查询生成器视图提供了一个更为简单直接的用户界面，用于构造和测试 SQL 查询。  
  
## <a name="options"></a>“常规”  
 **名称**  
 键入查询的名称。  
  
 **Description**  
 键入查询的说明（可选）。  
  
 **数据源**  
 为查询指定数据源。  
  
 **查询定义**  
 查询定义根据选定的视图提供用于定义和测试查询的一个工具栏和多个窗格。  
  
 **工具栏**  
 使用工具栏可以管理数据集、选择要显示的窗格以及控制各种查询函数。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**切换到一般查询生成器**|选择此选项将只显示可用于一般查询生成器视图的选项。 仅显示下列选项：<br />**SQL 窗格**<br />**结果窗格**<br />**“工具栏”**，只包含 **“切换到 VDT 查询生成器”** 和 **“运行”**<br /><br /> <br /><br /> 注意：只有在选择了“切换到 VDT 查询生成器”时，才会显示此选项。 |  
|**切换到 VDT 查询生成器**|选择此选项将显示可用于 Visual Database Tools (VDT) 查询生成器视图的所有选项。<br /><br /> 注意：只有选定了“切换到一般查询生成器”  ，才会显示此选项。|  
|**显示/隐藏关系图窗格**|显示或隐藏 **关系图窗格**。<br /><br /> **注意** 只有在选择了 **“切换到 VDT 查询生成器”** 时，才会显示此选项。|  
|**显示/隐藏网格窗格**|显示或隐藏 **网格窗格**。<br /><br /> 注意：只有在选择了“切换到 VDT 查询生成器”时，才会显示此选项。 |  
|**显示/隐藏 SQL 窗格**|显示或隐藏 **SQL 窗格**。<br /><br /> 注意：只有在选择了“切换到 VDT 查询生成器”时，才会显示此选项。 |  
|**显示/隐藏结果窗格**|显示或隐藏 **结果窗格**。<br /><br /> 注意：只有在选择了“切换到 VDT 查询生成器”时，才会显示此选项。 |  
|**运行**|运行查询。 结果显示在 **结果窗格**中。|  
|**验证 SQL**|验证查询中的 SQL 语句。<br /><br /> 注意：只有在选择了“切换到 VDT 查询生成器”时，才会显示此选项。 |  
|**升序排序**|依据 **网格窗格**中的所选列对输出行按升序排序。<br /><br /> 注意：只有在选择了“切换到 VDT 查询生成器”时，才会显示此选项。 |  
|**降序排序**|依据 **网格窗格**中的所选列对输出行按降序排序。<br /><br /> 注意：只有在选择了“切换到 VDT 查询生成器”时，才会显示此选项。 |  
|**删除筛选器**|删除 **网格窗格**中所选行的排序条件（如果适用的话）。<br /><br /> 注意：只有在选择了“切换到 VDT 查询生成器”时，才会显示此选项。 |  
|**使用分组依据**|向查询中添加分组功能。<br /><br /> 注意：只有在选择了“切换到 VDT 查询生成器”时，才会显示此选项。 |  
|**添加表**|显示 **“添加表”** 对话框，以便向查询中添加新表或新视图。 有关“添加表”对话框的详细信息，请参阅[“添加表”对话框（Analysis Services - 多维数据）](add-table-dialog-box-analysis-services-multidimensional-data.md)。<br /><br /> 注意：只有在选择了“切换到 VDT 查询生成器”时，才会显示此选项。 |  
  
 **关系图窗格**  
 以关系图的形式显示查询所引用的对象。 关系图可显示查询中包含的表以及这些表的联接方式。 选中或清除表中某列旁边的复选框，即可在查询输出中添加或删除该列。  
  
 向查询中添加表时，该对话框将根据表中的键创建表之间的联接。 若要添加联接，请将一个表中的字段拖到另一个表中的字段上。 若要管理某个联接，请右键单击该联接。  
  
 右键单击“关系图窗格”，可以添加或删除表，选择所有表，以及显示或隐藏窗格。  
  
> [!NOTE]  
>  “关系图窗格”、“网格窗格”和“SQL 窗格”中的内容是同步的，这样其中一个窗格的更改可以反映在其他两个窗格中。  
  
> [!IMPORTANT]  
>  该对话框不支持更改查询类型。  
  
 **网格窗格**  
 在网格中显示查询所引用的对象。 使用此窗格可以在查询中添加和删除列，以及更改每一列的设置。  
  
> [!NOTE]  
>  “关系图窗格”、“网格窗格”和“SQL 窗格”中的内容是同步的，这样其中一个窗格的更改可以反映在其他两个窗格中。  
  
 **SQL 窗格**  
 将查询显示为 SQL 语句。 键入内容即可更改查询的 SQL 语句。  
  
> [!NOTE]  
>  “关系图窗格”、“网格窗格”和“SQL 窗格”中的内容是同步的，这样其中一个窗格的更改可以反映在其他两个窗格中。  
  
 **结果窗格**  
 单击“工具栏”窗格中的“运行”时会显示查询结果。  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 设计器和对话框&#40;多维数据&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [数据源视图中定义命名的查询&#40;Analysis Services&#41;](multidimensional-models/define-named-queries-in-a-data-source-view-analysis-services.md)  
  
  