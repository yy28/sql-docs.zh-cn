---
title: 修改日期维度 |Microsoft 文档
ms.custom: ''
ms.date: 03/01/2017
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
ms.assetid: 4689d780-4bf6-4cf8-8fde-eb3f15dd668a
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 3809c857622be453ee8a8347d6b2f10e48139e18
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="lesson-3-4---modifying-the-date-dimension"></a>Lesson 3-4-修改日期维度
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

在本主题的各任务中，将创建用户定义的层次结构，并更改为“日期”、“月份”、“日历季度”以及“日历半期”等属性显示的成员名称。 还将为属性定义组合键，控制维度成员的排序顺序以及定义属性关系。  
  
## <a name="adding-a-named-calculation"></a>添加命名计算  
可以向数据源视图的表中添加命名计算，命名计算是一个表示为计算列的 SQL 表达式。 该表达式的显示形式和工作方式类似于表中的列。 通过命名计算，不必修改基础数据源中的表即可扩展数据源视图中现有表的关系架构。 有关详细信息，请参阅 [在数据源视图中定义命名计算 (Analysis Services)](../analysis-services/multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)  
  
#### <a name="to-add-a-named-calculation"></a>添加命名计算  
  
1.  若要打开 **Adventure Works DW 2012** 数据源视图，请在解决方案资源管理器中的“数据源视图”文件夹中双击此视图。  
  
2.  在“表”窗格底部附近，右键单击“日期”，然后单击“新建命名计算”。  
  
3.  在“创建命名计算”对话框中，在“列名”框中键入 **SimpleDate**，然后在“表达式”框中键入或复制并粘贴以下 **DATENAME** 语句：  
  
    ```  
    DATENAME(mm, FullDateAlternateKey) + ' ' +  
    DATENAME(dd, FullDateAlternateKey) + ', ' +  
    DATENAME(yy, FullDateAlternateKey)  
    ```  
  
    该 **DATENAME** 语句从 FullDateAlternateKey 列中提取年、月和日的值。 将此新列用作 FullDateAlternateKey 属性的显示名称。  
  
4.  单击“确定”，然后展开“表”窗格中的“日期”。  
  
    **SimpleDate** 命名计算显示在 Date 表中列的列表中，由一个图标指示它是命名计算。  
  
5.  在“文件”  菜单上，单击“全部保存” 。  
  
6.  在“表”窗格中，右键单击“日期”，然后单击“浏览数据”。  
  
7.  滚动到右侧，以查看“浏览 Date 表”视图中的最后一列。  
  
    注意，**SimpleDate** 列显示在数据源视图中，正确串联基础数据源中多个列的数据，而无需修改原始数据源。  
  
8.  关闭“浏览 Date 表”视图。  
  
## <a name="using-the-named-calculation-for-member-names"></a>将命名计算用于成员名称  
在数据源视图中创建命名计算后，可以将命名计算用作特性的属性。  
  
#### <a name="to-use-the-named-calculation-for-member-names"></a>将命名计算用于成员名称  
  
1.  打开 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中的“日期”维度的“维度设计器”。 为此，请双击“解决方案资源管理器”的“维度”节点的“日期”维度。  
  
2.  在“维度结构”选项卡的“属性”窗格中，单击“日期键”属性。  
  
3.  如果未打开“属性”窗口，则打开“属性”窗口，然后单击标题栏上的“自动隐藏”按钮，以便该窗口保持打开状态。  
  
4.  单击此窗口底部附近的 **NameColumn** 属性字段，然后单击省略号浏览 (**…**) 按钮以打开“名称列”对话框。  
  
5.  选择位于“源列”列表底部的 **SimpleDate**，然后单击“确定”。  
  
6.  在“文件”  菜单上，单击“全部保存” 。  
  
## <a name="creating-a-hierarchy"></a>创建层次结构  
通过将属性从“属性”窗格拖至“层次结构”窗格可以创建新的层次结构。  
  
#### <a name="to-create-a-hierarchy"></a>创建层次结构  
  
1.  在“日期”维度的维度设计器的“维度结构”选项卡中，将“日历年”属性从“属性”窗格拖动到“层次结构”窗格中。  
  
2.  将“日历半期”属性从“属性”窗格拖动到“层次结构”窗格中“日历年”级别下方的 <new level> 单元格中。  
  
