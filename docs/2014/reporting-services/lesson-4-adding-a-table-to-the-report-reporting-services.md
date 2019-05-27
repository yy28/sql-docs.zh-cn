---
title: 第 4 课：向报表添加表 (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 5ddf2914-bcdd-427d-8cba-0ccb8342f819
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3bb152b749041451cdb3a3294c24d8b172c49a99
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66108453"
---
# <a name="lesson-4-adding-a-table-to-the-report-reporting-services"></a>第 4 课：向报表添加表 (Reporting Services)
  定义数据集后，您可以开始定义报表。 将要纳入报表的数据区域、文本框、图像和其他项拖放到设计图面上来创建报表布局。  
  
 包含基础数据集中重复数据行的项称为“数据区域”。 基本报表将只有一个数据区域，但是对于要将图表添加到表格报表等情况，则可以添加多个数据区域。 添加数据区域之后，可以向该数据区域添加字段。  
  
### <a name="to-add-a-table-data-region-and-fields-to-a-report-layout"></a>向报表布局中添加表数据区域和字段  
  
1.  在“工具箱”中，单击“表”，然后单击设计图面并拖动鼠标”。 报表设计器将在设计图面中心绘制一个具有三列的数据区域。  
  
    > [!NOTE]  
    >  “工具箱”可能显示为“报表数据”窗格左侧的一个选项卡。 若要打开“工具箱”，请将指针移到“工具箱”选项卡上。如果“工具箱”不可见，请单击“视图”菜单中的“工具箱”。  
  
2.  在中**报表数据**窗格中，展开**AdventureWorksDataset**数据集以显示字段。  
  
3.  将从该日期字段拖**报表数据**到表中的第一列的窗格。  
  
     将字段拖到第一列中时，会发生两件事。 首先，数据单元将在方括号中显示字段名称，也称为“字段表达式”：`[Date]`。 其次，列标题值自动添加到紧邻字段表达式上面的标题行。 默认情况下，该列是字段的名称。 您可以选中标题行文本，然后键入一个新名称。  
  
4.  将 Order 字段从**报表数据**到表中的第二个列的窗格。  
  
5.  将 Product 字段从**报表数据**到表中的第三个列的窗格。  
  
6.  将 Qty 字段拖到第三列的右边缘，直到显示一个垂直光标且鼠标指针带有加号 [+] 为止。 释放鼠标按钮后，将为 `[Qty]`创建第四列。  
  
7.  请以相同方式添加 LineTotal 字段，并创建第五列。  
  
    > [!NOTE]  
    >  列标题是 Line Total。 报表设计器通过将 LineTotal 拆分为两个单词，自动创建该列的友好名称。  
  
     下图展示了已填充有下面这些字段的表数据区域：“Date”、“Order”、“Product”、“Qty”和“Line Total”。  
  
     ![设计，具有标题行和详细信息行的表](../../2014/tutorials/media/rs-basictabledetailsdesign.gif "Design，Table with 标头行和详细信息行")  
  
## <a name="preview-your-report"></a>预览报表  
 通过预览报表，您可以不必先将报表发布到报表服务器，即可查看呈现的报表。 您可能希望在设计时频繁预览报表。 预览报表还将对设计和数据连接进行验证，以便您可以在将报表发布到报表服务器之前更正错误和问题。  
  
#### <a name="to-preview-a-report"></a>预览报表  
  
-   单击 **预览** 选项卡。报表设计器将运行此报表，并将其显示在“预览”视图中。  
  
     下图显示了“预览”视图中的部分报表。  
  
     ![具有 5 列的表的详细信息行预览](../../2014/tutorials/media/rs-basictabledetailspreview.gif "Preview, Detail rows of table with 5 columns")  
  
     请注意，Line Total 列中货币的小数点后面有六个小数位，并且日期包含时间戳。 此格式问题将在下一课中进行修复。  
  
> [!NOTE]  
>  在 **“文件”** 菜单上单击 **“全部保存”** 可保存报表。  
  
## <a name="next-steps"></a>后续步骤  
 您已成功地向报表添加了表数据区域、向数据区域添加了字段，并成功地预览了报表。 接下来，将设置列标题以及日期和货币值的格式。 请参阅[第 5 课：设置报表格式 &#40;Reporting Services&#41;](../reporting-services/lesson-5-formatting-a-report-reporting-services.md)。  
  
## <a name="see-also"></a>请参阅  
 [表（报表生成器和 SSRS）](report-design/tables-report-builder-and-ssrs.md)   
 [数据集字段集合（报表生成器和 SSRS）](report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
  
  
