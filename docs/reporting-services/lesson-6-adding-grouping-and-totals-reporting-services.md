---
title: 第 6 课：添加分组和总计 (Reporting Services) | Microsoft Docs
description: 了解如何向 Reporting Services 报表中添加分组和总计以便组织和汇总数据。
ms.date: 04/18/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: e3d61228-2aa4-42cc-955e-602dbf3406a7
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5d149bb85834ae9c775e414e405889631a81f288
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/28/2020
ms.locfileid: "87243259"
---
# <a name="lesson-6-adding-grouping-and-totals-reporting-services"></a>第 6 课：添加分组和总计 (Reporting Services)

在最后的教程课程中，你将向 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 报表中添加分组和总计以便组织和汇总数据。  

## <a name="to-group-data-in-a-report"></a>在报表中对数据进行分组

1. 选择“设计”选项卡。
2. 如果看不到“行组”窗格，请右键单击设计图面，然后选择“查看” >“分组”。
3. 从“报表数据”窗格将 `[Date]` 字段拖到“行组”窗格。 将其置于显示为 = (Details) 的行之上。

    > [!NOTE]
    > 请注意，行控点中现在有一个方括号，用来表示组。 表现在在垂直点线的两侧各有一个 `[Date]` 表达式列。
    >
    >![添加的日期组](media/rs-basictablegroups1design.png "添加的日期组")
4. 从“报表数据”窗格将 `[Order]` 字段拖到“行组”窗格。 并将其放置到 Date 下面和 = (Details) 上面。

    ![ssrs_ssdt_addorderfield](media/ssrs-ssdt-addorderfield.png)

    > [!NOTE]
    > 请注意，行句柄中现在有两个方括号 ![ssrs_ssdt_rowgroupdoublehandles](media/ssrs-ssdt-rowgroupdoublehandles.png)，用于表示两个组。 现在此表还包含两个 `[Order]` 表达式列。

5. 删除两根线条右侧的原始 `[Date]` 和 `[Order]` 表达式列。 选择并右键单击两个列的列句柄，然后选择“删除列”。 报表设计器将删除各个行表达式，以便只显示组表达式。

    ![选择要删除的列](media/rs-basictablegroupsdeletecols.gif "选择要删除的列")

6. 若要设置新 `[Date]` 列的格式，右键单击包含 `[Date]` 表达式的数据区域单元，然后选择“文本框属性”。
7. 选择最左侧列列表框中的“数量”，并选择“类别”列表框中的“日期”。
8. 在“类型”列表框中，选择“2000 年 1 月 31 日”。
9. 选择“确定”以应用格式。
10. 再次预览报表。 其外观应如下所示：

    ![rs_BasicTableGroupsPreview](media/rs-basictablegroupspreview.png)

## <a name="adding-totals-to-a-report"></a>向报表添加总计

1. 切换到“设计”视图。
2. 右键单击包含 `[LineTotal]` 表达式的数据区域单元，并选择“添加总计”。 报表设计器将添加一个带有每个订单的美元总金额的行。
3. 右键单击包含 `[Qty]` 字段的单元，并选择“添加总计”。 报表设计器将向总计行添加每个订单的总数量。
4. 在 `Sum[Qty]` 单元左侧的空单元中，键入字符串“Order Total”。
5. 可以向总计行添加背景色。 选择两个累加求和单元和标签单元。  
6. 从“格式”菜单中，选择“背景色” > “浅灰色”正方形。
7. 选择“确定”以应用格式。

   ![设计视图：含订单总计的基本表](media/rs-basictablesumlinetotaldesign.gif "设计视图：含订单总计的基本表")

## <a name="add-the-daily-total-to-the-report"></a>向报表添加每日总计

