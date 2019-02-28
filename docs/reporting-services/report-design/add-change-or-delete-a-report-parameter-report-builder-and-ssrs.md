---
title: 添加、更改或删除报表参数（报表生成器和 SSRS）| Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: d44a8e0a-10cf-4502-9391-09743ffc9bad
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d1c11541a449299f1dce55e720c7d882b3a70089
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2019
ms.locfileid: "56294475"
---
# <a name="add-change-or-delete-a-report-parameter-report-builder-and-ssrs"></a>添加、更改或删除报表参数（报表生成器和 SSRS）
  报表参数为选择报表数据、连接相关报表以及更改报表显示提供了一种方法。 您可以提供一个默认值和一列可用值，用户可以更改所选值。  
  
 报表发布后，您可以在报表服务器上更改报表参数的默认值、可用值以及其他属性。 通过创建链接报表，您可以提供多组默认参数值。 有关详细信息，请参阅 [报表参数（报表生成器和报表设计器）](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)的详细信息。  
  
 本文介绍如何将报表参数添加到 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] 中的分页报表或 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中的报表设计器。 还可将报表参数添加到  [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)]中的移动报表。 有关详细信息，请参阅 [Create mobile reports with SQL Server Mobile Report Publisher](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md) 。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-or-edit-a-report-parameter"></a>添加或编辑报表参数  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 的 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] 或报表设计器的“报表数据”窗格中，右键单击“参数”节点，然后单击“添加参数”。 此时将打开 **“报表参数属性”** 对话框。  
  
2.  在 **“名称”** 中，键入参数的名称，或接受默认名称。  
  
3.  在 **“提示”** 中，键入当用户运行报表时，参数文本框旁边将会显示的文本。  
  
4.  在 **“数据类型”** 中，选择参数值的数据类型。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [为报表参数添加、更改或删除可用值（报表生成器和 SSRS）](../../reporting-services/report-design/add-change-or-delete-available-values-for-a-report-parameter.md)   
 [为报表参数添加、更改或删除默认值（报表生成器和 SSRS）](../../reporting-services/report-design/add-change-or-delete-default-values-for-a-report-parameter.md)   
 [更改报表参数的顺序（报表生成器和 SSRS）](../../reporting-services/report-design/change-the-order-of-a-report-parameter-report-builder-and-ssrs.md)   
 [报表参数（报表生成器和报表设计器）](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [向报表添加级联参数（报表生成器和 SSRS）](../../reporting-services/report-design/add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)   
 [教程：向报表添加参数（报表生成器）](../../reporting-services/tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [添加数据集筛选器、数据区域筛选器和组筛选器（报表生成器和 SSRS）](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [参数集合引用（报表生成器和 SSRS）](../../reporting-services/report-design/built-in-collections-parameters-collection-references-report-builder.md)   
 [将多值参数添加到报表](../../reporting-services/report-design/add-a-multi-value-parameter-to-a-report.md)  
  
  