3.  将“日历季度”属性从“属性”窗格拖动到“层次结构”窗格中“日历半期”级别下方的 <new level> 单元格中。  
  
4.  将“英语月份名称”属性从“属性”窗格拖动到“层次结构”窗格中“日历季度”级别下方的 <new level> 单元格中。  
  
5.  将“日期键”属性从“属性”窗格拖动到“层次结构”窗格中“英语月份名称”级别下方的 <new level> 单元格中。  
  
6.  在“层次结构”窗格中，右键单击“层次结构”层次结构的标题栏，单击“重命名”，然后键入“日历日期”。  
  
7.  通过使用右键单击上下文菜单，在“日历日期”层次结构中，将“英语月份名称”级别重命名为“日历月份”，并将“日期键”级别重命名为“日期”。  
  
8.  因为不需要使用“完整日期备用键”属性，所以将其从“属性”窗格中删除。 在“删除对象”确认窗口中单击“确定”。  
  
9. 在“文件”  菜单上，单击“全部保存” 。  
  
## <a name="defining-attribute-relationships"></a>定义属性关系  
如果基础数据支持，则应定义属性间的属性关系。 定义属性关系可加快维度、分区和查询处理的速度。  
  
#### <a name="to-define-attribute-relationships"></a>定义属性关系  
  
1.  在“日期”维度的“维度设计器”中，单击“属性关系”选项卡。  
  
2.  在关系图中，右键单击“英语月份名称”属性，然后单击“新建属性关系”。  
  
3.  在“创建属性关系”对话框中，“源属性”是“英语月份名称”。 将“相关属性”设置为“日历季度”。  
  
4.  在“关系类型”列表中，将关系类型设置为“刚性”。  
  
    因为各成员之间的关系不会随时间变化，所以此关系类型为“刚性”。  
  
5.  单击 **“确定”**。  
  
6.  在关系图中，右键单击“日历季度”属性，然后单击“新建属性关系”。  
  
7.  在“创建属性关系”对话框中，“源属性”是“日历季度”。 将“相关属性”设置为“日历半期”。  
  
8.  在“关系类型”列表中，将关系类型设置为“刚性”。  
  
9. 单击 **“确定”**。  
  
10. 在关系图中，右键单击“日历半期”属性，然后单击“新建属性关系”。  
  
11. 在“创建属性关系”对话框中，“源属性”是“日历半期”。 将“相关属性”设置为“日历年”。  
  
12. 在“关系类型”列表中，将关系类型设置为“刚性”。  
  
13. 单击 **“确定”**。  
  
14. 在“文件”  菜单上，单击“全部保存” 。  
  
## <a name="providing-unique-dimension-member-names"></a>提供唯一的维度成员名称  
在此任务中，将创建由 **EnglishMonthName****CalendarQuarter** 和 **CalendarSemester** 属性使用的用户友好名称列。  
  
#### <a name="to-provide-unique-dimension-member-names"></a>提供唯一的维度成员名称  
  
1.  若要切换到 **[!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] DW 2012** 数据源视图，请在解决方案资源管理器中的“数据源视图”文件夹中双击此视图。  
  
2.  在“表”窗格中，右键单击“日期”，然后单击“新建命名计算”。  
  
3.  在“创建命名计算”对话框中，在“列名”框中键入 **MonthName**，然后在“表达式”框中键入或复制并粘贴以下语句：  
  
    ```  
    EnglishMonthName+' '+ CONVERT(CHAR (4), CalendarYear)  
    ```  
  
    该语句将表中每月的月份和年份连接成一个新列。  
  
4.  单击 **“确定”**。  
  
5.  在“表”窗格中，右键单击“日期”，然后单击“新建命名计算”。  
  
6.  在“创建命名计算”对话框的“列名”框中键入 **CalendarQuarterDesc**，然后在“表达式”框中键入或复制并粘贴以下 SQL 脚本：  
  
    ```  
    'Q' + CONVERT(CHAR (1), CalendarQuarter) +' '+ 'CY ' +  
    CONVERT(CHAR (4), CalendarYear)  
    ```  
  
    该 SQL 脚本将表中每季度的日历季度和年份连接成一个新列。  
  
7.  单击 **“确定”**。  
  
8.  在“表”窗格中，右键单击“日期”，然后单击“新建命名计算”。  
  
