---
title: "\"创建处理查询\" 对话框（Analysis Services 多维数据） |Microsoft Docs"
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.createprocessingquerydialog.f1
ms.assetid: c133d624-f35e-486e-be9f-ceafd906f168
author: minewiskan
ms.author: owend
ms.openlocfilehash: 185ea27c344ccb9e06f914507faca3fea9554dae
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2020
ms.locfileid: "84526425"
---
# <a name="create-processing-query-dialog-box-analysis-services---multidimensional-data"></a>“创建处理查询”对话框（Analysis Services - 多维数据）
  可以使用 **中的** “创建处理查询” [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 对话框，在 **“存储选项”** 对话框的 **“通知”** 选项卡中创建处理查询。 处理查询返回的行集包含与 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 对象相关联的表自上次轮询之后所做的更改，用于增量更新该对象的多维 OLAP (MOLAP) 缓存。 Analysis Services 使用另一种称为轮询查询的查询，来轮询与对象相关联的表并确定该表是否已经更改。 完全更新对象的 MOLAP 缓存时，不需要处理查询。  
  
 处理查询通常应进行参数化，当前支持两个参数：  
  
-   轮询查询在上一次按计划轮询期间所返回的单独值。  
  
-   轮询查询在当前按计划轮询期间所返回的单独值。  
  
 例如，下表中列出的查询可以用于增量更新 Adventure Works DW 示例 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 项目中的 Customer 维度。  
  
|查询类型|查询语句|  
|----------------|---------------------|  
|轮询查询|`SELECT`<br /><br /> `MAX([CustomerKey]) AS LastCustomerKey`<br /><br /> `FROM`<br /><br /> `[dbo].[DimCustomer]`|  
|处理查询|`SELECT`<br /><br /> `*`<br /><br /> `FROM`<br /><br /> `[dbo].[DimCustomer]`<br /><br /> `WHERE`<br /><br /> `(CustomerKey > COALESCE (@Param1, - 1))`<br /><br /> `AND (CustomerKey <= @Param2)`|  
  
 有关按计划轮询通知的增量更新的详细信息，请参阅[主动缓存（分区）](multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)。  
  
 在 **“存储选项”** 对话框的 **“通知”** 选项卡上 **“按计划轮询”** 选项的网格中，单击 **“处理查询”** 列中的 ( **...** )，即可显示 **“创建处理查询”** 对话框。 有关“存储选项”**** 对话框的“通知”**** 选项卡的详细信息，请参阅[通知（“存储选项”对话框）（Analysis Services - 多维数据）](notifications-storage-options-dialog-analysis-services-multidimensional-data.md)。  
  
 输入的查询必须是基本访问接口的有效查询命令。 查询将通过基本访问接口进行处理，以便进行验证，并用于标识返回的列。 该对话框可以显示两个视图：  
  
-   Visual Database Tools (VDT) 查询生成器  
  
     对于所有用户，VDT 查询生成器视图提供了一组用户界面工具，用于以可视方式构造和测试 SQL 查询。  
  
-   一般查询生成器  
  
     对于高级用户，一般查询生成器视图提供了一个更为简单直接的用户界面，用于构造和测试 SQL 查询。  
  
## <a name="options"></a>选项  
 **数据源**  
 为查询指定数据源。  
  
 **查询定义**  
 查询定义根据选定的视图提供用于定义和测试查询的一个工具栏和多个窗格。  
  
 **Toolbar**  
 使用工具栏可以管理数据集、选择要显示的窗格以及控制各种查询函数。  
  
|值|说明|  
|-----------|-----------------|  
|**切换到一般查询生成器**|选择此选项将只显示可用于一般查询生成器视图的选项。 仅显示下列选项：<br /><br /> **SQL 窗格**<br /><br /> **结果窗格**<br /><br /> **“工具栏”**，只包含 **“切换到 VDT 查询生成器”** 和 **“运行”**<br /><br /> 注意：只有在选择了“切换到 VDT 查询生成器”时，才会显示此选项。 ****|  
|**“切换到 VDT 查询生成器”**|选择此选项将显示可用于 Visual Database Tools (VDT) 查询生成器视图的所有选项。<br /><br /> 注意：只有选定了“切换到一般查询生成器” **** ，才会显示此选项。|  
|**显示/隐藏关系图窗格**|显示或隐藏 **关系图窗格**。<br /><br /> **注意**仅当选择了 "**切换到 VDT 查询生成器**" 时，才会显示此选项。|  
|**显示/隐藏网格窗格**|显示或隐藏 **网格窗格**。<br /><br /> 注意：只有在选择了“切换到 VDT 查询生成器”时，才会显示此选项。 ****|  
|**显示/隐藏 SQL 窗格**|显示或隐藏 **SQL 窗格**。<br /><br /> 注意：只有在选择了“切换到 VDT 查询生成器”时，才会显示此选项。 ****|  
|**显示/隐藏结果窗格**|显示或隐藏 **结果窗格**。<br /><br /> 注意：只有在选择了“切换到 VDT 查询生成器”时，才会显示此选项。 ****|  
|**运行**|运行查询。 结果将显示在 "**结果" 窗格**中。|  
|**验证 SQL**|验证查询中的 SQL 语句。<br /><br /> 注意：只有在选择了“切换到 VDT 查询生成器”时，才会显示此选项。 ****|  
|**升序排序**|依据 **网格窗格**中的所选列对输出行按升序排序。<br /><br /> 注意：只有在选择了“切换到 VDT 查询生成器”时，才会显示此选项。 ****|  
|**降序排序**|依据 **网格窗格**中的所选列对输出行按降序排序。<br /><br /> 注意：只有在选择了“切换到 VDT 查询生成器”时，才会显示此选项。 ****|  
|**删除筛选器**|删除 **网格窗格**中所选行的排序条件（如果适用的话）。<br /><br /> 注意：只有在选择了“切换到 VDT 查询生成器”时，才会显示此选项。 ****|  
|**使用 Group By**|向查询中添加分组功能。<br /><br /> 注意：只有在选择了“切换到 VDT 查询生成器”时，才会显示此选项。 ****|  
|**添加表**|显示 **“添加表”** 对话框，以便向查询中添加新表或新视图。 有关“添加表”**** 对话框的详细信息，请参阅[“添加表”对话框（Analysis Services - 多维数据）](add-table-dialog-box-analysis-services-multidimensional-data.md)。<br /><br /> 注意：只有在选择了“切换到 VDT 查询生成器”时，才会显示此选项。 ****|  
  
 **关系图窗格**  
 以关系图的形式显示查询所引用的对象。 关系图可显示查询中包含的表以及这些表的联接方式。 选中或清除表中某列旁边的复选框，即可在查询输出中添加或删除该列。  
  
 向查询中添加表时，该对话框将根据表中的键创建表之间的联接。 若要添加联接，请将一个表中的字段拖到另一个表中的字段上。 若要管理某个联接，请右键单击该联接。  
  
 右键单击“关系图窗格”，可以添加或删除表，选择所有表，以及显示或隐藏窗格。****  
  
> [!NOTE]  
>  **关系图窗格**、 **网格窗格**和 **SQL 窗格** 中的内容是同步的，这样其中一个窗格的更改可以反映在其他两个窗格中。  
  
> [!IMPORTANT]  
>  该对话框不支持更改查询类型。  
  
 **“网格”窗格**  
 在网格中显示查询所引用的对象。 使用此窗格可以在查询中添加和删除列，以及更改每一列的设置。  
  
> [!NOTE]  
>  **关系图窗格**、 **网格窗格**和 **SQL 窗格** 中的内容是同步的，这样其中一个窗格的更改可以反映在其他两个窗格中。  
  
 **SQL 窗格**  
 将查询显示为 SQL 语句。 键入内容即可更改查询的 SQL 语句。  
  
> [!NOTE]  
>  **关系图窗格**、 **网格窗格**和 **SQL 窗格** 中的内容是同步的，这样其中一个窗格的更改可以反映在其他两个窗格中。  
  
 **结果窗格**  
 单击“工具栏”窗格中的“运行”时会显示查询结果。********  
  
## <a name="see-also"></a>另请参阅  
 [&#40;多维数据的 Analysis Services 设计器和对话框&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)  
  
  
