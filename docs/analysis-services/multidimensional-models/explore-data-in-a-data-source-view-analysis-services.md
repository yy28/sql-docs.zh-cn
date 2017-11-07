---
title: "浏览数据源视图 (Analysis Services) 中的数据 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- exploring data [Analysis Services]
- data source views [Analysis Services], exploring data
- viewing source data
ms.assetid: 2c922c35-fbcb-45b2-96b1-c7a846d8b419
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: de15507d7fedd1f582e158e85d1f6245972cf27b
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="explore-data-in-a-data-source-view-analysis-services"></a>在数据源视图中浏览数据 (Analysis Services)
  可以使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 的数据源视图设计器中的“浏览数据”对话框，在数据源视图 (DSV) 中浏览表、视图或命名查询的数据。 在数据源视图设计器中浏览数据时，可以查看所选表、视图或命名查询中每个数据列的内容。 查看实际内容将帮助您确定是否需要所有列，是否需要命名计算来提高用户友好性和可用性，以及现有命名计算或命名查询是否返回预期值。  
  
 若要查看数据，必须与 DSV 中所选对象的一个或多个数据源建立活动连接。 此外，还在该查询中发送表中的任何命名计算。  
  
 您可以对以表格格式返回的数据进行排序和复制。 单击列标题可以按该列对行进行重新排序。 也可以突出显示网格中的数据，然后按下 Ctrl-C 以便将选定内容复制到剪贴板。  
  
 还可以控制抽样方法和抽样计数。 默认情况下，将返回前 5000 行。  
  
## <a name="to-browse-data-or-change-sampling-options"></a>浏览数据或更改抽样选项  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开项目或连接到数据库，此项目或数据库包含要在其中浏览数据的数据源视图。  
  
2.  在解决方案资源管理器中，展开“数据源视图”文件夹，然后双击数据源视图。  
  
3.  右键单击包含要查看的数据的表、视图或命名查询，再单击“浏览数据”。  
  
     数据源基础表、 视图或命名查询中的数据源视图是查询，并且结果将显示在**浏览\<对象名称 > 表**选项卡。  
  
4.  上**浏览\<对象名称 > 表**工具栏上，单击**抽样选项**图标。  
  
     此时将打开 **“数据浏览选项”** 对话框。 在该对话框中可以指定抽样方法（记录少于或多于默认抽样大小 5000 行）或抽样计数。  
  
5.  根据需要单击 **“确定”** 或 **“取消”** 。  
  
6.  若要对数据重新取样，请单击**重新取样数据**上**浏览\<对象名称 > 表**工具栏。  
  
## <a name="see-also"></a>另请参阅  
 [多维模型中的数据源视图](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)  
  
  