9. 在“创建命名计算”对话框的“列名”框中键入 **CalendarSemesterDesc**，然后在“表达式”框中键入或复制并粘贴以下 SQL 脚本：  
  
    ```  
    CASE  
    WHEN CalendarSemester = 1 THEN 'H1' + ' ' + 'CY' + ' '   
           + CONVERT(CHAR(4), CalendarYear)  
    ELSE  
    'H2' + ' ' + 'CY' + ' ' + CONVERT(CHAR(4), CalendarYear)  
    END  
    ```  
  
    该 SQL 脚本将表中每半期的日历半期和年份连接成一个新列。  
  
10. 单击 **“确定”**。  
  
11. 在“文件”  菜单上，单击“全部保存” 。  
  
## <a name="defining-composite-keycolumns-and-setting-the-name-column"></a>定义组合的 KeyColumns 和设置名称列  
**KeyColumns** 属性中包含表示特性键的一个或多个列。 在本任务中，将定义组合的 **KeyColumns**。  
  
#### <a name="to-define-composite-keycolumns-for-the-english-month-name-attribute"></a>为“英语月份名称”属性定义组合的 KeyColumns  
  
1.  打开“日期”维度的“维度结构”选项卡。  
  
2.  在“属性”窗格中，单击“英语月份名称”属性。  
  
3.  在“属性”窗口中，单击 **KeyColumns** 字段，然后单击浏览 (**...**) 按钮。  
  
4.  在“键列”对话框的“可用列”列表中，选择 **CalendarYear** 列，然后单击“>”按钮。  
  
5.  现在，**EnglishMonthName** 和 **CalendarYear** 列会显示在“键列”列表中。  
  
6.  单击 **“确定”**。  
  
7.  若要设置 **EnglishMonthName** 特性的 **NameColumn** 属性，请单击“属性”窗口中的 **NameColumn** 字段，然后单击浏览 (**...**) 按钮。  
  
8.  在“名称列”对话框的“源列”列表中，选择 **MonthName**，然后单击“确定”。  
  
9. 在“文件”  菜单上，单击“全部保存” 。  
  
#### <a name="to-define-composite-keycolumns-for-the-calendar-quarter-attribute"></a>为“日历季度”属性定义组合的 KeyColumns  
  
1.  在“属性”窗格中，单击“日历季度”属性。  
  
2.  在“属性”窗口中，单击 **KeyColumns** 字段，然后单击浏览 (**...**) 按钮。  
  
3.  在“键列”对话框的“可用列”列表中，选择 **CalendarYear** 列，然后单击“>”按钮。  
  
    现在，**CalendarQuarter** 和 **CalendarYear** 列会显示在“键列”列表中。  
  
4.  单击 **“确定”**。  
  
5.  若要设置“日历季度”特性的 **NameColumn** 属性，请单击“属性”窗口的 **NameColumn** 字段，然后单击浏览 (**...**) 按钮。  
  
6.  在“名称列”对话框的“源列”列表中，选择 **CalendarQuarterDesc**，然后单击“确定”。  
  
7.  在“文件”  菜单上，单击“全部保存” 。  
  
#### <a name="to-define-composite-keycolumns-for-the-calendar-semester-attribute"></a>为“日历半期”属性定义组合的 KeyColumns  
  
1.  在在“属性”窗格中，单击“日历半期”属性。  
  
2.  在“属性”窗口中，单击 **KeyColumns** 字段，然后单击浏览 (**...**) 按钮。  
  
3.  在“键列”对话框的“可用列”列表中，选择 **CalendarYear** 列，然后单击“>”按钮。  
  
    现在，**CalendarSemester** 和 **CalendarYear** 列会显示在“键列”列表中。  
  
4.  单击 **“确定”**。  
  
5.  若要设置“日历半期”特性的 **NameColumn** 属性，请单击“属性”窗口的 **NameColumn** 字段，然后单击浏览 (**...**) 按钮。  
  
6.  在“名称列”对话框的“源列”列表中，选择 **CalendarSemesterDesc**，然后单击“确定”。  
  
7.  在“文件”  菜单上，单击“全部保存” 。  
  
## <a name="deploying-and-viewing-the-changes"></a>部署和查看更改  
更改属性和层次结构后，必须部署更改并重新处理相关对象，然后才能查看这些更改。  
  
#### <a name="to-deploy-and-view-the-changes"></a>部署和查看更改  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 的“生成”菜单中，单击“部署 Analysis Services 教程”。  
  
