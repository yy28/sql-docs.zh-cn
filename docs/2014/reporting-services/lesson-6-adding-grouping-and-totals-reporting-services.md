---
title: 第 6 课：添加分组和总计 (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: e3d61228-2aa4-42cc-955e-602dbf3406a7
caps.latest.revision: 50
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: c411b3780f1e3f5b91d00d08093f281a5daa286f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37218873"
---
# <a name="lesson-6-adding-grouping-and-totals-reporting-services"></a>Lesson 6: Adding Grouping and Totals (Reporting Services)
  向报表中添加分组和总计以便组织和汇总数据。  
  
 有关向报表添加运行总计的信息，请参阅此特选上的综合处理：[向 Reporting Services (SSRS) 报表添加总计](http://go.microsoft.com/fwlink/p/?LinkId=403698)。  
  
 **本主题内容：**  
  
-   [对在报表中数据进行分组](#bkmk_groupdata)  
  
-   [若要向报表添加总计](#bkmk_addtotals)  
  
-   [若要向报表添加每日总计](#bkmk_adddailytotal)  
  
-   [若要向报表添加总计](#bkmk_addgrandtotal)  
  
-   [若要将报表发布到报表服务器 （可选）](#bkmk_publishreport)  
  
##  <a name="bkmk_groupdata"></a> 对在报表中数据进行分组  
  
1.  单击 **“设计”** 选项卡。  
  
2.  如果没有看到**行组**窗格中，右键单击设计图面，然后单击**视图**，然后单击**分组**。  
  
3.  从**报表数据**窗格中，拖动`Date`字段**行组**窗格。 并将其放置到名为 **(Details)** 的行上面。  
  
     请注意，行控点中现在有一个方括号，用于显示组。 表现在在垂直点线的两侧各有一个 Date 列。  
  
     ![](../../2014/tutorials/media/rs-basictablegroups1design.gif "rs_BasicTableGroups1Design")  
  
4.  从**报表数据**窗格中，拖动`Order`字段**行组**窗格。 并将其放置到 Date 下面和 **(Details)** 上面。  
  
     请注意，行控点中现在有两个方括号，用于显示两个组。 现在，此表包含两个`Order`列过。  
  
5.  删除到原始日期和订单的列**右**两根线条。 这将删除该单个记录值，以便仅显示组值。 选择并右键单击两个列的列句柄，然后单击“删除列”。  
  
     ![选择要删除的列](../../2014/tutorials/media/rs-basictablegroupsdeletecols.gif "选择要删除的列")  
  
     您可以重新设置列标题和日期的格式。  
  
6.  切换到 **“预览”** 选项卡以预览报表。 其外观应与下图类似：  
  
     ![先按日期后按订单分组的表](../../2014/tutorials/media/rs-basictablegroupspreview.gif "Table grouped by date and then order")  
  
##  <a name="bkmk_addtotals"></a> 若要向报表添加总计  
  
1.  切换到“设计”视图。  
  
2.  右键单击包含 `[LineTotal]` 字段的数据区域单元，并单击“添加总计”。  
  
     这将添加一个带有每个订单的美元总金额的行。  
  
3.  右键单击包含 `[Qty]` 字段的单元，并单击“添加总计”。  
  
     这将向总计行添加每个订单的总数量。  
  
4.  在 `Sum[Qty]`左侧的空单元中，键入标签“**Order Total**”。  
  
5.  可以向总计行添加背景色。 选择两个累加求和单元和标签单元。  
  
6.  在 **“格式”** 菜单上，依次单击 **“背景色”**、 **“浅灰色”** 和 **“确定”**。  
  
     ![设计视图：带有订单总计的基本表](../../2014/tutorials/media/rs-basictablesumlinetotaldesign.gif "Design view: Basic table with order total")  
  
##  <a name="bkmk_adddailytotal"></a> 若要向报表添加每日总计  
  
1.  右键单击 Order 单元，指向**添加总计**，然后单击**后**。  
  
     这会添加包含每一天和标签的总量和美元总金额的新行"**总**"Order 列中。  
  
2.  在相同单元中，在 **Total** 单词之前键入 **Daily** 单词，使其显示为 **Daily Total**。  
  
3.  选定 **Daily Total** 单元、两个 **Sum** 单元及其之间的空单元。  
  
4.  在 **“格式”** 菜单上，依次单击 **“背景色”**、 **“橙色”** 和 **“确定”**。  
  
     ![](../../2014/tutorials/media/rs-basictablesumdaytotaldesign.gif "rs_BasicTableSumDayTotalDesign")  
  
##  <a name="bkmk_addgrandtotal"></a> 若要向报表添加总计  
  
1.  右键单击“Date”单元，指向“添加总计”，并单击“晚于”。  
  
     这会添加包含整个报表的总量和美元总金额的新行并**总**中的标签`Date`列。  
  
2.  在相同单元中，在 **Total** 单词之前键入 **Grand** 单词，使其显示为 **Grand Total**。  
  
3.  选定 **Grand Total** 单元、两个 **Sum** 单元及其之间的空单元。  
  
4.  在 **“格式”** 菜单上，依次单击 **“背景色”**、 **“浅蓝色”** 和 **“确定”**。  
  
     ![设计视图：基本表中的总计](../../2014/tutorials/media/rs-basictablesumgrandtotaldesign.gif "Design view: Grand total in basic table")  
  
5.  单击“预览”。  
  
     最后一页的外观应与下图相似：  
  
     ![预览：带有总计的基本表](../../2014/tutorials/media/rs-basictablesumgrandtotalpreview.gif "Preview: Basic table with grand total")  
  
##  <a name="bkmk_publishreport"></a> 若要将报表发布到报表服务器 （可选）  
  
1.  一个可选步骤是将已完成的报表发送到本机模式报表服务器上，以便您可以从报表管理器查看该报表。  
  
2.  在工具栏上，单击 **“项目”** ，然后单击 **“教程属性...”**。  
  
3.  在中**TargetServerURL**键入你的报表服务器的名称的名称，例如**http://\<服务器名 > / reportserver**  
  
4.  单击 **“确定”**。  
  
5.  在工具栏上，单击 **“生成”** ，然后单击 **“部署教程”**。  
  
     如果您在输出窗口中看到如下消息，则指示成功部署。  
  
    > ------ Build started: Project: tutorial, Configuration: Debug ------Skipping 'Sales Orders.rdl'. 项是最新。生成完成--0 个错误，0 个警告---启动的部署： 项目： 教程中，配置： 调试---部署到 http://\<服务器名称 > / reportserverDeploying 报告 / 教程/销售订单。部署完成--0 个错误，0 个警告 === 生成： 1 成功或最新，0 个失败，0 已跳过 === 部署： 1 个成功，0 失败，0 已跳过 ===  
  
     如果您看到如下错误消息，则确认您对报表服务器的权限并且已使用管理员权限启动了 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 。  
  
    > "向用户授予权限 XXXXXXXX\\< 你的用户名\>不足，无法执行此操作"  
  
6.  例如使用管理员权限，启动报表管理器中，右键单击 Internet Explorer 图标，单击**以管理员身份运行**。  
  
     浏览至报表管理器 URL，例如： `http://<server name>/reports`。  
  
7.  浏览到包含该报表的文件夹，然后单击报表的名称`Sales Orders`浏览器中查看呈现的报表。  
  
## <a name="next-steps"></a>后续步骤  
 这样，您就成功完成了对“创建基本表报表”教程的学习。  
  
## <a name="see-also"></a>请参阅  
 [筛选、 分组和对数据进行排序&#40;报表生成器和 SSRS&#41;](report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)  
  
  
