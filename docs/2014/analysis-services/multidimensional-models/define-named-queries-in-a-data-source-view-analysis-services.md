---
title: 数据源视图 (Analysis Services) 中定义命名的查询 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- named queries [Analysis Services], creating
- modifying named queries
- data source views [Analysis Services], named queries
ms.assetid: f09ba8aa-950e-4c0d-961e-970de13200be
caps.latest.revision: 30
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: aacf40665a651436c159aeb67a6514c6647883e7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37263813"
---
# <a name="define-named-queries-in-a-data-source-view-analysis-services"></a>在数据源视图中定义命名查询 (Analysis Services)
  命名查询是以表的形式表示的 SQL 表达式。 在命名查询中，可以指定一个 SQL 表达式以选择从一个或多个数据源的一个或多个表返回的行和列。 命名查询基于一个表达式，除此之外，它在行和关系方面都与数据源视图 (DSV) 中的其他表相似。  
  
 命名查询允许您不修改基础数据源即可扩展 DSV 中现有表的关系架构。 例如，可以使用一系列命名查询将一个复杂的维度表分割为几个较小、较简单的维度表以便在数据库维度中使用。 命名查询还可以用来将来自一个或多个数据源的多个数据库表联接到单个数据源视图表。  
  
## <a name="creating-a-named-query"></a>创建命名查询  
  
> [!NOTE]  
>  您不能将命名计算添加到命名查询，也不能基于包含命名计算的表创建命名查询。  
  
 创建命名查询时，需要为 SQL 查询返回的此表的列和数据指定名称，并根据需要对命名查询进行说明。 SQL 表达式可以引用数据源视图中的其他表。 定义命名查询后，命名查询中的 SQL 查询将发送到数据源提供程序并作为一个整体进行验证。 如果提供程序在 SQL 查询中没有发现任何错误，则将该列添加到表中。  
  
 SQL 查询中引用的表和列不应被限定或只应由表名限定。 例如，在引用某个表中的 SaleAmount 列时， `SaleAmount` 或 `Sales.SaleAmount` 是有效的，而 `dbo.Sales.SaleAmount` 则会生成错误。  
  
 **请注意** 定义查询 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 数据源的命名查询时，包含相关子查询和 GROUP BY 子句的命名查询将失败。 有关详细信息，请参阅 [知识库中的](http://support.microsoft.com/kb/274729) Internal Error with SELECT Statement Containing Correlated Subquery and GROUP BY [!INCLUDE[msCoName](../../includes/msconame-md.md)] （有关包含相关子查询和 GROUP BY 的 SELECT 语句的内部错误）。  
  
## <a name="add-or-edit-a-named-query"></a>添加或编辑命名查询  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开项目或连接到数据库，此项目或数据库包含要在其中添加命名查询的数据源视图。  
  
2.  在解决方案资源管理器中，展开“数据源视图”文件夹，然后双击数据源视图。  
  
3.  在“表”或“关系图”窗格中，右键单击空白区域，再单击“新建命名查询”。  
  
4.  在 **“创建命名查询”** 对话框中，执行下列操作：  
  
    1.  在 **“名称”** 文本框中，键入查询名称。  
  
    2.  还可以在 **“说明”** 文本框中键入对查询的说明。  
  
    3.  在 **“数据源”** 列表框中，选择将对其执行命名查询的数据源。  
  
    4.  在底部窗格中键入此查询，或者使用图形查询生成工具创建查询。  
  
    > [!NOTE]  
    >  查询生成用户界面 (UI) 取决于数据源。 您所得到的不是图形 UI，而是基于文本的一般 UI。 您可以使用这些不同的 UI 来实现同样的功能，但必须以不同的方式来操作。 有关详细信息，请参阅[“创建或编辑命名查询”对话框（Analysis Services - 多维数据）](../create-or-edit-named-query-dialog-box-analysis-services-multidimensional-data.md)。  
  
5.  单击“确定” 。 一个显示两个重叠表的图标出现在表格表头上，指示此表已被一个命名查询替代。  
  
## <a name="see-also"></a>请参阅  
 [多维模型中的数据源视图](data-source-views-in-multidimensional-models.md)   
 [数据源视图中定义命名的计算&#40;Analysis Services&#41;](define-named-calculations-in-a-data-source-view-analysis-services.md)  
  
  
