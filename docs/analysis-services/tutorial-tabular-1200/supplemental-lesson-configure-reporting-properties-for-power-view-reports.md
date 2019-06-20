---
title: 为 Power View 报表配置报表属性 |Microsoft Docs
ms.date: 05/07/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3ee35ac833a1170a688bb9439ed4dd8f6b6d6716
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65403369"
---
# <a name="supplemental-lesson---configure-reporting-properties-for-power-view-reports"></a>补充课程-为 Power View 报表配置报表属性
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

在本补充课程中，您将设置报表的 AW Internet 销售项目属性。 报告属性，使用户更轻松地选择和 Power View 中显示模型数据。 您还可以设置属性以隐藏特定的列和表，并创建新数据以在图表中使用。   
  
估计的时间才能完成本课程中：**30 分钟**  
  
## <a name="prerequisites"></a>先决条件  
本补充课程是表格建模教程的一部分，该教程应按顺序学习。 在执行本补充课程中的任务之前，您应已完成所有之前的课程。  
为了完成这一特定的补充课程，您还必须具备以下各项：  
  
-   （已完成本教程通过） AW Internet Sales 项目准备好进行部署或已部署到 Analysis Services 服务器。  
  
  
## <a name="model-properties-that-affect-reporting"></a>影响报表的模型属性  
当创作表格模型，有某些属性可以对其设置的单个列和表来增强用户报告在 Power View 中的体验。 此外，您还可以创建其他模型数据，以支持数据可视化和特定于报表客户端的其他功能。 对于示例 Adventure Works Internet Sales Model，您将进行以下某些更改：  
  
-   **添加新数据**-使用 DAX 公式在计算列中添加新数据更轻松地在图表中显示的格式创建日期信息。  
  
-   **隐藏对最终用户无用的表和列** -“隐藏”  属性控制是否在报表客户端中显示表和表列。 所隐藏的项仍然是模型的一部分，且保持可用于查询和计算。  
  
-   **启用一次单击表**-默认情况下，会发生任何操作如果用户单击字段列表中的表。 若要更改此行为，以便在单击表后会将该表添加到报表，需要针对您要在表中包含的每列设置“默认字段集”。 将对最终用户最可能要使用的表列设置此属性。  
  
-   **根据需要设置分组** -“保留唯一行”  属性确定列中的值是否应按其他字段（如标识符字段）中的值进行分组。 对于包含重复值，如客户名称 （例如，多个客户名为 John Smith） 的列，它是重要分组 （保留唯一行） 上**行标识符**以便向最终用户使用的字段正确的结果。  
  
-   **设置数据类型和数据格式** - 默认情况下，Power View 根据列数据类型应用规则，以确定字段是否可用作度量值。 因为 Power View 中的每个数据可视化还具有有关在何处可放置度量值和非度量值的规则，务必在模型中，设置数据类型或覆盖默认值，以实现您希望您的用户的行为。  
  
-   **设置按列排序**属性-**按列排序**属性指定列中的值是否应按排序不同字段中的值。 例如，在包含月份名称的 Month Calendar 列中，按列 Month Number 进行排序。  
  
## <a name="hide-tables-from-client-tools"></a>从客户端工具中隐藏表  
因为 Product 表中已经有了 Product Category 计算列和 Product Subcategory 计算列，所以没有必要向客户端应用程序显示 Product Category 表和 Product Subcategory 表。  
  
#### <a name="to-hide-the-product-category-and-product-subcategory-tables"></a>隐藏 Product Category 表和 Product Subcategory 表  
  
1.  在模型设计器中，右键单击 **Product Category** 表（选项卡），然后单击“从客户端工具中隐藏”  。  
  
2.  右键单击 **Product Subcategory** 表（选项卡），然后单击“从客户端工具中隐藏”  。  
  
## <a name="create-new-data-for-charts"></a>创建新的图表数据  
有时，可能需要使用 DAX 公式在模型中创建新数据。 在此任务中，您将向 Date 表添加两个新的计算列。 这些新列将以便于在表中使用的格式提供日期字段。  
  
#### <a name="to-create-new-data-for-charts"></a>创建新的图表数据  
  
1.  在“Date”  表中，滚动到最右侧，然后单击“添加列”  。  
  
