---
title: 定义计算成员 |Microsoft 文档
ms.custom: ''
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 07f13e1c-0b20-4f9e-ad62-c438983f2785
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: ca85c5105a56b180cd819dbf35a55ec5238b73ce
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="lesson-6-1---defining-calculated-members"></a>课程 6-1-定义计算成员
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

计算成员是基于多维数据集数据、算术运算符、数字和函数组合定义的维度或度量值组成员。 例如，可以创建用于计算多维数据集中的两个物理度量值之和的计算成员。 计算成员定义将存储在多维数据集中，但它们的值将在查询时计算。  
  
若要创建计算成员，请在多维数据集设计器的“计算”选项卡上使用“新建计算成员”命令。 您可以在包括度量值维度在内的任意维度中创建计算成员。 还可以将计算成员放在“计算属性”对话框的显示文件夹内。 有关详细信息，请参阅[计算](../analysis-services/multidimensional-models-olap-logical-cube-objects/calculations.md)、[多维模型中的计算](../analysis-services/multidimensional-models/calculations-in-multidimensional-models.md)和[创建计算成员](../analysis-services/multidimensional-models/create-calculated-members.md)。  
  
在此主题的任务中，将定义计算度量值，以便让用户查看 Internet 销售、分销商销售和所有销售的毛利润率百分比和销售率。  
  
## <a name="defining-calculations-to-aggregate-physical-measures"></a>定义聚合物理度量值的计算  
  
1.  打开 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教程多维数据集的多维数据集设计器，然后单击“计算”选项卡。  
  
    请注意“计算表达式”窗格和“脚本组织程序”窗格中的默认 CALCULATE 命令。 此命令指定多维数据集中的度量值应该根据其 AggregateFunction 属性所指定的值进行聚合。 度量值通常会求和，但也可能计数或按其他某种方式进行聚合。  
  
    下图显示多维数据集设计器的“计算”选项卡。  
  
    ![多维数据集设计器计算选项卡](../analysis-services/media/l6-calculatedmembers-1.gif "多维数据集设计器计算选项卡")  
  
2.  在“计算”选项卡的工具栏上，单击“新建计算成员”。  
  
    新窗体将出现在“计算表达式”窗格中，可在该窗格内定义这个新计算成员的属性。 新成员还将出现在“脚本组织程序”窗格中。  
  
    下图显示单击“新建计算成员”时出现在“计算表达式”窗格中的窗体。  
  
    ![计算表达式窗格窗体](../analysis-services/media/l6-calculatedmembers-02.gif "计算表达式窗格窗体")  
  
3.  在“名称”框中，将计算度量值的名称更改为 **[Total Sales Amount]**。  
  
    如果计算成员的名称包含空格，则该计算成员名称必须放在方括号中。  
  
    请注意，在“父层次结构”列表中，默认情况下，将在“Measures”维度中创建新的计算成员。 通常，度量值维度中的计算成员也称为计算度量值。  
  
4.  在“计算”选项卡的“计算工具”窗格中的“元数据”选项卡上，依次展开“Measures”和“Internet Sales”，查看“Internet Sales”度量值组的元数据。  
  
    可以将元数据元素从“计算工具”窗格拖到“表达式”框中，然后添加运算符和其他元素，创建多维表达式 (MDX) 表达式。 或者，可以直接在“表达式”框中键入 MDX 表达式。  
  
    > [!NOTE]  
    > 如果无法在“计算工具”窗格中查看任何元数据，请在工具栏上单击“重新连接”。 如果该操作失败，则可能必须处理多维数据集，或启动 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例。  
  
5.  将“Internet Sales-Sales Amount”从“计算工具”窗格中的“元数据”选项卡拖到“计算表达式”窗格中的“表达式”框中。  
  
6.  在“表达式”框中，在 **[Measures].[Internet Sales-Sales Amount]** 后键入加号 (**+**)。  
  
7.  在“计算工具”窗格中的“元数据”选项卡上，展开“Reseller Sales”，然后将“Reseller Sales-Sales Amount”拖到“计算表达式”窗格的“表达式”框中的加号 (+) 后面。  
  
8.  在“格式字符串”列表中，选择“Currency”。  
  
