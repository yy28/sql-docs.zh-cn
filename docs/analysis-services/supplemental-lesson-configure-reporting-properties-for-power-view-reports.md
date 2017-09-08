---
title: "为 Power View 报表配置报表属性 |Microsoft 文档"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 0ffc5f44-17d3-42d4-bc2c-baf3b4485e2d
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4bf24a40a820b42b185f8fd6838816a51b4cd424
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="supplemental-lesson---configure-reporting-properties-for-power-view-reports"></a>补充课-为 Power View 报表配置报表属性
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

在此补充课程中，你将设置 reporting AW Internet Sales 项目的属性。 通过报表属性，最终用户可以更轻松地在 Power View 中选择和显示模型数据。 您还可以设置属性以隐藏特定的列和表，并创建新数据以在图表中使用。   
  
学完本课的估计时间： **30 分钟**  
  
## <a name="prerequisites"></a>先决条件  
本补充课程是表格建模教程的一部分，该教程应按顺序学习。 在执行本补充课程中的任务之前，您应已完成所有之前的课程。  
为了完成这一特定的补充课程，您还必须具备以下各项：  
  
-   （通过本教程中完成） 的 AW Internet Sales 项目准备好部署或已部署到 Analysis Services 服务器。  
  
  
## <a name="model-properties-that-affect-reporting"></a>影响报表的模型属性  
当创作表格模型时，您可以对单独的列和表设置某些属性，以增强最终用户在 Power View 中的报表体验。 此外，您还可以创建其他模型数据，以支持数据可视化和特定于报表客户端的其他功能。 对于示例 Adventure Works Internet Sales Model，您将进行以下某些更改：  
  
-   **添加新数据** – 使用 DAX 公式在计算列中添加新数据，会以更易于在图表中显示的格式创建日期信息。  
  
-   **隐藏对最终用户无用的表和列** -“隐藏”属性控制是否在报表客户端中显示表和表列。 所隐藏的项仍然是模型的一部分，且保持可用于查询和计算。  
  
-   **启用一次单击表** – 默认情况下，如果最终用户在字段列表中单击了某个表，将不会发生任何操作。 若要更改此行为，以便在单击表后会将该表添加到报表，需要针对您要在表中包含的每列设置“默认字段集”。 将对最终用户最可能要使用的表列设置此属性。  
  
-   **根据需要设置分组** -“保留唯一行”属性确定列中的值是否应按其他字段（如标识符字段）中的值进行分组。 对于包含重复值的列（如“Customer Name”列，具有多个名为 John Smith 的客户），务必依据“行标识符”字段进行分组（保留唯一行），以便向最终用户提供正确的结果。  
  
-   **设置数据类型和数据格式** - 默认情况下，Power View 根据列数据类型应用规则，以确定字段是否可用作度量值。 因为 Power View 中的每个数据可视化还具有有关在何处可放置度量值和非度量值的规则，所以，务必在模型中设置此数据类型或覆盖默认值，以实现你希望向最终用户展示的行为。  
  
-   **设置“按列排序”**属性 –“按列排序”属性指定列中的值是否应按其他字段中的值进行排序。 例如，在包含月份名称的 Month Calendar 列中，按列 Month Number 进行排序。  
  
## <a name="hide-tables-from-client-tools"></a>从客户端工具中隐藏表  
因为 Product 表中已经有了 Product Category 计算列和 Product Subcategory 计算列，所以没有必要向客户端应用程序显示 Product Category 表和 Product Subcategory 表。  
  
#### <a name="to-hide-the-product-category-and-product-subcategory-tables"></a>隐藏 Product Category 表和 Product Subcategory 表  
  
1.  在模型设计器中，右键单击 **Product Category** 表（选项卡），然后单击“从客户端工具中隐藏”。  
  
2.  右键单击 **Product Subcategory** 表（选项卡），然后单击“从客户端工具中隐藏”。  
  
## <a name="create-new-data-for-charts"></a>创建新的图表数据  
有时，可能需要使用 DAX 公式在模型中创建新数据。 在此任务中，您将向 Date 表添加两个新的计算列。 这些新列将以便于在表中使用的格式提供日期字段。  
  
#### <a name="to-create-new-data-for-charts"></a>创建新的图表数据  
  
1.  在“Date”表中，滚动到最右侧，然后单击“添加列”。  
  