2.  在收到“部署成功完成”消息后，单击“日期”维度的“维度设计器”的“浏览器”选项卡，然后单击设计器工具栏上的“重新连接”图标。  
  
3.  从“层次结构”列表中选择“日历季度”。 查看“日历季度”属性层次结构的成员。  
  
    注意，由于创建了要用作名称的命名计算，因此，“日历季度”属性层次结构的成员名称更明确且更易于使用。 成员现在位于每年每个季度的“日历季度”属性层次结构中。 成员不是按时间顺序排序的。 相反，它们先按季度然后按年份进行排序。 在本主题的下一个任务中，您将修改此行为，以先按年然后按季度对此属性的层次结构成员进行排序。  
  
4.  查看“英语月份名称”和“日历半期”属性层次结构的成员。  
  
    注意，这些层次结构的成员也不是按时间顺序排序的。 相反，它们先分别按月或半期然后按年份进行排序。 在本主题的下一个任务中，您将修改此行为以更改这种排序顺序。  
  
## <a name="changing-the-sort-order-by-modifying-composite-key-member-order"></a>通过修改组合键成员顺序来更改排序顺序  
在本任务中，您将通过更改组成组合键的键顺序来更改排序顺序。  
  
#### <a name="to-modify-the-composite-key-member-order"></a>修改组合键成员顺序  
  
1.  打开“日期”维度的维度设计器的“维度结构”选项卡，然后在“属性”窗格中选择“日历半期”。  
  
2.  在“属性”窗口中，查看 **OrderBy** 属性的值。 它被设置为“键”。  
  
    “日历半期”属性层次结构的成员按其键值进行排序。 使用组合键，成员键首先基于第一个成员键的值，然后基于第二个成员键的值进行排序。 换言之，“日历半期”属性层次结构的成员首先按半期、然后按年份进行排序。  
  
3.  在“属性”窗口中，单击省略号浏览按钮 (**...**)，以更改 **KeyColumns** 属性值。  
  
4.  在“键列”对话框的“键列”列表中，验证是否选中了 **CalendarSemester**，然后单击向下箭头以反转该组合键成员的顺序。 单击 **“确定”**。  
  
    现在，属性层次结构成员首先按年份、然后按半期进行排序。  
  
5.  在“特性”窗格中，选择“日历季度”，然后单击“属性”窗口中 **KeyColumns** 属性的省略号浏览按钮 (**...**)。  
  
6.  在“键列”对话框的“键列”列表中，验证是否选中了 **CalendarQuarter**，然后单击向下箭头以反转该组合键成员的顺序。 单击 **“确定”**。  
  
    现在，属性层次结构成员首先按年份、然后按季度进行排序。  
  
7.  在“特性”窗格中，选择“英语月份名称”，然后单击“属性”窗口中 **KeyColumns** 属性的省略号按钮 (**...**)。  
  
8.  在“键列”对话框的“键列”列表中，验证是否选中了 **EnglishMonthName**，然后单击向下箭头以反转该组合键成员的顺序。 单击 **“确定”**。  
  
    现在，属性层次结构成员首先按年份、然后按月份进行排序。  
  
9. 在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 的“生成”菜单上，单击“部署 Analysis Services 教程”。 部署成功完成后，在“日期”维度的维度设计器中单击“浏览器”选项卡。  
  
10. 在“浏览器”项卡的工具栏上，单击“重新连接”按钮。  
  
11. 查看“日历季度”和“日历半期”属性层次结构的成员。  
  
    注意，这些层次结构的成员现在按时间顺序排序，首先按年份、然后分别按季度或半期排序。  
  
12. 查看“英语月份名称”属性层次结构的成员。  
  
    注意，层次结构成员首先按年份然后按月份的字母顺序排序。 这是因为“数据源”视图中 EnglishCalendarMonth 列的数据类型是字符串列，它基于基础关系数据库中的 nvarchar 数据类型。 有关如何对每年内的月份按时间顺序进行排序的信息，请参阅 [根据辅助属性对属性成员进行排序](../analysis-services/lesson-4-5-sorting-attribute-members-based-on-a-secondary-attribute.md)。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
[浏览已部署的多维数据集](../analysis-services/lesson-3-5-browsing-the-deployed-cube.md)  
  
## <a name="see-also"></a>另请参阅  
[多维模型中的维度](../analysis-services/multidimensional-models/dimensions-in-multidimensional-models.md)  
  