2.  在公式栏中使用以下公式添加两个新的计算列：  
  
    |列名|公式|  
    |---------------|-----------|  
    |Year Quarter|=[Calendar Year] & " Q" & [Calendar Quarter]|  
    |Year Month|=[Calendar Year] & FORMAT([Month],"#00")|  
  
## <a name="default-field-set"></a>默认字段集  
默认字段集是预定义的列和表在报表字段列表中单击时自动添加到报表画布的表的度量值列表。 重要的是，您可以指定当在 Power View 报表中直观显示此表时，用户希望看到的默认列、度量值和字段排序方式。  对于 Internet Sales 模型，您将为 Customer 表、Geography 表和 Product 表定义一个默认字段集和顺序。 其中包含的只是当用户使用 Power View 报表分析 Adventure Works Internet Sales 数据时，希望看到的那些最常见的列。  
  
有关默认字段集的详细信息，请参阅[配置默认字段集为 Power View 报表](../tabular-models/power-view-configure-default-field-set-for-reports.md)。  
  
#### <a name="to-set-default-field-set-for-tables"></a>为表设置默认字段集  
  
1.  在模型设计器中，单击“Customer”  表（选项卡）。  
  
2.  在“属性”  窗口的“报表属性”  下，在“默认字段集”  属性中，单击“单击可编辑”  以打开“默认字段集”  对话框。  
  
3.  在“默认字段集”  对话框的“表中的字段”  列表框中，按 Ctrl 并选择以下字段，然后单击“添加”  。  
  
    **出生日期**， **Customer Alternate ID**，**名字**，**姓氏**。  
  
4.  在“默认字段，按顺序”  窗口中，使用“上移”和“下移”按钮确定以下顺序：  
  
    **Customer Alternate ID**  
  
    **First Name**  
  
    **Last Name**  
  
    **Birth Date**。  
  
5.  单击“确定”  以关闭“Customer”  表的“默认字段集”  对话框。  
  
6.  对“Geography”  表执行上述相同步骤，同时选择以下字段并按如下顺序排列。  
  
    “City”  、“State Province Code”  、“Country Region Code”  。  
  
7.  最后，对“Product”  表执行上述相同步骤，同时选择以下字段并按如下顺序排列。  
  
    **Product Alternate ID**，**产品名称**。  
  
## <a name="table-behavior"></a>表行为  
通过使用“表行为”属性，您可以针对不同的可视化类型更改默认行为，并针对 Power View 报表中使用的表更改分组行为。 这样，就可以按图块、卡片和图表布局对标识信息（如名称、图像或标题）生成更好的默认位置。  
  
有关表行为属性的详细信息，请参阅[为 Power View 报表配置表行为属性](../tabular-models/power-view-configure-table-behavior-properties-for-reports.md)。  
  
#### <a name="to-set-table-behavior"></a>若要设置表行为 
  
1.  在模型设计器中，单击“Customer”  表（选项卡）。  
  
2.  在“属性”  窗口的“表行为”  属性下，单击“单击可编辑”  以打开“表行为”  对话框。  
  
3.  在中**表行为**对话框中**行标识符**下拉列表框中，选择**客户 ID**列。  
  
4.  在“保留唯一行”  列表框中，依次选择“First Name”  和“Last Name”  。  
  
    此属性设置指定这些列提供应视为唯一的值，即使这些值重复也不例外（例如，当两个或更多员工同名时）。  
  
5.  在“默认标签”  下拉列表框中，选择“Last Name”  列。  
  
    此属性设置指定此列提供一个表示行数据的显示名称。  
  
6.  重复这些步骤**地理**表中，选择**Geography ID**列作为行标识符，并**城市**中的列**保留唯一行**列表框。 您不需要为此表设置“默认标签”。  
  
7.  重复这些步骤**产品**表中，选择**产品 ID**列作为行标识符，并**产品名称**中的列**保持唯一行**列表框。 有关**默认标签**，选择**Product Alternate ID**。  
  
## <a name="reporting-properties-for-columns"></a>列的报表属性  
对于列而言，您可以设置许多基本列属性和特定的报表属性，以改善模型报表体验。 例如，用户可能不需要看到每个表中的每一列。 就像隐藏 Product Category 和 Product Subcategory 表更早版本，通过使用列的 Hidden 属性，您可以隐藏特定列的表，否则所示。 其他属性（如“数据格式”和“按列排序”）也可能影响列数据出现在报表中的方式。 您可以现在对特定的列设置上述某些属性。 其他列不要求您执行任何操作，下面也没显示它们。  
  