2.  在公式栏中使用以下公式添加两个新的计算列：  
  
    |列名|公式|  
    |---------------|-----------|  
    |Year Quarter|=[Calendar Year] & " Q" & [Calendar Quarter]|  
    |Year Month|=[Calendar Year] & FORMAT([Month],"#00")|  
  
## <a name="default-field-set"></a>默认字段集  
默认字段集是预定义的列和表在报表字段列表中单击时自动添加到报表画布的表的度量值列表。 重要的是，您可以指定当在 Power View 报表中直观显示此表时，用户希望看到的默认列、度量值和字段排序方式。  对于 Internet Sales 模型，您将为 Customer 表、Geography 表和 Product 表定义一个默认字段集和顺序。 其中包含的只是当用户使用 Power View 报表分析 Adventure Works Internet Sales 数据时，希望看到的那些最常见的列。  
  
有关默认字段集的详细信息，请参阅 SQL Server 联机丛书中的[配置 Power View 报表的默认字段集（SSAS 表格）](../analysis-services/tabular-models/power-view-configure-default-field-set-for-reports.md)。  
  
#### <a name="to-set-default-field-set-for-tables"></a>为表设置默认字段集  
  
1.  在模型设计器中，单击“Customer”表（选项卡）。  
  
2.  在“属性”窗口的“报表属性”下，在“默认字段集”属性中，单击“单击可编辑”以打开“默认字段集”对话框。  
  
3.  在“默认字段集”对话框的“表中的字段”列表框中，按 Ctrl 并选择以下字段，然后单击“添加”。  
  
    “Birth Date”、“Customer Alternate Id”、“First Name”、“Last Name”。  
  
4.  在“默认字段，按顺序”窗口中，使用“上移”和“下移”按钮确定以下顺序：  
  
    **Customer Alternate Id**  
  
    **First Name**  
  
    **Last Name**  
  
    **Birth Date**。  
  
5.  单击“确定”以关闭“Customer”表的“默认字段集”对话框。  
  
6.  对“Geography”表执行上述相同步骤，同时选择以下字段并按如下顺序排列。  
  
    “City”、“State Province Code”、“Country Region Code”。  
  
7.  最后，对“Product”表执行上述相同步骤，同时选择以下字段并按如下顺序排列。  
  
    “Product Alternate Id”、“Product Name”。  
  
## <a name="table-behavior"></a>表行为  
通过使用“表行为”属性，您可以针对不同的可视化类型更改默认行为，并针对 Power View 报表中使用的表更改分组行为。 这样，就可以按图块、卡片和图表布局对标识信息（如名称、图像或标题）生成更好的默认位置。  
  
有关表行为属性的详细信息，请参阅 SQL Server 联机丛书中的[为 Power View 报表配置表行为属性（SSAS 表格）](../analysis-services/tabular-models/power-view-configure-table-behavior-properties-for-reports.md)。  
  
#### <a name="to-set-table-behavior"></a>若要设置表行为 
  
1.  在模型设计器中，单击“Customer”表（选项卡）。  
  
2.  在“属性”窗口的“表行为”属性下，单击“单击可编辑”以打开“表行为”对话框。  
  
3.  在“表行为”对话框的“行标识符”下拉列表框中，选择“Customer Id”列。  
  
4.  在“保留唯一行”列表框中，依次选择“First Name”和“Last Name”。  
  
    此属性设置指定这些列提供应视为唯一的值，即使这些值重复也不例外（例如，当两个或更多员工同名时）。  
  
5.  在“默认标签”下拉列表框中，选择“Last Name”列。  
  
    此属性设置指定此列提供一个表示行数据的显示名称。  
  
6.  对“Geography”表重复上述步骤，同时选择“Geography Id”列作为“行标识符”，并在“保留唯一行”列表框中选择“City”列。 您不需要为此表设置“默认标签”。  
  
7.  对“Product” 表重复上述步骤，同时选择“Product Id”列作为“行标识符”，并在“保留唯一行”列表框中选择“Product Name”列。 对于“默认标签”，选择“Product Alternate Id”。  
  
## <a name="reporting-properties-for-columns"></a>列的报表属性  
对于列而言，您可以设置许多基本列属性和特定的报表属性，以改善模型报表体验。 例如，用户可能不需要看到每个表中的每一列。 就像前面您通过使用列的“隐藏”属性隐藏 Product Category 表和 Product Subcategory 表一样，您可以隐藏表中原本应显示的特定列。 其他属性（如“数据格式”和“按列排序”）也可能影响列数据出现在报表中的方式。 您可以现在对特定的列设置上述某些属性。 其他列不要求您执行任何操作，下面也没显示它们。  
  
