---
title: "隐藏项（报表生成器和 SSRS）| Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rtp.rptdesigner.shared.visibility.f1
- "10503"
ms.assetid: 9d78f8de-959b-456f-8947-687fa6e2ba91
caps.latest.revision: "7"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 285d84aaa0f73cb8e366b6c96fcf279883591667
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="hide-an-item-report-builder-and-ssrs"></a>隐藏项（报表生成器和 SSRS）
  如果希望基于报表参数或指定的某个其他表达式来有条件地隐藏项，则可以设置报表项的可见性。  
  
 还可以设计报表（如明细报表），使用户通过单击报表中的文本框即可切换报表项的可见性。 有关详细信息，请参阅 [为项添加展开或折叠操作（报表生成器和 SSRS）](../../reporting-services/report-design/add-an-expand-or-collapse-action-to-an-item-report-builder-and-ssrs.md)。  
  
 下面的过程介绍了如何基于常量或表达式，显示或隐藏呈现报表中的报表项。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-hide-a-report-item"></a>隐藏报表项  
  
1.  在报表设计视图中，右键单击相应的报表项并打开其“属性”页。  
  
    > [!NOTE]  
    >  要选择整个表或矩阵数据区域，请在数据区域内单击以将其选定，再右键单击某个行控点、列控点或角控点，然后单击“Tablix 属性”。  
  
2.  单击 **“可见性”**。  
  
3.  在 **“在报表最初运行时”**中，指定是否要在第一次查看报表时隐藏该项：  
  
    -   若要显示项，请单击 **“显示”**。  
  
    -   若要隐藏项，请单击 **“隐藏”**。  
  
    -   要指定运行时计算的表达式，请单击“基于表达式显示或隐藏”。 键入表达式或单击表达式 (fx) 按钮，以便在“表达式”对话框中创建该表达式。  
  
        > [!NOTE]  
        >  为可见性指定表达式时，需要设置报表项的 Hidden 属性，如下图所示。 当表达式的计算结果值为 False 时，将显示报表项；当该值为 True 时，将隐藏报表项。   
        > ![Properties_Visibility 对话框和 Hidden 属性](../../reporting-services/report-builder/media/hiddenproperty-propertiesvisibility.png "Properties_Visibility dialog and Hidden property")  
  
4.  单击两次 **“确定”** 。  
  
### <a name="to-hide-static-rows-in-a-table-matrix-or-list"></a>隐藏表、矩阵或列表中的静态行  
  
1.  在报表设计视图中，单击表、矩阵或列表以显示行控点和列控点。  
  
2.  右键单击行控点，然后单击“行可见性”。 将打开 **“行可见性”** 对话框。  
  
3.  若要设置可见性，请执行第一个过程中的步骤 3 和 4。  
  
### <a name="to-hide-static-columns-in-a-table-matrix-or-list"></a>隐藏表、矩阵或列表中的静态列  
  
1.  在“设计”视图中，选择表、矩阵或列表以显示行控点和列控点。  
  
2.  右键单击列控点，然后单击“列可见性”。  
  
3.  在 **“列可见性”** 对话框中，执行第一个过程中的步骤 3 和 4。  
  
## <a name="see-also"></a>另请参阅  
 [深化操作（报表生成器和 SSRS）](../../reporting-services/report-design/drilldown-action-report-builder-and-ssrs.md)   
 [为项添加展开或折叠操作（报表生成器和 SSRS）](../../reporting-services/report-design/add-an-expand-or-collapse-action-to-an-item-report-builder-and-ssrs.md)   
 [表达式示例（报表生成器和 SSRS）](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)  
  
  
