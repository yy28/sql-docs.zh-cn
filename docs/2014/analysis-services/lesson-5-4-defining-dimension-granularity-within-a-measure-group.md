---
title: 定义度量值组中的维度粒度 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 4f079485-9eb4-405c-9a20-81258298b810
caps.latest.revision: 20
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.openlocfilehash: deeae89f59779000ac2dda9ca4da639666852bae
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36127619"
---
# <a name="defining-dimension-granularity-within-a-measure-group"></a>定义度量值组中的维度粒度
  用户可能需要针对不同目的定义不同粒度或专一性的事实数据表维度。 例如，分销商或 Internet 销售的销售额数据可以每天记录一次，而销售配额信息则可能按月或按季度级别来记录。 在这些情况下，用户可能需要时间维度针对这些不同的事实数据表具有不同的粒度或详细程度。 尽管可以将新的数据库维度定义为具有这种不同粒度的时间维度，但 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]提供了更简单的方法。  
  
 默认情况下，在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]中，当在度量值组中使用维度时，该维度内的数据粒度将基于该维度的键属性。 例如，当度量值组中包括时间维度并且时间维度的默认粒度为每天，则度量值组中该维度的默认粒度也为每天。 多数情况下这样是合适的，例如本教程中的“Internet 销售”和“分销商销售”度量值组便是恰当的示例。 但是，当其他类型的度量值组（例如“销售配额”或“预算”度量值组）中包括此类维度时，则使用每月粒度或每季度粒度更为合适。  
  
 若要为多维数据集维度指定默认粒度以外的粒度，则需要在多维数据集设计器的“维度用法”选项卡上修改特定度量值组中使用的多维数据集维度的粒度属性。 当您将特定度量值组中某一维度的粒度更改为该维度的键属性之外的属性时，必须保证该度量值组中的所有其他属性与这一新粒度属性直接或间接相关。 方法是在所有其他属性与被指定为度量值组中粒度属性的属性之间指定属性关系。 在这种情况下，可以定义其他属性关系，而不是移动属性关系。 对于维度中的其余属性而言，有效指定为粒度属性的属性将成为度量值组中的键属性。 如果未恰当指定属性关系，则 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 将无法正确地聚合值，您在本主题的各任务中会看到这种情况。  
  
 有关详细信息，请参阅 [维度关系](multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)、 [定义常规关系和常规关系属性](multidimensional-models/define-a-regular-relationship-and-regular-relationship-properties.md)。  
  
 在本主题的任务中，您将添加“销售配额”度量值组并将该度量值组中的“日期”维度的粒度定义为每月。 然后定义月属性和其他维度属性之间的属性关系，以确保 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 能够正确地聚合值。  
  
## <a name="adding-tables-and-defining-the-sales-quotas-measure-group"></a>添加表并定义“销售配额”度量值组  
  
1.  切换到 **Adventure Works DW 2012** 数据源视图。  
  
2.  右键单击任意位置**关系图组织程序**窗格中，单击**新关系图**，并将其命名关系图`Sales Quotas`。  
  
3.  拖动**员工**，**销售区域**，和`Date`表从**表**窗格**图**窗格。  
  
4.  右键单击“关系图”窗格中的任意位置并选择“添加/删除表”，以将 **FactSalesQuota** 表添加到“关系图”窗格中。  
  
     注意，**SalesTerritory**表通过 **Employee** 表链接到 **FactSalesQuota** 表。  
  
5.  检查 **FactSalesQuota** 表中的列，然后浏览此表中的数据。  
  
     注意，此表内数据的粒度为日历季度，该粒度的详细程度处于 FactSalesQuota 表中的最低级别。  
  
6.  在数据源视图设计器中，更改**FriendlyName**属性**FactSalesQuota**表`SalesQuotas`。  
  
7.  切换到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 多维数据集，再单击“多维数据集结构”选项卡。  
  