您将只在此处设置一些不同的列属性，但其他属性还有很多。 有关列报表属性的详细信息，请参阅 SQL Server 联机丛书中的[列属性（SSAS 表格）](../analysis-services/tabular-models/column-properties-ssas-tabular.md)。  
  
#### <a name="to-set-properties-for-columns"></a>设置列的属性  
  
1.  在模型设计器中，单击“Customer”表（选项卡）。  
  
2.  单击“Customer Id”列，以便在“属性”窗口中显示列属性。  
  
3.  在“属性”窗口中，将“隐藏”属性设置为 True。 然后，“Customer Id”列在模型设计器中将变为灰显状态。  
  
4.  重复这些步骤，同时为每个指定的表设置以下列和报表属性。 将所有其他属性保留为其默认设置。  
  
    注意：对于所有日期列，请确保“数据类型”为“日期”。  
  
    **Customer**  
  
    |列|属性|“值”|  
    |----------|------------|---------|  
    |Geography Id|Hidden|True|  
    |Birth Date|数据格式|短日期|  
  
    **日期**  
  
    > [!NOTE]  
    > 因为我们在第 7 课“标记为日期表”中已经使用“标记为日期表”设置选择 Date 表作为模型日期表，并且选择 Date 表中的 Date 列作为要用作唯一标识符的列，所以，Date 列的“行标识符”属性将自动设置为 True 且无法更改。 在 DAX 公式中使用时间智能函数时，必须指定一个日期表。 在此模型中，您使用时间智能函数创建了许多度量值，以计算不同时期（如上一季度和当前季度）的销售数据，同时也用于 KPI 中。 有关指定日期表的详细信息，请参阅 SQL Server 联机丛书中的[指定“标记为日期表”以便用于时间智能（SSAS 表格）](../analysis-services/tabular-models/specify-mark-as-date-table-for-use-with-time-intelligence-ssas-tabular.md)。  
  
    |列|属性|“值”|  
    |----------|------------|---------|  
    |日期|数据格式|短日期|  
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
  
    |列|属性|“值”|  
    |----------|------------|---------|  
    |Geography Id|Hidden|True|  
    |Sales Territory Id|Hidden|True|  
  
    **Product**  
  
    |列|属性|“值”|  
    |----------|------------|---------|  
    |Product Id|Hidden|True|  
    |Product Alternate Id|默认标签|True|  
    |Product Subcategory Id|Hidden|True|  
    |Product Start Date|数据格式|短日期|  
    |Product End Date|数据格式|短日期|  
  
    **Internet Sales**  
  
    |列|属性|“值”|  
    |----------|------------|---------|  
    |Product Id|Hidden|True|  
    |Customer Id|Hidden|True|  
    |Promotion Id|Hidden|True|  
    |Currency Id|Hidden|True|  
    |Sales Territory Id|Hidden|True|  
    |Order Quantity|数据类型<br /><br />数据格式<br /><br />小数位数|小数<br /><br />小数<br /><br />0|  
    |Order Date|数据格式|短日期|  
    |Due Date|数据格式|短日期|  
    |Ship Date|数据格式|短日期|  
  
## <a name="redeploy-the-adventure-works-internet-sales-tabular-model"></a>重新部署 Adventure Works Internet Sales 表格模型  
因为您更改了模型，所以必须重新部署此模型。  
  
#### <a name="to-redeploy-the-adventure-works-internet-sales-tabular-model"></a>重新部署 Adventure Works Internet Sales 表格模型  
  
-   在 SSDT 中，单击**生成**菜单，，然后单击**部署 Adventure Works Internet 销售模型**。  
  
    “部署”对话框将出现，并且显示模型中包括的元数据和每个表的部署状态。  
  
## <a name="next-steps"></a>后续步骤  
现在可以使用 Power View 直观显示模型中的数据了。 确保 SharePoint 网站上的 Analysis Services 和 Reporting Services 帐户对于您在其中部署模型的 Analysis Services 实例具有读取权限。  
  
若要创建指向模型的 Reporting Services 报表数据源，请参阅 [Table Model Connection Type (SSRS)](http://msdn.microsoft.com/library/hh270317%28v=SQL.110%29.aspx)表模型连接类型 (SSRS)。  
  
  
  

