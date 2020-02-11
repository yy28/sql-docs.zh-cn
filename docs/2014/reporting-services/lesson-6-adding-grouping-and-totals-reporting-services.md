---
title: 第 6 课：添加分组和总计 (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: e3d61228-2aa4-42cc-955e-602dbf3406a7
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5607dfb046e7f50eb3a015e1f4f13711256435a8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66108404"
---
# <a name="lesson-6-adding-grouping-and-totals-reporting-services"></a>Lesson 6: Adding Grouping and Totals (Reporting Services)
  向报表中添加分组和总计以便组织和汇总数据。  
  
 有关向报表添加运行总计的信息，请参阅：向[Reporting Services （SSRS）报表添加总计](https://www.tutorialgateway.org/add-total-and-subtotal-to-ssrs-report/)。  
  
 **本主题内容：**  
  
-   [对报表中的数据进行分组](#bkmk_groupdata)  
  
-   [向报表添加总计](#bkmk_addtotals)  
  
-   [向报表添加每日总计](#bkmk_adddailytotal)  
  
-   [向报表添加总计](#bkmk_addgrandtotal)  
  
-   [将报表发布到报表服务器（可选）](#bkmk_publishreport)  
  
##  <a name="bkmk_groupdata"></a>对报表中的数据进行分组  
  
1.  单击 **“设计”** 选项卡。  
  
2.  如果看不到 "**行组**" 窗格，请右键单击设计图面，然后单击 "**查看**"，然后单击 "**分组**"。  
  
3.  从“报表数据”**** 窗格将 `Date` 字段拖到“行组”**** 窗格。 并将其放置到名为 **(Details)** 的行上面。  
  
     请注意，行控点中现在有一个方括号，用于显示组。 表现在在垂直点线的两侧各有一个 Date 列。  
  
     ![](../../2014/tutorials/media/rs-basictablegroups1design.gif "rs_BasicTableGroups1Design")  
  
4.  从“报表数据”**** 窗格将 `Order` 字段拖到“行组”**** 窗格。 并将其放置到 Date 下面和 **(Details)** 上面。  
  
     请注意，行控点中现在有两个方括号，用于显示两个组。 该表现在也有两`Order`列。  
  
5.  删除两根线条 右侧 的原始 Date 和 **Order** 列。 这将删除该单个记录值，以便仅显示组值。 选择并右键单击两个列的列句柄，然后单击“删除列”****。  
  
     ![选择要删除的列](../../2014/tutorials/media/rs-basictablegroupsdeletecols.gif "选择要删除的列")  
  
     您可以重新设置列标题和日期的格式。  
  
6.  切换到 **“预览”** 选项卡以预览报表。 其外观应与下图类似：  
  
     ![先按日期后按订单分组的表](../../2014/tutorials/media/rs-basictablegroupspreview.gif "先按日期后按订单分组的表")  
  
##  <a name="bkmk_addtotals"></a>向报表添加总计  
  
1.  切换到“设计”视图。  
  
2.  右键单击包含 `[LineTotal]` 字段的数据区域单元，并单击“添加总计”****。  
  
     这将添加一个带有每个订单的美元总金额的行。  
  
3.  右键单击包含 `[Qty]` 字段的单元，并单击“添加总计”****。  
  
     这将向总计行添加每个订单的总数量。  
  
4.  在 `Sum[Qty]`左侧的空单元中，键入标签“**Order Total**”。  
  
5.  可以向总计行添加背景色。 选择两个累加求和单元和标签单元。  
  
6.  在 **“格式”** 菜单上，依次单击 **“背景色”**、 **“浅灰色”** 和 **“确定”**。  
  
     ![设计视图：带有订单总计的基本表](../../2014/tutorials/media/rs-basictablesumlinetotaldesign.gif "设计视图：带有订单总计的基本表")  
  
##  <a name="bkmk_adddailytotal"></a>向报表添加每日总计  
  
1.  右键单击 Order 单元，指向“添加总计”****，并单击“晚于”****。  
  
     这会添加一个新行，其中包含每天的数量和美元量的总和，以及 Order 列中的标签 "**Total**"。  
  
2.  在同一单元格中的单词**Total**之前键入单词，使**其每****日汇总**一次。  
  
3.  选定 **Daily Total** 单元、两个 **Sum** 单元及其之间的空单元。  
  
4.  在 **“格式”** 菜单上，依次单击 **“背景色”**、 **“橙色”** 和 **“确定”**。  
  
     ![](../../2014/tutorials/media/rs-basictablesumdaytotaldesign.gif "rs_BasicTableSumDayTotalDesign")  
  
##  <a name="bkmk_addgrandtotal"></a>向报表添加总计  
  
1.  右键单击“Date”单元，指向“添加总计”****，并单击“晚于”****。  
  
     这将添加一个新行，其中包含整个报表的数量和美元金额的总和，以及**** `Date`列中的总标签。  
  
2.  在相同单元中，在 **Total** 单词之前键入 **Grand** 单词，使其显示为 **Grand Total**。  
  
3.  选定 **Grand Total** 单元、两个 **Sum** 单元及其之间的空单元。  
  
4.  在 **“格式”** 菜单上，依次单击 **“背景色”**、 **“浅蓝色”** 和 **“确定”**。  
  
     ![设计视图：基本表中的总计](../../2014/tutorials/media/rs-basictablesumgrandtotaldesign.gif "设计视图：基本表中的总计")  
  
5.  单击“预览”。  
  
     最后一页的外观应与下图相似：  
  
     ![预览：带有总计的基本表](../../2014/tutorials/media/rs-basictablesumgrandtotalpreview.gif "预览：带有总计的基本表")  
  
##  <a name="bkmk_publishreport"></a>将报表发布到报表服务器（可选）  
  
1.  一个可选步骤是将已完成的报表发送到本机模式报表服务器上，以便您可以从报表管理器查看该报表。  
  
2.  在工具栏上，单击 **“项目”** ，然后单击 **“教程属性...”**。  
  
3.  在**TargetServerURL**中，键入 Report Server 名称的名称，例如**http://\<servername>/reportserver**  
  
4.  单击 **"确定"**  
  
5.  在工具栏上，单击 **“生成”** ，然后单击 **“部署教程”**。  
  
     如果您在输出窗口中看到如下消息，则指示成功部署。  
  
    > ------ Build started: Project: tutorial, Configuration: Debug ------Skipping 'Sales Orders.rdl'. 项是最新的。生成完成--0 个错误，------部署开始时出现0个警告：项目：教程，配置： Debug\<------部署到 http://server 名称>/reportserverdeploying 报表 "/tutorial/Sales 订单"。部署完成-0 个错误，0个警告 = = = = = = = = = = 生成：成功或最新，0失败，0已跳过 = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = =  
  
     如果您看到如下错误消息，则确认您对报表服务器的权限并且已使用管理员权限启动了 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 。  
  
    > "为用户 ' XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX\\<\>的权限不足，无法执行此操作"  
  
6.  以管理员权限启动报表管理器，例如，右键单击 Internet Explorer 图标，然后单击 "以**管理员身份运行**"。  
  
     浏览至报表管理器 URL，例如： `http://<server name>/reports`。  
  
7.  浏览到包含该报表的文件夹，并单击报表 `Sales Orders` 的名称以在浏览器中查看呈现的报表。  
  
## <a name="next-steps"></a>后续步骤  
 这样，您就成功完成了对“创建基本表报表”教程的学习。  
  
## <a name="see-also"></a>另请参阅  
 [对数据进行筛选、分组和排序（报表生成器和 SSRS）](report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)  
  
  
