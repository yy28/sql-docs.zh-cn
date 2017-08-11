---
title: "添加、 更改或删除报表参数 （报表生成器和 SSRS） |Microsoft 文档"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d44a8e0a-10cf-4502-9391-09743ffc9bad
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: bd82e177a0399fcf846e0b17e852434f2971a7ef
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="add-change-or-delete-a-report-parameter-report-builder-and-ssrs"></a>添加、更改或删除报表参数（报表生成器和 SSRS）
  报表参数为选择报表数据、连接相关报表以及更改报表显示提供了一种方法。 您可以提供一个默认值和一列可用值，用户可以更改所选值。  
  
 报表发布后，您可以在报表服务器上更改报表参数的默认值、可用值以及其他属性。 通过创建链接报表，您可以提供多组默认参数值。 有关详细信息，请参阅 [报表参数（报表生成器和报表设计器）](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)。  
  
 本文介绍如何将报表参数添加到 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] 中的分页报表或 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中的报表设计器。 还可将报表参数添加到  [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long-md.md)]中的移动报表。 有关详细信息，请参阅 [Create mobile reports with SQL Server Mobile Report Publisher](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md) 。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-or-edit-a-report-parameter"></a>添加或编辑报表参数  
  
1.  在[!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)]或报表设计器中[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中**报表数据**窗格中，右键单击**参数**节点，然后单击**添加参数**。 此时将打开 **“报表参数属性”** 对话框。  
  
2.  在 **“名称”**中，键入参数的名称，或接受默认名称。  
  
3.  在 **“提示”**中，键入当用户运行报表时，参数文本框旁边将会显示的文本。  
  
4.  在 **“数据类型”**中，选择参数值的数据类型。  
  
5.  如果参数可以包含空白值，请选择 **“允许空白值”**。  
  
6.  如果参数可以包含 Null 值，请选择 **“允许 Null 值”**。  
  
7.  若要允许用户为参数选择多个值，请选择 **“允许多个值”**。  
  
8.  设置可见性选项。  
  
    -   若要在报表顶部的工具栏中显示参数，请选择 **“可见”**。  
  
    -   若要隐藏参数使其不显示在工具栏中，请选择 **“隐藏”**。  
  
    -   若要隐藏参数，以保护其不会在报表发布后，被从报表服务器上修改，请选择 **“内部”**。 这样将仅可在报表定义中查看该报表参数。 对于此选项，您必须设置一个默认值，或允许参数接受 Null 值。  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-delete-a-report-parameter"></a>删除报表参数  
  
1.  在 **“报表数据”** 窗格中，展开 **“参数”** 节点。  
  
2.  右键单击报表参数，然后单击 **“删除”**。  
  
## <a name="see-also"></a>另請參閱  
 [为报表参数添加、更改或删除可用值（报表生成器和 SSRS）](../../reporting-services/report-design/add-change-or-delete-available-values-for-a-report-parameter.md)   
 [添加、 更改或删除报表参数 &#40; 默认值报表生成器和 SSRS &#41;](../../reporting-services/report-design/add-change-or-delete-default-values-for-a-report-parameter.md)   
 [更改报表参数 &#40; 的顺序报表生成器和 SSRS &#41;](../../reporting-services/report-design/change-the-order-of-a-report-parameter-report-builder-and-ssrs.md)   
 [报表参数 &#40;报表生成器和报表设计器 &#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [将级联参数添加到报表 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)   
 [教程： 将参数添加到您的报表 &#40;报表生成器 &#41;](../../reporting-services/tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [添加数据集筛选器、 数据区域筛选器和组筛选器 （&） #40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [参数的集合引用 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/built-in-collections-parameters-collection-references-report-builder.md)   
 [将多值参数添加到报表](../../reporting-services/report-design/add-a-multi-value-parameter-to-a-report.md)  
  
  
