---
title: "报表模型查询设计器用户界面 |Microsoft 文档"
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
- "10015"
- sql13.rtp.rptdesigner.dataview.smqlquerydesigner.f1
helpviewer_keywords:
- report models [Reporting Services], queries
- datasets [Reporting Services], creating
- query designers [Reporting Services]
ms.assetid: db86c208-ff1e-4297-aa0c-c250f053f83e
caps.latest.revision: 31
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 08ab050564e74a18d8231701f2355c042efc8685
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="report-model-query-designer-user-interface"></a>报表模型查询设计器用户界面
  报表设计器提供了两个查询设计器，可帮助您指定报表服务器模型数据源中要用于报表的数据。 使用图形查询设计器可以浏览和选择模型实体和实体字段。 使用基于文本的查询设计器可以直接以 XML 格式使用语义模型定义语言 (SMDL) 规范。  
  
> [!IMPORTANT]  
>  用户创建和运行查询时访问数据源。 您应授予对数据源的最小权限（如只读权限）。  
  
## <a name="graphical-query-designer"></a>图形查询设计器  
 报表设计器提供了图形查询设计器，用于设计并运行在报表处理期间填充报表数据集的字段集合的 SMDL 查询。 图形查询设计器分为三个区域（或窗格）。  
  
 下图标出了每个窗格。  
  
 ![语义模型查询设计器 UI](../../reporting-services/report-data/media/rsqd-dsawmodel-smql.gif "语义模型查询设计器 UI")  
  
 下表介绍了每个窗格的功能。  
  
|窗格|函数|  
|----------|--------------|  
|“资源管理器”窗格|显示模型中的实体和实体字段的图形化表示形式。 使用此窗格可以浏览实体、实体之间的关系以及字段。|  
|设计区域|显示模型中的字段列表。 使用此窗格可以排列所选字段的布局。|  
|“结果”窗格|显示查询的结果。 若要运行查询，在任何窗格中，右键单击，然后单击**运行**，或单击**运行**(![运行查询](../../reporting-services/report-data/media/rsqdicon-run.gif "运行查询")) 在工具栏上的按钮。|  
  
 若在“资源管理器”和“设计区域”窗格中更改信息，则单击 **“运行”**时将会影响到“结果”窗格中的内容。  
  
 若要在某个特定窗格中执行操作（如在设计区域中删除列），请右键单击该列，然后单击菜单上的命令。  
  
### <a name="graphical-query-designer-toolbar"></a>图形查询设计器工具栏  
 设计查询时也可以使用工具栏按钮。 下表列出了工具栏中的按钮及其用途。  
  
|按钮|Description|  
|------------|-----------------|  
|**编辑为文本**|在基于文本的查询设计器和图形查询设计器之间切换。 报表服务器模型数据源的查询为 XML 格式的语义模型查询语言 (SMQL) 规范。|  
|**导入**|从文件系统中的报表定义 (.rdl) 文件导入现有查询。 有关详细信息，请参阅[报表的嵌入数据集和共享数据集（报表生成器和 SSRS）](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)。|  
|![撤消操作](../../reporting-services/report-data/media/rsqdicon-undo.gif "撤消操作")|撤消上一操作。|  
|![重做操作](../../reporting-services/report-data/media/rsqdicon-redo.gif "重做操作")|重做上一操作。|  
|![运行查询](../../reporting-services/report-data/media/rsqdicon-run.gif "运行查询")|运行查询并在“结果”窗格中显示结果行。|  
|![选定的筛选器列旁边的筛选器图形](../../reporting-services/report-data/media/rsqdicon-filter.gif "选定的筛选器列旁边的筛选器图形")|打开 **“筛选数据”** 对话框，以便指定要筛选的数据。 可以独立于当前设计区域中的数据单独指定筛选器。|  
  
## <a name="text-based-query-designer"></a>基于文本的查询设计器  
 创建报表服务器模型数据集查询时，默认情况下，会显示图形查询设计器。 若要切换为基于文本的查询设计器，请单击工具栏上的“编辑为文本”切换按钮。  
  
 基于文本的查询设计器包含两个窗格：“SMQL 查询”窗格和“结果”窗格。 当您已经有来自其他源的 SMQL 查询规范并且要将其粘贴到查询窗格时，查询设计器视图很有用。 与图形查询设计器不同的是，基于文本的查询设计器不检查查询语法或重新组织查询的结构。 单击工具栏上的 **“运行”** 时，将在数据源中运行查询并在“结果”窗格中显示结果。  
  
 下图标出了每个窗格。  
  
 ![泛型语义模型语言查询设计器](../../reporting-services/report-data/media/rsqd-dsawmodel-smql-generic.gif "泛型语义模型语言查询设计器")  
  
 下表介绍了每个窗格的功能。  
  
|窗格|函数|  
|----------|--------------|  
|“查询”窗格|显示 SMQL 规范文本。|  
|“结果”窗格|显示查询的结果。 若要运行查询，请右键单击任意窗格，再单击“运行”，或者单击工具栏中的“运行”按钮。|  
  
### <a name="text-based-query-designer-toolbar"></a>基于文本的查询设计器工具栏  
 设计查询时也可以使用工具栏按钮。 下表列出了工具栏中的按钮及其用途。  
  
|按钮|Description|  
|------------|-----------------|  
|**编辑为文本**|在基于文本的查询设计器和图形查询设计器之间切换。|  
|**导入**|从现有报表导入查询。|  
|![运行查询](../../reporting-services/report-data/media/rsqdicon-run.gif "运行查询")|运行查询文本并在“结果”窗格中显示结果行集。|  
  
## <a name="see-also"></a>另请参阅  
 [查询设计工具 (SSRS)](../../reporting-services/report-data/query-design-tools-ssrs.md)   
 [从外部数据源中添加数据 (SSRS)](../../reporting-services/report-data/add-data-from-external-data-sources-ssrs.md)   
 [报表模型连接 &#40;SSRS &#41;](../../reporting-services/report-data/report-model-connection-ssrs.md)   
 [RSReportDesigner 配置文件](../../reporting-services/report-server/rsreportdesigner-configuration-file.md)  
  
  