您将只在此处设置一些不同的列属性，但其他属性还有很多。 有关详细信息有关列报表属性的详细信息，请参阅[列属性](../tabular-models/column-properties-ssas-tabular.md)。  
  
#### <a name="to-set-properties-for-columns"></a>设置列的属性  
  
1.  在模型设计器中，单击“Customer”  表（选项卡）。  
  
2.  单击**Customer ID**列中显示的列的属性中**属性**窗口。  
  
3.  在“属性”  窗口中，将“隐藏”  属性设置为 True。 **客户 ID**列然后将变为灰显状态模型设计器中。  
  
4.  重复这些步骤，同时为每个指定的表设置以下列和报表属性。 将所有其他属性保留为其默认设置。  
  
    注意：对于所有日期列，请确保**数据类型**是**日期**。  
  
    **Customer**  
  
    |“列”|属性|ReplTest1|  
    |----------|------------|---------|  
    |地理 ID|Hidden|True|  
    |Birth Date|数据格式|短日期|  
  
    **Date**  
  
    > [!NOTE]  
    > 作为模型日期表使用标记为日期表设置选择日期表，因为在第 7 课：标记为日期表和列作为日期表中的日期列用作唯一标识符，日期列的行标识符属性将自动设置为 True，并且不能更改。 在 DAX 公式中使用时间智能函数时，必须指定一个日期表。 在此模型中，您使用时间智能函数创建了许多度量值，以计算不同时期（如上一季度和当前季度）的销售数据，同时也用于 KPI 中。 有关指定日期表的详细信息，请参阅[指定标记为日期表用于时间智能](../tabular-models/specify-mark-as-date-table-for-use-with-time-intelligence-ssas-tabular.md)。  
  
    |“列”|属性|ReplTest1|  
    |----------|------------|---------|  
    |Date|数据格式|短日期|  
    |Day Number of Week|Hidden|True|  
    |Day Name|按列排序|Day Number of Week|  
    |Day of Week|Hidden|True|  
    |Day of Month|Hidden|True|  
    |Day of Year|Hidden|True|  
    |Month Name|按列排序|Month|  
    |Month|Hidden|True|  
    |Month Calendar|Hidden|True|  
    |Fiscal Quarter|Hidden|True|  
    |Fiscal Year|Hidden|True|  
    |Fiscal Semester|Hidden|True|  
  
    **地域**  
  
    |“列”|属性|ReplTest1|  
    |----------|------------|---------|  
    |地理 ID|Hidden|True|  
    |销售区域 ID|Hidden|True|  
  
    **Product**  
  
    |“列”|属性|ReplTest1|  
    |----------|------------|---------|  
    |产品 ID|Hidden|True|  
    |Product Alternate ID|默认标签|True|  
    |产品子类别 ID|Hidden|True|  
    |Product Start Date|数据格式|短日期|  
    |Product End Date|数据格式|短日期|  
  
    **Internet Sales**  
  
    |“列”|属性|ReplTest1|  
    |----------|------------|---------|  
    |产品 ID|Hidden|True|  
    |客户 ID|Hidden|True|  
    |促销 ID|Hidden|True|  
    |货币 ID|Hidden|True|  
    |销售区域 ID|Hidden|True|  
    |Order Quantity|数据类型<br /><br />数据格式<br /><br />小数位数|小数<br /><br />小数<br /><br />0|  
    |Order Date|数据格式|短日期|  
    |Due Date|数据格式|短日期|  
    |Ship Date|数据格式|短日期|  
  
## <a name="redeploy-the-adventure-works-internet-sales-tabular-model"></a>重新部署 Adventure Works Internet Sales 表格模型  
因为您更改了模型，所以必须重新部署此模型。  
  
#### <a name="to-redeploy-the-adventure-works-internet-sales-tabular-model"></a>重新部署 Adventure Works Internet Sales 表格模型  
  
-   在 SSDT 中，单击**构建**菜单，并单击**部署 Adventure Works Internet Sales Model**。  
  
    “部署”  对话框将出现，并且显示模型中包括的元数据和每个表的部署状态。  
  
## <a name="next-steps"></a>后续步骤  
现在可以使用 Excel 直观显示模型中的数据。 确保 SharePoint 网站上的 Analysis Services 和 Reporting Services 帐户对于您在其中部署模型的 Analysis Services 实例具有读取权限。  
  
  
  
  
