---
title: 报表数据窗格 （报表生成器） |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- "10435"
helpviewer_keywords:
- Report Data pane
ms.assetid: 1492aa39-aeb1-4509-ab97-b9edd0901b7e
caps.latest.revision: 11
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: cf8180224bd06e2f5e38316c992063621796d42b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36128029"
---
# <a name="report-data-pane-report-builder"></a>“报表数据”窗格（报表生成器）
  使用 **“报表数据”** 窗格可以查看报表中当前定义的参数、数据源、数据集、字段集合和图像。 该窗格会显示表示报表中数据的项的层次结构视图。 顶级节点表示内置字段、参数、图像和数据源引用。 展开每个节点可以查看各数据项。 例如，展开某个数据源节点时，会显示为该数据源定义的数据集。 展开数据集时，会显示其字段集合。 将报表项拖至报表设计图面或“分组”窗格可将数据与报表页上选定的报表项相链接。 有关详细信息，请参阅[报表设计视图（报表生成器）](report-builder/report-design-view-report-builder.md)。  
  
## <a name="options"></a>“常规”  
 **内置字段**  
 表示报表中常用的字段，如报表名称或页码。 有关详细信息，请参阅[表达式中的内置集合（报表生成器和 SSRS）](report-design/built-in-collections-in-expressions-report-builder.md)。  
  
 **Parameters**  
 表示报表参数的集合，每个参数都可为单值或多值参数。 有关详细信息，请参阅[报表参数（报表生成器和报表设计器）](report-design/report-parameters-report-builder-and-report-designer.md)。  
  
 **映像**  
 表示报表中使用的图像集。 有关详细信息，请参阅[图像（报表生成器和 SSRS）](report-design/images-report-builder-and-ssrs.md)。  
  
 **数据源**  
 表示一个嵌入数据源或对共享数据源的引用。 数据源表示报表的数据源。 数据源是使用该数据源的数据集集合的父节点。 有关详细信息，请参阅[向报表添加数据&#40;报表生成器和 SSRS&#41; ](report-data/report-datasets-ssrs.md)和[数据连接、 数据源和报表生成器中的连接字符串](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-report-builder.md)。  
  
 **数据集**  
 表示通过运行某个命令（如用于从 [!INCLUDE[tsql](../includes/tsql-md.md)] 数据库检索数据的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 查询）从数据源检索到的数据。 数据集是查询指定的字段集合（也包括计算字段）的父节点。 Report Builder 支持可帮助您指定查询的查询设计器。 有关详细信息，请参阅[向报表添加数据&#40;报表生成器和 SSRS&#41;](report-data/report-datasets-ssrs.md)。  
  
## <a name="see-also"></a>请参阅  
 [数据集字段集合（报表生成器和 SSRS）](report-data/dataset-fields-collection-report-builder-and-ssrs.md)   
 [用于对话框、窗格和向导的报表生成器帮助](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [“分组”窗格（报表生成器）](report-design/grouping-pane-report-builder.md)   
 [查找、查看和管理报表（报表生成器和 SSRS）](report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)  
  
  