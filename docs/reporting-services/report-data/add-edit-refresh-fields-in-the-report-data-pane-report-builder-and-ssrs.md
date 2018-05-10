---
title: 在“报表数据”窗格中添加、编辑和刷新字段（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-data
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 2e36f0fe-8100-4513-b169-14d611646f81
caps.latest.revision: 7
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 637b3790cd4120969bbc75102f980ed9a6364210
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs"></a>在“报表数据”窗格中添加、编辑和刷新字段（报表生成器和 SSRS）
  数据集字段是在对外部数据源运行数据集查询时返回的表示数据的字段名称的内置集合。  
  
 对于嵌入数据集，数据集字段是您生成查询并关闭查询设计器窗格后创建的字段以及创建的计算字段。  
  
 对于共享数据集，数据集字段是将共享数据集定义添加到报表中时来自该定义的字段。 尽管在运行报表时，始终使用报表服务器上共享数据集的查询，但是报表中的数据集字段列表是静态的。  
  
 使用 **“刷新字段”** 更新报表中的字段列表，以匹配共享数据集查询中的当前字段列表。 刷新字段列表不影响您在报表中定义的计算字段。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-query-field"></a>添加查询字段  
  
1.  在“报表数据”窗格中，右键单击数据集，再单击“添加查询字段”。  
  
    > [!NOTE]  
    >  如果看不到“报表数据”窗格，请单击“视图”菜单上的“报表数据”。  
  
2.  在 **“数据集属性”** 对话框的 **“字段”** 页中，单击 **“添加”**，再单击 **“查询字段”**。 将向网格底部添加一个新行。  
  
3.  在 **“字段名称”** 文本框中，键入字段的名称。  
  
    > [!NOTE]  
    >  名称在数据集中必须是唯一的。  
  
4.  在 **“字段源”** 文本框中，键入数据源中现有字段的名称。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-add-a-calculated-field"></a>添加计算字段  
  
1.  在“报表数据”窗格中，右键单击数据集，再单击“添加计算字段”。  
  
2.  在 **“数据集属性”** 对话框的 **“字段”** 页中，单击 **“添加”**，再单击 **“计算字段”**。 将向网格底部添加一个新行。  
  
3.  在 **“字段名称”** 文本框中，键入字段的名称。  
  
    > [!NOTE]  
    >  名称在数据集中必须是唯一的。  
  
4.  在 **“字段源”** 文本框中，键入字段的表达式。 单击表达式 (**fx**) 按钮可生成表达式。  
  
    > [!NOTE]  
    >  计算字段的表达式不能包含对报表项的聚合或引用。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-edit-a-query-field-or-a-dataset-field"></a>编辑查询字段或数据集字段  
  
1.  在“报表数据”窗格中，右键单击字段，然后单击“字段属性”。  
  
2.  在 **“数据集属性”** 对话框的 **“字段”** 页中，单击现有字段来选择行。  
  
3.  更改字段名称或字段值。  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-delete-a-query-field-or-a-calculated-field"></a>删除查询字段或计算字段  
  
1.  在“报表数据”窗格中，展开数据集以显示字段集合。  
  
2.  右键单击要删除的字段，再单击“删除”。  
  
### <a name="to-refresh-the-field-collection-in-the-report-data-pane-for-a-shared-dataset"></a>为共享数据集刷新“报表数据”窗格中的字段集合  
  
1.  在“报表数据”窗格中，右键单击该数据集，然后单击“查询”。  
  
2.  单击 **“刷新字段”**。  
  
     在报表服务器上，运行共享数据集查询并返回当前的字段集合。  
  
## <a name="see-also"></a>另请参阅  
 [数据集字段集合（报表生成器和 SSRS）](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)   
 [报表数据集 (SSRS)](../../reporting-services/report-data/report-datasets-ssrs.md)   
 [报表的嵌入数据集和共享数据集（报表生成器和 SSRS）](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [Reporting Services 查询设计器](http://msdn.microsoft.com/library/07efd3f1-804f-45f7-b62a-3e727a3d9835)   
 [查询设计器（报表生成器）](http://msdn.microsoft.com/library/553f0d4e-8b1d-4148-9321-8b41a1e8e1b9)  
  
  
