---
title: 第 5 课：设置报表格式 (Reporting Services) | Microsoft Docs
ms.date: 04/29/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: ae46efa9-6e04-48ec-afb4-5a2314dcb05a
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: a8bf8b6814f7989a904507cd89fbea397b8b6930
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "65105930"
---
# <a name="lesson-5-formatting-a-report-reporting-services"></a>第 5 课：设置报表格式 (Reporting Services)

既然您已经向 Sales Orders 报表添加了一个数据区域和一些字段，那么您就可以设置日期和货币字段以及列标题的格式。

## <a name="format-the-date"></a><a name="bkmk_format_date"></a>设置日期格式

默认情况下，Date 字段表达式显示日期和时间信息。 您可以设置其格式，使其只显示日期。

1. 选择“设计”  选项卡。
2. 右键单击带有 `[Date]` 字段表达式的单元格，然后单击“文本框属性”  。
3. 选择“数字”  ，然后在“类别”  字段中，选择“日期”  。
4. 在 **“类型”** 框中，选择 **“2000 年 1 月 31 日”** 。
5. 选择“确定”  以应用格式。
6. 预览报表以查看对 `[Date]` 字段格式的更改，然后更改回设计视图。

## <a name="format-the-currency"></a><a name="bkmk_format_currency"></a>设置货币格式

LineTotal 字段表达式显示常规数字。 可以设置其格式，以使其显示货币形式的数字。

1. 右键单击带有 `[LineTotal]` 表达式的单元格，然后选择“文本框属性”  。
2. 选择最左侧列列表框中的“数字”  ，并选择“类别”  列表框中的“货币”  。
3. 如果区域设置为“英语(美国)”，则“类型”  列表框中的默认设置应为：
    - **小数位数：2**
    - **负数：($12345.00)**
    - **符号：$ 英语(美国)**
4. 选择“使用千位分隔符(,)”。  如果示例文本显示“$12,345.00”  ，则说明设置是正确的。
5. 选择“确定”  以应用格式。
6. 预览报表以查看对 `[LineTotal]` 表达式列的更改，然后更改回设计视图。  

## <a name="change-text-style-and-column-widths"></a><a name="bkmk_change_textstyle"></a>更改文本样式和列宽

可以通过突出显示标题行并调整数据列的宽度向报表添加其他格式。

### <a name="to-format-header-rows-and-table-columns"></a>设置标题行和表列的格式

1. 选择表，以便在此表的上方和旁边显示列控点和行控点。 沿此表的上方和一侧显示的灰色条状物就是列控点和行控点。

2. 指向列控点之间的行，使光标变为双箭头。 拖动列，调整到所需大小。
    ![rs_BasicTableDetailsDesign](media/rs-basictabledetailsdesign.png)

3. 选择包含列标题标签的行，从“格式”  菜单中选择“字体”   > “加粗”  。

4. 预览报表。 应如下所示：

    ![带有以粗体显示的列标题的表预览](media/rs-basictabledetailsformattedpreview.png "带有以粗体显示的列标题的表预览")  

5. 在“文件”  菜单上，选择“全部保存”  来保存报表。

## <a name="next-steps"></a>后续步骤

在本课程中，你已成功设置列标题和字段表达式格式。 接下来，向报表添加分组和总计。 继续学习[第 6 课：添加分组和总计 (Reporting Services)](lesson-6-adding-grouping-and-totals-reporting-services.md)。

## <a name="see-also"></a>另请参阅

[设置数字和日期格式（报表生成器和 SSRS）](report-design/formatting-numbers-and-dates-report-builder-and-ssrs.md)
[呈现行为（报表生成器和 SSRS）](report-design/rendering-behaviors-report-builder-and-ssrs.md)
