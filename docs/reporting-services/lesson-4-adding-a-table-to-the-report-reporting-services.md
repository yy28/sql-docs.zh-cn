---
title: 第 4 课：向报表添加表 (Reporting Services) | Microsoft Docs
ms.date: 04/29/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 5ddf2914-bcdd-427d-8cba-0ccb8342f819
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: e925dec5eb14365a6c313349599a77ffe1d7ab13
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65106010"
---
# <a name="lesson-4-adding-a-table-to-the-report-reporting-services"></a>第 4 课：向报表添加表 (Reporting Services)

定义数据集后，您可以开始定义报表。 通过将“工具箱”  窗格中的报表对象  拖放到“设计图面”  来创建报表布局。 一些报表对象的类型包括：

- 表
- 文本框
- 图像
- 行
- Rectangle
- 图表
- 映射

包含基础数据集中重复数据行的项称为“数据区域”  。 添加数据区域之后，可以向该数据区域添加字段。 基本报表将只有一个数据区域。 可以添加其他选项来显示更多信息，比如图表。

## <a name="add-a-table-data-region-and-fields-to-a-report-layout"></a>向报表布局添加表数据区域和字段

1. 选择报表设计器左窗格中的“工具箱”  选项卡。 使用鼠标选择“表”  对象，并将其拖至报表设计图面。 报表设计器将在设计图面中心绘制一个具有三列的数据区域。 如果没有看到“工具箱”  选项卡，选择“视图”  菜单 > “工具箱”  。

    ![ssrs_ssdt_addtable](media/ssrs-ssdt-addtable.png)

    你还可以从设计图面向报表添加表。 右键单击设计图面，然后选择“插入”   > “表”  。

2. 在“报表数据”  窗格中，展开 AdventureWorksDataset 以显示字段。

3. 将 `[Date]` 字段从“报表数据”  窗格拖到表的第一列。

    > [!IMPORTANT]
    > 将字段拖到第一列中时，会发生两件事。 首先，报表设计器将在方括号中显示字段名称，也称为“字段表达式”  ：数据单元中的 `[Date]`。 其次，它将列标签添加到标题行，就在字段表达式的上方。 默认情况下，该列标签是字段的名称。 如果要更改列标签，可以选择它并键入一个新值。

4. 将 `[Order]` 字段从“报表数据”  窗格拖到表的第二列。

5. 将 `[Product]` 字段从“报表数据”  窗格拖到表的第三列。

6. 将 `[Qty]` 字段拖到第三列的右边缘，直到显示一个垂直光标且鼠标指针显示加号 [+] 为止。 释放鼠标按钮后，将为 `[Qty]` 字段表达式创建第四列。

    ![ssrs_tutorial_addcolumn](media/ssrs-tutorial-addcolumn.png)

7. 请以相同方式添加 `[LineTotal]` 字段，并创建第五列。 列标签添加为“行总数”。 报表设计器通过将“LineTotal”拆分为两个单词，自动创建该列的友好名称。

以下关系图显示已由下列字段填充的表数据区域：Date、Order、Product、Qty 和 Line Total。
![rs_BasicTableDetailsDesign](media/rs-basictabledetailsdesign.png)

## <a name="preview-your-report"></a>预览报表

通过预览报表，您可以不必先将报表发布到报表服务器，即可查看呈现的报表。 在设计时频繁预览报表。 通过此操作，可以验证设计和数据连接，从而允许你随时纠正错误和问题。

### <a name="to-preview-a-report"></a>预览报表

- 选择“预览”  选项卡。报表设计器将运行此报表，并将其显示在“预览”  视图中。

    ![ssrs_ssdt_preview](media/ssrs-ssdt-preview.png)

下图显示了“预览”  视图中的部分报表。

   ![具有五列的表的详细信息行预览](media/rs-basictabledetailspreview.png "Preview, Detail rows of table with five columns")

查看 Date 和 Line Total 的值。 在下一课中，你将了解如何设置其格式以更整齐地显示。

> [!NOTE]
> 在“文件”  菜单上，选择“全部保存”  来保存报表。

## <a name="next-steps"></a>后续步骤

你已成功地向报表添加了表数据区域、向数据区域添加了字段，并成功地预览了报表。 在下一课中，将了解如何设置列标题和字段表达式的格式。 接下来，请继续学习[第 5 课：设置报表格式 (Reporting Services)](lesson-5-formatting-a-report-reporting-services.md)。
  
## <a name="see-also"></a>另请参阅

[表（报表生成器和 SSRS）](report-design/tables-report-builder-and-ssrs.md)  
[数据集字段集合（报表生成器和 SSRS）](report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