8.  右键单击任意位置**度量值**窗格中，单击**新建度量值组**，单击`SalesQuotas`中**新建度量值组**对话框框中，并依次**确定**。  
  
     `Sales Quotas`中会出现度量值组**度量值**窗格。 在**维度**窗格中，请注意，新`Date`也定义多维数据集维度，基于`Date`数据库维度。 因为 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 不了解与时间相关的哪个现有多维数据集维度与“销售配额”度量值组下面的 **FactSalesQuota** 事实数据表中的 **DateKey** 列相关，所以定义了与时间相关的新的多维数据集维度。 以后在本主题的其他任务中，您可以对此进行更改。  
  
9. 展开`Sales Quotas`度量值组。  
  
10. 在“度量值”窗格中，选择“销售额配额”，然后在“属性”窗口中将 **FormatString** 属性的值设置为 **Currency**。  
  
11. 选择**销售配额计数**测量，，然后键入`#,#`的值作为**FormatString**属性窗口中的属性。  
  
12. 删除**日历季度**度量值，从`Sales Quotas`度量值组。  
  
     [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 检测出“日历季度”度量值下的列是包含度量值的列。 但是，在本主题后面部分，您将使用该列和 CalendarYear 列包含的值将“销售配额”度量值组链接到“日期”维度。  
  
13. 在**度量值**窗格中，右键单击`Sales Quotas`度量值组，并依次**新度量值**。  
  
     将打开“新建度量值”对话框，其中包含使用类型为 **Sum** 的度量值的可用源列。  
  
14. 在**新度量值**对话框中，选择**非重复计数**中**用法**列表中，验证`SalesQuotas`中选择**源表**列表中，选择**EmployeeKey**中**源列**列表，，然后单击**确定**。  
  
     注意，将在名为“销售配额 1”的新度量值组中创建该度量值。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中的非重复计数度量值在它们自己的度量值组中创建，以最大程度地提高处理性能。  
  
15. 值更改**名称**属性**员工密钥非重复计数**测量到`Sales Person Count`，然后键入`#,#`的值作为**FormatString**属性。  
  
## <a name="browsing-the-measures-in-the-sales-quota-measure-group-by-date"></a>按日期浏览“销售配额”度量值组中的度量值  
  
1.  在“生成”菜单上，单击“部署 Analysis Services 教程”。  
  
2.  在部署成功完成后，在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教程多维数据集的多维数据集设计器中单击“浏览器”选项卡，再单击“重新连接”按钮。  
  
3.  单击 Excel 快捷方式，然后单击“启用”。  
  
4.  在数据透视表字段列表中，展开`Sales Quotas`度量值组，并将**销售额配额**测量到值区域。  
  
5.  展开“销售区域”维度，然后将“销售区域”用户定义层次结构添加到行标签。  
  
     注意，“销售区域”多维数据集维度没有与 Fact Sales Quota 表直接或间接相关，如下图所示。  
  
     ![销售区域多维数据集维度](../../2014/tutorials/media/l5-granularity-2.gif "销售区域多维数据集维度")  
  
     在本主题的下一系列步骤中，您将在该维度和该事实数据表之间定义引用维度关系。  
  
6.  将“销售区域”用户层次结构从“行标签”区域移到“列标签”区域。  
  
7.  在数据透视表字段列表中，选择“销售区域”用户层次结构，然后单击右侧的向下箭头。  
  
     ![字段列表中的销售区域层次结构](../../2014/tutorials/media/l5-granularity-1a.png "字段列表中的销售区域层次结构")  
  
8.  在筛选器中，单击“全选”复选框以取消选中所有选择，然后仅选择 **North America**。  
  
     ![筛选器窗格中选择北美](../../2014/tutorials/media/l5-granularity-1b.png "用于选择北美的筛选器窗格")  
  
9. 在数据透视表字段列表中，展开`Date`。  
  
10. 将 **Date.Fiscal Date** 用户层次结构拖到行标签  
  
11. 在数据透视表中，单击“行标签”旁的向下箭头。 取消选中除 **FY 2008**之外的所有年份。  
  
     请注意，只有**2007 年 7 月**的成员**月**级别显示，而不是**2007 年 7 月，**， **2007 年 8 月，**，和**2007 年 9 月，** 的成员**月**级别，并且仅**2007 年 7 月 1 日**的成员`Date`级别显示，而不是所有的 31 天。 出现此行为的事实数据表中的数据粒度是按季度级别和最粒度因为`Date`维度是每日级别。 在本主题的下一个任务中，您可以对此行为进行更改。  
  
     另注意，月份级别和日级别以及季度级别的“销售额配额”值相同，都为 $13,733,000.00。 这是因为“销售配额”度量值组中最低的数据级别为季度级别。 你可以在第 6 课中更改此行为。  
  
     下图显示了“销售额配额”的值。  
  
     ![值的销售金额配额](../../2014/tutorials/media/l5-granularity-3.png "值的销售金额配额")  
  
## <a name="defining-dimension-usage-properties-for-the-sales-quotas-measure-group"></a>定义“销售配额”度量值组的维度用法属性  
  
1.  打开“雇员”维度的维度设计器，右键单击“数据源视图”窗格中的 **SalesTerritoryKey**，然后单击“从列新建属性”。  
  
2.  在“属性”窗格中，选择 **SalesTerritoryKey**，然后在“属性”窗口中，将 **AttributeHierarchyVisible** 属性设置为 **False**，将 **AttributeHierarchyOptimizedState** 属性设置为 **NotOptimized**，并将 **AttributeHierarchyOrdered** 属性设置为 **False**。  
  
     此属性需要链接**销售区域**维度到`Sales Quotas`和**销售配额 1**作为引用维度的度量值组。  
  
3.  在多维数据集设计器中为[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]教程多维数据集，请单击**维度用法**选项卡，然后查看内的维度用法`Sales Quotas`和**销售配额 1**度量值组。  
  
     请注意，**员工**和`Date`多维数据集维度链接到**销售 Quotasand 销售配额 1**度量值组通过常规关系。 另外注意，“销售区域”多维数据集维度未链接到这些度量值组中的任何一组。  
  
4.  单击的交叉点处的单元格**销售区域**维度和`Sales Quotas`度量值组，然后单击浏览按钮 (**...**). 将打开“定义关系”对话框。  
  
5.  在“选择关系类型”列表中，选择“被引用的”。  
  
6.  在“中间维度”列表中，选择“雇员”。  
  
7.  在“引用维度属性”列表中，选择“销售区域所属地区”。  
  
8.  在“中间维度属性”列表中，选择“销售区域关键字”。 （“销售区域所属地区”属性的键列为 SalesTerritoryKey 列。）  
  
9. 验证是否选中了“具体化”复选框。  
  
10. 单击“确定” 。  
  
11. 单击“销售区域”维度和“销售配额 1”度量值组相交处的单元，然后单击浏览按钮 (**…**)。 将打开“定义关系”对话框。  
  
12. 在“选择关系类型”列表中，选择“被引用的”。  
  
13. 在“中间维度”列表中，选择“雇员”。  
  
14. 在“引用维度属性”列表中，选择“销售区域所属地区”。  
  
15. 在“中间维度属性”列表中，选择“销售区域关键字”。 （“销售区域所属地区”属性的键列为 SalesTerritoryKey 列。）  
  
16. 验证是否选中了“具体化”复选框。  
  
17. 单击“确定” 。  
  
18. 删除`Date`多维数据集维度。  
  
     而不是有四个时间相关的多维数据集维度，你将使用**订单日期**中的多维数据集维度`Sales Quotas`为日期将依据标注销售配额的度量值组。 还会将此多维数据集维度用作多维数据集中的主日期维度。  
  
19. 在**维度**列表中，重命名**订单日期**多维数据集维度与`Date`。  
  
     重命名**订单日期**多维数据集维度与`Date`使用户更轻松地了解其角色中此多维数据集的主日期维度相同。  
  
20. 单击浏览按钮 (**...**) 的交叉点处的单元格中`Sales Quotas`度量值组和`Date`维度。  
  
21. 在“定义关系”对话框中，选择“选择关系类型”列表中的“常规”。  
  
22. 在“粒度属性”列表中，选择“日历季度”。  
  
     注意此时会出现一个警告，它指出由于已选择非键属性作为粒度属性，所以必须通过将所有其他属性指定为成员属性来确保它们与粒度属性直接或间接相关。  
  
23. 在“定义关系”对话框的“关系”区域中，将“日期”多维数据集维度下面表中的 **CalendarYear** 和 **CalendarQuarter** 维度列链接到“销售配额”度量值组下面表中的 **CalendarYear** 和 **CalendarQuarter** 列，然后单击“确定”。  
  
    > [!NOTE]  
    >  “日历季度”定义为“销售配额”度量值组中“日期”多维数据集维度的粒度属性，但“日期”属性仍作为“Internet 销售”和“分销商”度量值组的粒度属性。  
  
24. 对 **Sales Quotas 1** 度量值组重复前面的四个步骤。  
  
## <a name="defining-attribute-relationships-between-the-calendar-quarter-attribute-and-the-other-dimension-attributes-in-the-date-dimension"></a>定义“日期”维度中“日历季度”属性和其他维度属性之间的属性关系  
  
1.  切换到**维度设计器**为`Date`维度，并依次**属性关系**选项卡。  
  
     请注意，尽管**日历年**链接到**日历季度**通过**日历半期**属性，属性链接到一个仅会计日历另一个;它们未链接到**日历季度**属性，因此将不聚合中正确`Sales Quotas`度量值组。  
  
2.  在关系图中，右键单击“日历季度”属性，然后选择“新建属性关系”。  
  
3.  在“创建属性关系”对话框中，“源属性”是“日历季度”。 将“相关属性”设置为“会计季度”。  
  
4.  单击“确定” 。  
  
     请注意，一条警告消息显示消息，指出`Date`维度包含一个或多个冗余属性关系可能导致数据无法聚合有非键属性用作粒度属性。  
  
5.  请删除“月份名称”属性和“会计季度”属性之间的属性关系。  
  
6.  在“文件”  菜单上，单击“全部保存” 。  
  
## <a name="browsing-the-measures-in-the-sales-quota-measure-group-by-date"></a>按日期浏览“销售配额”度量值组中的度量值  
  
1.  在“生成”菜单上，单击“部署 Analysis Services 教程”。  
  
2.  部署成功完成后，在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教程多维数据集的多维数据集设计器中单击“浏览器”选项卡，再单击“重新连接”。  
  
3.  单击 Excel 快捷方式，然后单击“启用”。  
  
4.  将“销售配额”度量值拖到“值”区域。  
  
5.  将“销售区域”用户层次结构拖到列标签，然后筛选 **North America**。  
  
6.  将 **Date.FiscalDate** 用户层次结构拖到行标签，然后在数据透视表上单击“行标签”旁的向下箭头，并且取消选中除了 **FY 2008** 之外的所有复选框，以便只显示会计年度 2008。  
  
7.  单击“确定”。  
  
8.  依次展开 **FY 2008**、 **H1 FY 2008**以及 **Q1 FY 2008**。  
  
     下图显示了 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 多维数据集的数据透视表，其中正确定义了“销售配额”度量值组维度。  
  
     请注意，会计季度级别的每个成员都具有与季度级别相同的值。 以 **Q1 FY 2008** 为例， **Q1 FY 2008** 的 $9,180,000.00 的配额也是其每个成员的值。 出现此行为是因为事实数据表中数据的粒度属于季度级别，“日期”维度的粒度也属于季度级别。 在第 6 课中，你将了解如何按比例将季度量分配到每个月。  
  
     ![销售配额度量值组维度正确](../../2014/tutorials/media/l5-granularity-7.gif "正确进行维度化的销售配额度量值组")  
  
## <a name="next-lesson"></a>下一课  
 [第 6 课： 定义计算]((课程-6-定义-calculations.md)  
  
## <a name="see-also"></a>请参阅  
 [维度关系](multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)   
 [定义常规关系和常规关系属性](multidimensional-models/define-a-regular-relationship-and-regular-relationship-properties.md)   
 [使用数据源视图设计器中的关系图&#40;Analysis Services&#41;](multidimensional-models/work-with-diagrams-in-data-source-view-designer-analysis-services.md)  
  
  