9. 在“非空行为”列表中，选中“Internet Sales-Sales Amount”和“Reseller Sales-Sales Amount”的复选框，然后单击“确定”。  
  
    在“非空行为”列表中指定的度量值将用于解析 MDX 中的 NON EMPTY 查询。 在“非空行为”列表中指定一个或多个度量值时，如果所有指定的度量值为空，[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 将把计算成员视为空。 如果“非空行为”属性为空白，[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 必须对计算成员本身进行计算才能确定成员是否为空。  
  
    下图显示使用前面步骤中所指定的设置填充的“计算表达式”窗格。  
  
    ![Populated 计算表达式窗格](../analysis-services/media/l6-calculatedmembers-03.gif "填充计算表达式窗格")  
  
10. 在“计算”选项卡的工具栏上，单击“脚本视图”，然后在“计算表达式”窗格中检查计算脚本。  
  
    注意，新的计算将添加到初始 CALCULATE 表达式中；将以分号分隔每个单独的计算。 另外注意，在计算脚本的开始位置将出现注释。 在计算组的计算脚本中添加注释是好的做法，这样可以帮助您和其他开发人员理解复杂的计算脚本。  
  
11. 在计算脚本中的 **Calculate;** 命令之后和新添加的计算脚本之前添加一行，然后在脚本中独立的一行上添加以下文本：  
  
    ```  
    /* Calculations to aggregate Internet Sales and Reseller Sales measures */  
    ```  
  
    下图显示此时在教程中应该出现在“计算表达式”窗格中的计算脚本。  
  
    ![在计算表达式窗格中的脚本](../analysis-services/media/l6-calculatedmembers-04.gif "在计算表达式窗格中的脚本")  
  
12. 在“计算”选项卡的工具栏上，单击“窗体视图”，确认已在“脚本组织程序”窗格中选中“[Total Sales Amount]”，然后单击“新建计算成员”。  
  
13. 将这个新计算成员的名称更改为 **[Total Product Cost]**，然后在“表达式”框中创建以下表达式：  
  
    ```  
    [Measures].[Internet Sales-Total Product Cost] + [Measures].[Reseller Sales-Total Product Cost]  
    ```  
  
14. 在“格式字符串”列表中，选择“Currency”。  
  
15. 在“非空行为”列表中，选中“Internet Sales-Total Product Cost”和“Reseller Sales-Total Product Cost”的复选框，然后单击“确定”。  
  
    现已定义两个计算成员，它们都在“脚本组织程序”窗格中显示。 这些计算成员可以由随后在计算脚本中定义的其他计算来使用。 通过在“脚本组织程序”窗格中选择计算成员，可查看任何计算成员的定义；计算成员的定义将出现在窗体视图内的“计算表达式”窗格中。 在部署新定义的计算成员前，这些对象不会出现在“计算工具”窗格中。 计算不需要处理。  
  
## <a name="defining-gross-profit-margin-calculations"></a>定义毛利润率计算  
  
1.  确认已在“脚本组织程序”窗格中选中“[Total Product Cost]”，然后在“计算”选项卡的工具栏上单击“新建计算成员”。  
  
2.  在“名称”框中，将这个新计算度量值的名称更改为 **[Internet GPM]**。  
  
3.  在“表达式”框中，创建以下 MDX 表达式：  
  
    ```  
    ([Measures].[Internet Sales-Sales Amount] -   
    [Measures].[Internet Sales-Total Product Cost]) /  
    [Measures].[Internet Sales-Sales Amount]  
    ```  
  
4.  在“格式字符串”列表中，选择“Percent”。  
  
5.  在“非空行为”列表中，选中“Internet Sales-Sales Amount”的复选框，然后单击“确定”。  
  
6.  在“计算”选项卡的工具栏上，单击“新建计算成员”。  
  
7.  在“名称”框中，将这个新计算度量值的名称更改为 **[Reseller GPM]**。  
  
8.  在“表达式”框中，创建以下 MDX 表达式：  
  
    ```  
    ([Measures].[Reseller Sales-Sales Amount] -   
    [Measures].[Reseller Sales-Total Product Cost]) /  
    [Measures].[Reseller Sales-Sales Amount]  
    ```  
  
9. 在“格式字符串”列表中，选择“Percent”。  
  
10. 在“非空行为”列表中，选中“Reseller Sales-Sales Amount”的复选框，然后单击“确定”。  
  
11. 在“计算”选项卡的工具栏上，单击“新建计算成员”。  
  
12. 在“名称”框中，将此计算度量值的名称更改为 **[Total GPM]**。  
  
13. 在“表达式”框中，创建以下 MDX 表达式：  
  
    ```  
    ([Measures].[Total Sales Amount] -   
    [Measures].[Total Product Cost]) /  
    [Measures].[Total Sales Amount]  
    ```  
  
    注意，此计算成员引用了其他计算成员。 由于此计算成员将在它所引用的计算成员之后进行计算，所以这是有效的计算成员。  
  
14. 在“格式字符串”列表中，选择“Percent”。  
  
15. 在“非空行为”列表中，选中“Internet Sales-Sales Amount”和“Reseller Sales-Sales Amount”的复选框，然后单击“确定”。  
  
16. 在“计算”选项卡的工具栏上，单击“脚本视图”，然后检查刚才添加到计算脚本中的三个计算。  
  
17. 在计算脚本中紧接 **[Internet GPM]** 计算之前添加一行，然后在脚本中独立的一行上添加以下文本：  
  
    ```  
    /* Calculations to calculate gross profit margin */  
    ```  
  
    下图显示有三个新计算的“表达式”窗格。  
  
    ![在计算表达式窗格中的新计算](../analysis-services/media/l6-calculatedmembers-05.gif "在计算表达式窗格中的新计算")  
  
## <a name="defining-the-percent-of-total-calculations"></a>定义总计计算的百分比  
  
1.  在“计算”选项卡的工具栏上，单击“窗体视图”。  
  
2.  在“脚本组织程序”窗格中，选择“[Total GPM]”，然后在“计算”选项卡的工具栏上单击“新建计算成员”。  
  
    在单击“新建计算成员”之前单击“脚本组织程序”窗格中的最后一个计算成员，可以保证在脚本末尾输入新计算成员。 脚本按它们出现在“脚本组织程序”窗格中的顺序执行。  
  
3.  将这个新计算成员的名称更改为 **[Internet Sales Ratio to All Products]**。  
  
4.  在“表达式”框中键入以下表达式：  
  
    ```  
    Case  
        When IsEmpty( [Measures].[Internet Sales-Sales Amount] )   
        Then 0  
        Else ( [Product].[Product Categories].CurrentMember,  
               [Measures].[Internet Sales-Sales Amount]) /  
             ( [Product].[Product Categories].[(All)].[All],   
               [Measures].[Internet Sales-Sales Amount] )  
        End  
    ```  
  
    此 MDX 表达式将计算每个产品在总计 Internet 销售额中所占的比例。 Case 语句与 IS EMPTY 函数一起确保当产品没有销售额时不会发生被零除错误。  
  
5.  在“格式字符串”列表中，选择“Percent”。  
  
6.  在“非空行为”列表中，选中“Internet Sales-Sales Amount”的复选框，然后单击“确定”。  
  
7.  在“计算”选项卡的工具栏上，单击“新建计算成员”。  
  
8.  将此计算成员的名称更改为 **[Reseller Sales Ratio to All Products]**。  
  
9. 在“表达式”框中键入以下表达式：  
  
    ```  
    Case  
        When IsEmpty( [Measures].[Reseller Sales-Sales Amount] )   
        Then 0  
        Else ( [Product].[Product Categories].CurrentMember,  
               [Measures].[Reseller Sales-Sales Amount]) /  
             ( [Product].[Product Categories].[(All)].[All],   
               [Measures].[Reseller Sales-Sales Amount] )  
        End  
    ```  
  
10. 在“格式字符串”列表中，选择“Percent”。  
  
11. 在“非空行为”列表中，选中“Reseller Sales-Sales Amount”的复选框，然后单击“确定”。  
  
12. 在“计算”选项卡的工具栏上，单击“新建计算成员”。  
  
13. 将此计算成员的名称更改为 **[Total Sales Ratio to All Products]**。  
  
14. 在“表达式”框中键入以下表达式：  
  
    ```  
    Case  
        When IsEmpty( [Measures].[Total Sales Amount] )   
        Then 0  
        Else ( [Product].[Product Categories].CurrentMember,  
               [Measures].[Total Sales Amount]) /  
             ( [Product].[Product Categories].[(All)].[All],   
               [Measures].[Total Sales Amount] )  
        End  
    ```  
  
15. 在“格式字符串”列表中，选择“Percent”。  
  
16. 在“非空行为”列表中，选中“Internet Sales-Sales Amount”和“Reseller Sales-Sales Amount”的复选框，然后单击“确定”。  
  
17. 在“计算”选项卡的工具栏上，单击“脚本视图”，然后检查刚才添加到计算脚本中的三个计算。  
  
18. 在计算脚本中紧接 **[Internet Sales Ratio to All Products]** 计算之前添加新行，然后在脚本中独立的一行上添加以下文本：  
  
    ```  
    /* Calculations to calculate percentage of product to total product sales */  
    ```  
  
    现在总共定义了八个计算成员，位于“窗体”视图中时，这些成员将在“脚本组织程序”窗格中显示。  
  
## <a name="browsing-the-new-calculated-members"></a>浏览新计算成员  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 的“生成”菜单上，单击“部署 Analysis Services 教程”。  
  
2.  成功完成部署后，请切换到“浏览器”选项卡，然后单击“重新连接”。  
  
3.  单击 Excel 图标，然后单击“启用”。  
  
4.  在“数据透视表字段列表”窗格中，展开“值”文件夹，查看“Measures”维度中的新计算成员。  
  
5.  将“Total Sales Amount”拖到“值”区域中，然后检查结果。  
  
    将“Internet Sales-Sales Amount”和“Reseller Sales-Sales Amount”度量值从“Internet Sales”和“Reseller Sales”度量值组拖到“值”区域中。  
  
    请注意，“Total Sales Amount”度量值是“Internet Sales-Sales Amount”度量值与“Reseller Sales-Sales Amount”度量值之和。  
  
6.  将“Product Categories”用户定义层次结构添加到“报表筛选器”区域的筛选区域中，然后按“Mountain Bikes”对数据进行筛选。  
  
    请注意，“Total Sales Amount”度量值是基于“Mountain Bikes”的“Internet Sales-Sales Amount”和“Reseller Sales-Sales Amount”度量值，针对“Mountain Bikes”类别的产品销售额进行计算的。  
  
7.  将“Date.Calendar Date”用户定义层次结构添加到行标签区域，然后检查结果。  
  
    请注意，每个日历年的“Total Sales Amount”度量值是基于“Mountain Bikes”的“Internet Sales-Sales Amount”和“Reseller Sales-Sales Amount”度量值，针对“Mountain Bikes”类别的产品销售额进行计算的。  
  
8.  将“Total GPM”、“Internet GPM”和“Reseller GPM”度量值添加到“值”区域，然后检查结果。  
  
    请注意，分销商销售的毛利润率要比 Internet 销售低很多，如下图中所示。  
  
    ![数据窗格中显示的分销商销售额](../analysis-services/media/l6-calculatedmembers-7b.gif "数据窗格中显示的分销商销售额")  
  
9. 将“Total Sales Ratio to All Products”、“Internet Sales Ratio to All Products”和“Reseller Sales Ratio to All Products”度量值添加到“值”区域。  
  
    注意，Internet 销售的山地车销售额在所有产品中所占的比率随时间推移而增长，但在分销商那里却在随时间推移而减少。 另外注意，通过分销商销售的山地车销售额在所有产品中所占的比率低于通过 Internet 销售完成的该比率。  
  
10. 将筛选器从“Mountain Bikes”更改为“Bikes”，然后检查结果。  
  
    注意，通过分销商销售的所有自行车的毛利润率都是负数，这是因为观光自行车和道路自行车都在亏损销售。  
  
11. 将筛选器更改为“Accessories”，然后检查结果。  
  
    注意，附件的销售正在随时间而增长，但这些销售只构成总销售额的一小部分。 还要注意的是，附件销售的毛利润率比自行车还高。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
[定义命名集](../analysis-services/lesson-6-2-defining-named-sets.md)  
  
## <a name="see-also"></a>另请参阅  
[计算](../analysis-services/multidimensional-models-olap-logical-cube-objects/calculations.md)  
[多维模型中的计算](../analysis-services/multidimensional-models/calculations-in-multidimensional-models.md)  
[创建计算成员](../analysis-services/multidimensional-models/create-calculated-members.md)  
  
  
  
