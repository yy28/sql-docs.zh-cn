---
title: 自定义报表中的参数窗格（报表生成器）| Microsoft Docs
description: 了解使用报表生成器中的参数创建分页报表时如何自定义“参数”窗格。
ms.date: 06/15/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 4ce9e8d5-911a-4422-928f-a8d005b79fc6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 29bd397d64280644394077a29a3420dbf43b5e6f
ms.sourcegitcommit: 7d6eb09588ff3477cf39a8fd507d537a603bc60d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/16/2020
ms.locfileid: "84796558"
---
# <a name="customize-the-parameters-pane-in-a-report-report-builder"></a>Customize the Parameters Pane in a Report (Report Builder)
  使用报表生成器中的参数创建分页报表时，可以自定义参数窗格。 在报表设计视图中，可以将参数拖到参数窗格中的特定列和行。 你可以通过添加和删除列来更改窗格的布局。

 将参数拖到窗格中的新列和新行时，“报表数据”窗格中的参数顺序也会发生变化。 更改“报表数据”窗格中参数顺序时，窗格中参数的位置会发生变化。 有关参数顺序的重要性的详细信息，请参阅[更改报表参数的顺序（报表生成器和 SSRS）](../../reporting-services/report-design/change-the-order-of-a-report-parameter-report-builder-and-ssrs.md)。

## <a name="to-customize-the-parameters-pane"></a>自定义参数窗格的步骤

1.  在“视图”  选项卡上，选中“参数”  复选框以显示参数窗格。

     ![从“视图”选项卡访问“参数”窗格](../../reporting-services/report-design/media/ssrs-customparameter-accessparameterpanedesignmode.png "从“视图”选项卡访问“参数”窗格")

     窗格将显示在设计图面的顶部。

2.  若要向窗格添加参数，请执行以下操作之一。

    -   右键单击参数窗格中的空白单元格，然后单击“添加参数” 。

         ![从“参数”窗格添加新参数](../../reporting-services/report-design/media/ssrs-customizeparameter-addnewparameter.png "从“参数”窗格添加新参数")

    -   在“报表数据”窗格中，右键单击“参数”，然后单击“添加参数” 。

3.  若要将参数移动到参数窗格中的新位置，请将参数拖到窗格中的不同单元格。

     更改窗格中参数的位置时，“报表数据”窗格的“参数”列表中的参数顺序将自动发生变化********。 有关参数顺序的影响的详细信息，请参阅[更改报表参数的顺序（报表生成器和 SSRS）](../../reporting-services/report-design/change-the-order-of-a-report-parameter-report-builder-and-ssrs.md)

4.  若要访问参数的属性，请执行以下操作之一。

    -   右键单击参数窗格中的参数，然后单击“参数属性” 。

         ![从“参数”窗格访问参数属性](../../reporting-services/report-design/media/ssrs-customizeparameter-accessparameterproperties-composite.png "从“参数”窗格访问参数属性")

    -   右键单击“报表数据”窗格中的参数，然后单击“参数属性” 。

5.  若要向窗格添加新的列和行，或删除现有的行和列，请右键单击参数窗格中的任意位置，然后单击所示菜单中的命令。

     ![将列和行添加到“参数”窗格](../../reporting-services/report-design/media/ssrs-customparameter-addcolumnsrows.png "将列和行添加到“参数”窗格")

    > [!IMPORTANT]
    >  删除包含参数的列或行时，将从报表中删除这些参数。

6.  若要从窗格和报表中删除参数，请执行以下操作之一。

    -   右键单击参数窗格中的参数，然后单击“删除”  。

         ![从“参数”窗格删除参数](../../reporting-services/report-design/media/ssrs-customparameter-deleteparameter.png "从“参数”窗格删除参数")

    -   右键单击“报表数据”窗格中的参数，然后单击“删除” 。

## <a name="hiddeninternal-parameters-during-runtime"></a>运行时的隐藏/内部参数
如果有隐藏/内部参数，则在运行时是否将其呈现为空白区域的逻辑如下所示：

   - 如果任何行或列仅包含隐藏/内部参数或空单元格，则在运行时不会呈现整行或整列
   - 否则，隐藏/内部参数或空单元格将呈现为空白区域

例如，`ReportParameter1` 隐藏，而其余的参数可见：

![隐藏参数示例 1](../../reporting-services/report-design/media/ssrs-hidden-parameter-rb-1.png "布局网格中的一个隐藏参数")

这将在运行时导致空白区域，因为在第一列或第一行中有可见参数：

![隐藏参数示例 1 - 运行时](../../reporting-services/report-design/media/ssrs-hidden-parameter-server-1.png "布局网格中的一个隐藏参数导致运行时出现空白区域")

同一个示例中，如果同时将 `ReportParameter3` 设置为隐藏：

![隐藏参数示例 2](../../reporting-services/report-design/media/ssrs-hidden-parameter-rb-2.png "同一列中的两个隐藏参数")

那么在运行时不会呈现第一列，因为整个列都被视为空的：

![隐藏参数示例 2 - 运行时](../../reporting-services/report-design/media/ssrs-hidden-parameter-server-2.png "运行时期间同一列中的两个隐藏参数")

## <a name="default-layout"></a>默认布局
对于在 SQL Server Reporting Services 2016 之前创作的报表，将在运行时使用 2 列和 N 行的默认参数布局网格。 若要更改默认布局，请在 Microsoft 报表生成器中打开报表并保存报表。 保存报表后，自定义的参数布局信息将保存为 .rdl 文件。


## <a name="see-also"></a>另请参阅
 [报表参数（报表生成器和报表设计器）](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)


