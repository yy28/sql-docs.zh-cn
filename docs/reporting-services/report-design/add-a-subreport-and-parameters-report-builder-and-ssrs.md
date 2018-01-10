---
title: "添加子报表和参数（报表生成器和 SSRS）| Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- "10093"
- sql13.rtp.rptdesigner.subreportproperties.general.f1
ms.assetid: 94f960f8-a629-4f1e-8277-c3b8f0680d98
caps.latest.revision: "9"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: bef0babb7531e4ef6c513175515fb8e92ac89e6b
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2018
---
# <a name="add-a-subreport-and-parameters-report-builder-and-ssrs"></a>添加子报表和参数（报表生成器和 SSRS）
  当您希望创建作为多个相关报表的容器的主报表时，可以向报表添加子报表。 子报表是对另一个报表的引用。 若要通过数据值使报表相关联（例如，使多个报表显示同一客户的数据），必须设计参数化报表（例如，显示特定客户详细信息的报表）作为子报表。 向主报表添加子报表时，可以指定传递给子报表的参数。  
  
 还可以向表或矩阵中的动态行或动态列添加子报表。 处理主报表时，会处理每行的子报表。 在这种情况下，请考虑您是否能通过使用数据区域或嵌套数据区域实现所需的效果。  
  
 若要向报表中添加子报表，您必须首先创建将作为子报表的报表。 有关创建子报表详细信息，请参阅 [子报表（报表生成器和 SSRS）](../../reporting-services/report-design/subreports-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-subreport"></a>添加子报表  
  
1.  在 **“插入”** 选项卡上，单击 **“子报表”**。  
  
2.  在设计图面上，单击报表上的某个位置，然后拖动一个框调整到所需子报表大小。 也可以单击设计图面来创建默认大小的子报表。  
  
3.  右键单击子报表，然后单击“子报表属性”。  
  
4.  在 **“子报表属性”** 对话框的 **“名称”** 文本框中键入名称，或接受默认值。 该名称在报表中必须是唯一的。 默认情况下，会分配一个常规名称，例如 Subreport1 或 Subreport2。  
  
5.  在 **“将此报表用作子报表”** 框中，单击 **“浏览”**，或者键入报表的名称。 应当优先单击 **“浏览”** ，因为将自动指定子报表的路径。 可以通过多种方式指定报表。 有关详细信息，请参阅[指定外部项的路径（报表生成器和 SSRS）](../../reporting-services/report-design/specifying-paths-to-external-items-report-builder-and-ssrs.md)。  
  
6.  （可选）如果子报表横跨多页，针对“去掉分页符上的边框”单击“是”，就可以避免在子报表中间呈现边框。  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-specify-parameters-to-pass-to-a-subreport"></a>指定传递给子报表的参数  
  
1.  在“设计”视图中，右键单击子报表，然后单击“子报表属性”。  
  
2.  在 **“子报表属性”** 对话框中，单击 **“参数”**。  
  
3.  单击 **“添加”**。 将向参数网格添加一个新行。  
  
4.  在 **“名称”** 文本框中，键入子报表中参数的名称或者从列表框中选择该名称。 该名称必须与子报表中的报表参数的名称（而不是查询参数的名称）相匹配。  
  
5.  在 **“值”** 列表框中，键入或选择要传递给子报表的值。 此值可以是静态文本、引用字段的表达式或主报表中的其他对象。  
  
    > [!NOTE]  
    >  在报表生成器中，如果“参数”列表中缺少某参数并且子报表定义了默认值，则会正确处理子报表。  
    >   
    >  在报表设计器中，子报表所需的所有参数都必须包括在 **“参数”** 列表中。 如果缺少必需的参数，子报表将不会在主报表中正确显示。  
  
6.  重复步骤 3-5，以便指定每个子报表参数的名称和值。  
  
7.  若要删除子报表参数，请单击参数网格中的相应参数，然后单击 **“删除”**。  
  
8.  若要更改子报表参数的顺序，请单击相应参数，再单击上移按钮或下移按钮。  
  
     更改子报表参数的顺序不会影响子报表的处理。  
  
## <a name="see-also"></a>另请参阅  
 [子报表（报表生成器和 SSRS）](../../reporting-services/report-design/subreports-report-builder-and-ssrs.md)   
 [呈现行为（报表生成器和 SSRS）](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)  
  
  
