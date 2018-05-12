---
title: 4-6-指定用户定义层次结构中的属性关系 |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 712172f7c74e1c7efa7766ce4c25a9a8fca173f0
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="4-6-specifying-attribute-relationships-in-user-defined-hierarchy"></a>4-6-指定用户定义层次结构中的属性关系
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

您已了解本教程中的内容，现在可以将属性层次结构组织到用户层次结构内的级别中，以便在多维数据集中为用户提供导航路径。 用户层次结构可以表示自然层次结构（如市/县、州/省/自治区和国家/地区），或者可以只表示导航路径（如雇员姓名、职务和部门名称）。 对于在层次结构中导航的用户而言，这两类用户层次结构应相同。  
  
使用自然层次结构时，如果定义了组成级别的属性之间的属性关系，则 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 可以使用某个属性的聚合来获取相关属性的结果。 如果属性之间没有定义的关系，则 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 将根据键属性聚合所有非键属性。 因此，如果基础数据支持，则应定义属性间的属性关系。 定义属性关系可改进维度、分区和查询处理性能。 有关详细信息，请参阅[定义属性关系](../analysis-services/multidimensional-models/attribute-relationships-define.md)和[属性关系](../analysis-services/multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md)。  
  
在定义属性关系时，可以指定此关系是弹性的还是刚性的。 如果您将关系定义为刚性，则 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 会在更新维度时保留聚合。 如果实际过程更改了定义为刚性的关系，那么除非维度得到完全处理，否则 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 将在处理过程中生成错误。 指定适当的关系和关系属性，可提高查询和处理性能。 有关详细信息，请参阅 [定义属性关系](../analysis-services/multidimensional-models/attribute-relationships-define.md)和 [用户层次结构属性](../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md)。  
  
在本主题的各个任务中，您将为 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 项目的自然用户层次结构中的属性定义属性关系。 这些层次结构包括“客户”维度中的“客户所在地域”层次结构、“销售区域”维度中的“销售区域”层次结构、“产品”维度中的“产品型号系列”层次结构，以及“日期”维度中的“会计日期”和“日历日期”层次结构。 这些用户层次结构全部是自然层次结构。  
  
## <a name="defining-attribute-relationships-for-attributes-in-the-customer-geography-hierarchy"></a>为“客户所在地域”层次结构中的属性定义属性关系  
  
1.  切换到“客户”维度的维度设计器，然后单击“维度结构”选项卡。  
  
    在“层次结构”窗格中，请注意“客户所在地域”用户定义层次结构中的级别。 此层次结构当前只是用户的向下钻取路径，因为在级别或属性之间未定义任何关系。  
  
2.  单击 **“属性关系”** 选项卡。  
  
    请注意用于将 **Geography** 表的非键属性链接到 **Geography** 表的键属性的 4 个属性关系。 “地域”属性与“全名”属性相关。 由于“邮政编码”链接到“地域”属性，“地域”属性链接到“全名”属性，所以“邮政编码”属性通过“地域”属性间接链接到“全名”属性。 接下来，我们将更改属性关系，以便它们不使用“地域”属性。  
  
3.  在关系图中，右键单击“全名”属性，然后选择“新建属性关系”。  
  
4.  在“创建属性关系”对话框中，“源属性”是“全名”。 将“相关属性”设置为“邮政编码”。 因为各成员之间的关系会随时间变化，所以在“关系类型”列表中，将关系类型设置保留为“柔性”。  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    因为此关系是冗余关系，所以在关系图中会显示警告图标。 “全名” -> “地域”-> “邮政编码”关系已经存在，而且你刚创建了“全名” -> “邮政编码”关系。 现在，“地域”-> “邮政编码”关系是冗余的，因此要将其删除。  
  
6.  在“属性关系”窗格中，右键单击“地域”-> “邮政编码”，然后单击“删除”。  
  
7.  显示“删除对象”对话框时，单击“确定”。  
  
8.  在关系图中，右键单击“邮政编码”属性，然后选择“新建属性关系”。  
  
9. 在“创建属性关系”对话框中，“源属性”是“邮政编码”。 将“相关属性”设置为“市县”。 在“关系类型”列表中，将关系类型设置保留为“柔性”。  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    现在，“地域”-> “市县”关系是冗余的，因此要将其删除。  
  
11. 在“属性关系”窗格中，右键单击“地域”-> “市县”，然后单击“删除”。  
  
12. 显示“删除对象”对话框时，单击“确定”。  
  
13. 在关系图中，右键单击“市县”属性，然后选择“新建属性关系”。  
  
14. 在“创建属性关系”对话框中，“源属性”是“市县”。 将“相关属性”设置为“省/市/自治区”。 因为市/县与州/省/自治区之间的关系将不会随着时间推移而更改，所以在“关系类型”列表中将关系类型设置为“刚性”。  
  
15. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
16. 右键单击“地域”和“省/市/自治区”之间的箭头，然后单击“删除”。  
  
17. 显示“删除对象”对话框时，单击“确定”。  
  
18. 在关系图中，右键单击“省/市/自治区”属性，然后选择“新建属性关系”。  
  
19. 在“创建属性关系”对话框中，“源属性”是“省/市/自治区”。 将“相关属性”设置为“国家/地区-区域”。 因为州/省/自治区与国家/地区区域之间的关系将不会随着时间的推移而更改，所以在“关系类型”列表中，将关系类型设置为“刚性”。  
  
20. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
21. 在“属性关系”窗格中，右键单击“地域”-> “国家/地区-区域”，然后单击“删除”。  
  
22. 显示“删除对象”对话框时，单击“确定”。  
  
23. 单击“维度结构”选项卡。  
  
    请注意，在你删除“地域”和其他属性之间的最后一个属性关系后，“地域”本身也将被删除。 这是因为不再使用该属性。  
  