1. 右键单击 `[Order]` 表达式单元，然后选择“添加总计” > “之后”。 报表设计器添加了一个新行，其中包含 `[Qty]` 和 `[Linetotal]` 值的每日总计，并在 `[Order]` 表达式列的底部添加了字符串“Total”。
2. 在相同单元中，在“Total”词前键入“Daily”一词，使其显示为“Daily Total”。
3. 选择该单元和右侧相邻的两个单元及其之间的空单元。
4. 从“格式”菜单重，选择“背景色” > “橙色”正方形。
5. 选择“确定”以应用格式。

   ![将背景色设置为橙色](media/rs-basictablesumdaytotaldesign.gif "rs_BasicTableSumDayTotalDesign")

## <a name="add-the-grand-total-to-the-report"></a>向报表添加总计

1. 右键单击 `[Date]` 表达式单元，然后选择“添加总计” > “之后”。 报表设计器添加了一个新行，其中包含整个报表 `[Qty]` 和 `[LineTotal]` 值的总计，并在 `[Date]` 表达式列的底部添加了字符串“Total”。
2. 在相同单元中，在“Total”词前键入“Grand”一词，使其显示为“Grand Total”。
3. 选定“Grand Total”单元、两个 `Sum()` 表达式单元及其之间的空单元。
4. 从“格式”菜单中，选择“背景色” > “蓝色”正方形。
5. 选择“确定”以应用格式。

    ![设计视图：基本表中的总计](media/rs-basictablesumgrandtotaldesign.gif "设计视图：基本表中的总计")

## <a name="preview-the-report"></a>预览报表

若要预览格式更改，请选择“预览”选项卡。在“预览”工具栏中，选择“最后一页”按钮，如 ![ssrs_ssdt_viewertoolbar_lastpage](media/ssrs-ssdt-viewertoolbar-lastpage.png) 中所示。 结果应如下所示：

   ![预览：含总计的基本表](media/rs-basictablesumgrandtotalpreview.gif "预览版：含总计的基本表")

## <a name="publishing-the-report-to-the-report-server-optional"></a>将报表发布到报表服务器（可选）

一个可选步骤是将已完成的报表发送到报表服务器上，以便可以在 Web 门户中查看该报表。

1. 选择“项目”菜单 > “教程属性...”
2. 在“TargetServerURL”中，键入报表服务器的名称，例如：
    - `http:/<servername>/reportserver` 或
    - 如果在报表服务器上设计报表，则 `https://localhost/reportserver` 有效。

3. 请注意，“TargetReportFolder”是根据项目名称命名的教程。 报表设计器将报表部署到此文件夹。
4. 选择“确定”。
5. 选择“构建”菜单 > “部署教程”。

    如果在“输出”窗口中看到如下消息，则指示成功部署。

    > ------ 生成已开始：项目：教程，配置：调试 ------  
    > Skipping 'Sales Orders.rdl'. 项是最新版本。  
    > 生成完成 -- 0 个错误，0 个警告  
    > ------ 部署已开始：项目：教程，配置：调试 ------  
    > 正在部署到 `https://[server name]/reportserver`  
    > 部署 report '/tutorial/Sales Orders'。  
    > 部署完成 - 0 个错误，0 个警告  
    > ========== 生成：1 个成功或最新，0 个失败，0 个跳过 ==========  
    > ========== 部署：1 个成功，0 个失败，0 个跳过 ==========  

    如果看到如下错误消息，则确认你对报表服务器有适当的权限并且已使用管理员权限启动了 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]。
    >
    > “为用户‘XXXXXXXX\\[你的用户名]’授予的权限不足，无法执行此操作”

6. 打开具有管理员权限的浏览器。 例如，右键单击 Internet Explorer 图标，然后选择“以管理员身份运行”。
7. 浏览到 Web 门户 URL。
   - `https://<server name>/reports`.
   - 如果在报表服务器上设计报表，则 `https://localhost/reports` 有效。

8. 选择“教程”文件夹，并选择“销售订单”报表来查看报表。

    ![ssrs_tutorial_tutorialfolder](media/ssrs-tutorial-tutorialfolder.png)  

你已成功完成了“创建基本表报表教程”的学习。

## <a name="see-also"></a>另请参阅

[对数据进行筛选、分组和排序（报表生成器和 SSRS）](report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)
