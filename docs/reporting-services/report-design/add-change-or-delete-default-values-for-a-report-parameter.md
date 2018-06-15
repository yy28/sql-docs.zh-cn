---
title: 为报表参数添加、更改或删除默认值 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-design
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- "10460"
- sql13.rtp.rptdesigner.reportparameters.defaultvalues.f1
- "10072"
ms.assetid: 6a87e069-b3a9-47b6-bcec-afcdd8aff65f
caps.latest.revision: 11
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 86e726e458454a5f1016b36b5a63f0e4fdaaf542
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "33021054"
---
# <a name="add-change-or-delete-default-values-for-a-report-parameter"></a>为报表参数添加、更改或删除默认值
  创建报表参数后，您可以提供一个默认值列表。 如果所有参数都有有效默认值，报表会在您第一次查看或预览它时自动运行。  
  
 报表参数可以是单值参数或多值参数。 对于单值参数，可以提供一个文字或表达式。 对于多值参数，可以提供静态值列表或者来自报表数据集的列表。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 在您发布某一报表后，您可以通过对报表服务器设置参数属性值，在报表创作工具中覆盖在报表中定义的默认值。 您还可以通过创建链接报表，提供多组默认参数值。 有关详细信息，请参阅  [报表参数（报表生成器和报表设计器）](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)  
  
### <a name="to-add-or-change-the-default-values-for-a-report-parameter"></a>添加或更改报表参数的默认值  
  
1.  在“报表数据”窗格中，展开 **“参数”** 节点。 右键单击该参数，然后单击“编辑”。 此时将打开 **“报表参数属性”** 对话框。  
  
    > [!NOTE]  
    >  如果“报表数据”窗格不可见，请单击“视图”，然后单击“报表数据”。  
  
2.  单击 **“默认值”**。  
  
3.  选择一个默认选项：  
  
    -   若要手动提供一个值或值列表，请单击 **“指定值”**。 单击 **“添加”** ，然后在 **“值”** 文本框中输入值。 您可以为值编写表达式。 数据类型必须与参数的数据类型相匹配。 字段名称不能用于参数的表达式中。  
  
         对于多值参数，对每个要提供的值重复此步骤。 您在此列表中看到的项的顺序将决定用户在下拉列表中看到这些项的顺序。 若要更改列表中某一项的顺序，单击 **“值”** 文本框选择该项，然后使用上箭头或下箭头按钮在列表中上下移动该项。  
  
    -   若要提供检索值的现有数据集的名称，请单击 **“从查询中获取值”**。 在 **“数据集”** 中，选择该数据集的名称。  
  
         在 **“值字段”** 中，选择提供参数值的字段的名称。  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-remove-the-default-values-for-a-report-parameter"></a>删除报表参数的默认值  
  
1.  在“报表数据”窗格中，展开 **“参数”** 节点。 右键单击该参数，然后单击“编辑”。 此时将打开 **“报表参数属性”** 对话框。  
  
2.  单击 **“默认值”**。  
  
3.  在 **“选择以下选项之一”** 中，单击 **“无默认值”**。  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [报表参数（报表生成器和报表设计器）](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [向报表添加级联参数（报表生成器和 SSRS）](../../reporting-services/report-design/add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)   
 [教程：向报表添加参数（报表生成器）](../../reporting-services/tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [添加数据集筛选器、数据区域筛选器和组筛选器（报表生成器和 SSRS）](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [参数集合引用（报表生成器和 SSRS）](../../reporting-services/report-design/built-in-collections-parameters-collection-references-report-builder.md)   
 [更改报表参数的顺序（报表生成器和 SSRS）](../../reporting-services/report-design/change-the-order-of-a-report-parameter-report-builder-and-ssrs.md)   
 [添加、更改或删除报表参数（报表生成器和 SSRS）](../../reporting-services/report-design/add-change-or-delete-a-report-parameter-report-builder-and-ssrs.md)   
 [表达式（报表生成器和 SSRS）](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  