24. 在“文件”菜单上，单击“全部保存”。  
  
## <a name="defining-attribute-relationships-for-attributes-in-the-sales-territory-hierarchy"></a>为“销售区域”层次结构中的属性定义属性关系  
  
1.  打开“销售区域”维度的维度设计器，然后单击“属性关系”选项卡。  
  
2.  在关系图中，右键单击“销售区域所属国家/地区”属性，然后选择“新建属性关系”。  
  
3.  在“创建属性关系”对话框中，“源属性”是“销售区域所属国家/地区”。 将“相关属性”设置为“销售区域组”。 在“关系类型”列表中，将关系类型设置保留为“柔性”。  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    “销售区域组”现已链接到“销售区域所属国家”，而“销售区域所属国家”现已链接到“销售区域所属地区”。 因为一个国家/地区内的区域分组以及国家/地区的分组都可能会随着时间的推移而更改，所以每种关系的 **RelationshipType** 属性都设置为“柔性”。  
  
## <a name="defining-attribute-relationships-for-attributes-in-the-product-model-lines-hierarchy"></a>为“产品型号系列”层次结构中的属性定义属性关系  
  
1.  打开“产品”维度的维度设计器，然后单击“属性关系”选项卡。  
  
2.  在关系图中，右键单击“型号名称”属性，然后选择“新建属性关系”。  
  
3.  在“创建属性关系”对话框中，“源属性”是“型号名称”。 将“相关属性”设置为“产品系列”。 在“关系类型”列表中，将关系类型设置保留为“柔性”。  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="defining-attribute-relationships-for-attributes-in-the-fiscal-date-hierarchy"></a>为“会计日期”层次结构中的属性定义属性关系  
  
1.  切换到“日期”维度的维度设计器，然后单击“属性关系”选项卡。  
  
2.  在关系图中，右键单击“月份名称”属性，然后选择“新建属性关系”。  
  
3.  在“创建属性关系”对话框中，“源属性”是“月份名称”。 将“相关属性”设置为“会计季度”。 在“关系类型”列表中，将关系类型设置为“刚性”。  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  在关系图中，右键单击“会计季度”属性，然后选择“新建属性关系”。  
  
6.  在“创建属性关系”对话框中，“源属性”是“会计季度”。 将“相关属性”设置为“会计半期”。 在“关系类型”列表中，将关系类型设置为“刚性”。  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  在关系图中，右键单击“会计半期”属性，然后选择“新建属性关系”。  
  
9. 在“创建属性关系”对话框中，“源属性”是“会计半期”。 将“相关属性”设置为“会计年度”。 在“关系类型”列表中，将关系类型设置为“刚性”。  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="defining-attribute-relationships-for-attributes-in-the-calendar-date-hierarchy"></a>为“日历日期”层次结构中的属性定义属性关系  
  
1.  在关系图中，右键单击“月份名称”属性，然后选择“新建属性关系”。  
  
2.  在“创建属性关系”对话框中，“源属性”是“月份名称”。 将“相关属性”设置为“日历季度”。 在“关系类型”列表中，将关系类型设置为“刚性”。  
  
3.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
4.  在关系图中，右键单击“日历季度”属性，然后选择“新建属性关系”。  
  
5.  在“创建属性关系”对话框中，“源属性”是“日历季度”。 将“相关属性”设置为“日历半期”。 在“关系类型”列表中，将关系类型设置为“刚性”。  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  在关系图中，右键单击“日历半期”属性，然后选择“新建属性关系”。  
  
8.  在“创建属性关系”对话框中，“源属性”是“日历半期”。 将“相关属性”设置为“日历年”。 在“关系类型”列表中，将关系类型设置为“刚性”。  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="defining-attribute-relationships-for-attributes-in-the-geography-hierarchy"></a>为“地域”层次结构中的属性定义属性关系  
  
1.  打开“地域”维度的维度设计器，然后单击“属性关系”选项卡。  
  
2.  在关系图中，右键单击“邮政编码”属性，然后选择“新建属性关系”。  
  
3.  在“创建属性关系”对话框中，“源属性”是“邮政编码”。 将“相关属性”设置为“市县”。 在“关系类型”列表中，将关系类型设置为“柔性”。  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  在关系图中，右键单击“市县”属性，然后选择“新建属性关系”。  
  
6.  在“创建属性关系”对话框中，“源属性”是“市县”。 将“相关属性”设置为“省/市/自治区”。 在“关系类型”列表中，将关系类型设置为“刚性”。  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  在关系图中，右键单击“省/市/自治区”属性，然后选择“新建属性关系”。  
  
9. 在“创建属性关系”对话框中，“源属性”是“省/市/自治区”。 将“相关属性”设置为“国家/地区-区域”。 在“关系类型”列表中，将关系类型设置为“刚性”。  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
11. 在关系图中，右键单击“地域关键字”特性，然后选择“属性”。  
  
12. 将**AttributeHierarchyOptimizedState** 属性设置为 **NotOptimized**，将 **AttributeHierarchyOrdered** 属性设置为 **False**，并将 **AttributeHierarchyVisible** 属性设置为 **False**。  
  
13. 在“文件”  菜单上，单击“全部保存” 。  
  
14. 在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 的“生成”菜单上，单击“部署 Analysis Services 教程”。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
[定义未知的成员和 Null 处理属性](../analysis-services/lesson-4-7-defining-the-unknown-member-and-null-processing-properties.md)  
  
## <a name="see-also"></a>另请参阅  
[定义属性关系](../analysis-services/multidimensional-models/attribute-relationships-define.md)  
[用户层次结构属性](../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md)  
  
  
  
