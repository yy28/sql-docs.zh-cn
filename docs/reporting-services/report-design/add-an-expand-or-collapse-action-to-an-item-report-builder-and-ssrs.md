---
title: 为项添加展开或折叠操作（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-design
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 49f07ad6-242b-4861-8fc1-91ca78c36d6c
caps.latest.revision: 12
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 727521df55b09dc4d28a1b79054c4ad8c411cb01
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "33020874"
---
# <a name="add-an-expand-or-collapse-action-to-an-item-report-builder-and-ssrs"></a>为项添加展开或折叠操作（报表生成器和 SSRS）
  你可以使用户实现以交互方式展开或折叠报表项，或者展开或折叠与表或矩阵的组关联的行与列。 若要让用户能够展开或折叠某个项，请设置该项的可见性属性。 设置可见性在 HTML 报表查看器中有效，有时也称为“深化”  操作。  
  
 在报表设计视图中，可以指定要显示展开和折叠切换图标的文本框的名称。 在呈现的报表中，文本框中除了内容之外，还显示加号 (+) 或减号 (-)。 用户单击切换时，报表显示内容将相应刷新，以根据报表中各项的当前可见性设置显示或隐藏报表项。  
  
 通常，展开和折叠操作的使用方式是最初仅显示摘要数据，让用户能够单击加号以显示详细信息数据。 例如，您可以一开始就隐藏显示图表的值的表，或隐藏包含嵌套行组或列组的表的子组，这与在明细报表中相同。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-expand-and-collapse-action-to-a-group"></a>为组添加展开和折叠操作  
  
1.  在报表设计视图中，单击表或矩阵将其选中。 “分组”窗格随即显示行组和列组。  
  
     ![“分组”窗格](../../reporting-services/report-design/media/groupingpane.png "Grouping Pane")  
  
     如果未出现“分组”窗格，请单击 **“查看”** 菜单，然后单击 **“分组”**。  
  
2.  右键单击“分组”窗格标题栏中的任意位置，然后单击“高级”。 此时将切换“分组”窗格模式以便在设计图面上显示行和列的基础显示结构。  
  
     ![具有“高级模式”菜单的“分组”窗格](../../reporting-services/report-design/media/groupingpane-advancedmode.png "Grouping Pane with Advanced Mode menu")  
  
3.  在相应的组窗格中，单击要隐藏其关联行或列的行组或列组的名称。 该组即被选中，并且“属性”窗格会显示 **“Tablix 成员”** 属性。  
  
    > [!NOTE]  
    >  如果未看见“属性”窗格，请单击功能区上的“查看”，然后单击“属性”。  
  
4.  在 **“隐藏”** 中，选择以下选项之一来设置首次运行报表时该报表项的可见性：  
  
    -   选择 **False** 可以显示报表项。  
  
    -   选择 **True** 可以隐藏报表项。  
  
    -   选择“\<表达式>”打开“表达式”对话框，以创建在运行时要计算的表达式来确定可见性。  
  
5.  在“切换项”下拉框中，选择要向其添加切换图像的文本框名称。  
  
     在下图中，“颜色”行组配置为可使用户展开和折叠关联行。  
  
     ![配置要展开的行组](../../reporting-services/report-design/media/expandcollapse-confighiddentoggleitemwithnumbers.png "Configuring a row group to be expanded")  
  
    > [!NOTE]  
    >  包含切换图像的文本框不能是您要隐藏其关联行或列的行组或列组。 该文本框必须在要隐藏的项所在的同一组或祖先组中。 例如，若要切换与子组关联的行的可见性，请在与父组关联的行中选择一个文本框。  
  
6.  若要测试该切换，请运行报表，然后单击带有切换图像的文本框。 报表显示内容随即刷新，显示带有切换后的可见性的行组和列组。  
  
     ![运行具有可展开行组的报表](../../reporting-services/report-design/media/expandcollapse-runreport-rowgroup.png "Running report with expandable row group")  
  
### <a name="to-add-expand-and-collapse-action-to-a-report-item"></a>为报表项添加展开和折叠操作  
  
1.  在报表设计视图中，右键单击要显示或隐藏的报表项，然后单击“\<报表项> 属性”。 将打开该报表项的“\<报表项> 属性”对话框。  
  
2.  单击 **“可见性”**。  
  
3.  在 **“在报表最初运行时”** 中，选择以下选项之一来设置首次运行报表时该报表项的可见性：  
  
    -   选择 **“显示”** 可以显示报表项。  
  
    -   选择 **“隐藏”** 可以隐藏报表项。  
  
    -   选择 **“基于表达式显示或隐藏”** 可以使用在运行时计算的表达式来确定可见性。 单击 (fx) 打开“表达式”对话框以创建表达式。  
  
        > [!NOTE]  
        >  当指定可见性的表达式时，需要设置报表项的 Hidden 属性。 表达式计算结果为 **Boolean** 值，值为 **True** 时表示隐藏该项，值为 **False** 时表示显示该项。  
  
4.  在“可以通过此报表项切换显示”下拉框中，键入或选择要在其中显示切换图像的报表文本框的名称，例如 Textbox1。  
  
     在下图中，表配置为使用户可以展开或折叠此表。 表的显示通过“产品表”文本框进行切换。  
  
     ![配置要展开的报表表格](../../reporting-services/report-design/media/expandcollapse-reporttable.png "Configure a report table to be expanded")  
  
    > [!NOTE]  
    >  您选择的文本框必须位于此报表项的当前作用域或包含作用域中（上至表体）。 例如，若要切换图表的可见性，请选择一个与该图表位于同一包含作用域中的文本框；例如，表体或矩形。 文本框必须在同一容器层次结构或更高层次结构中。  
  
5.  若要测试该切换，请运行报表，然后单击带有切换图像的文本框。 报表显示内容随即刷新，显示带有切换后的可见性的报表项。  
  
     ![运行具有展开表格的报表](../../reporting-services/report-design/media/expandcollapse-runreport-reporttable.png "运行具有展开表格的报表")  
  
## <a name="see-also"></a>另请参阅  
 [深化操作（报表生成器和 SSRS）](../../reporting-services/report-design/drilldown-action-report-builder-and-ssrs.md)   
 [隐藏项（报表生成器和 SSRS）](../../reporting-services/report-builder/hide-an-item-report-builder-and-ssrs.md)  
  
  
