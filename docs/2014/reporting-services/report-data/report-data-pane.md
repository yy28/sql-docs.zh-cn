---
title: “报表数据”窗格 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.reportdata.f1
- "10039"
helpviewer_keywords:
- Report Data pane
ms.assetid: aa9614a3-12e7-4e17-9de2-fafccd1f5f9d
caps.latest.revision: 27
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 464bdb206986b01de68b018b8b6128956aee7036
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37270563"
---
# <a name="report-data-pane"></a>“报表数据”窗格
  使用 **“报表数据”** 窗格可以查看报表中当前定义的参数、数据源、数据集、字段集合和图像。 该窗格会显示表示报表中数据的项的层次结构视图。 顶级节点表示内置字段、参数、图像和数据源引用。 展开每个节点可以查看各数据项。 例如，展开某个数据源节点时，会显示为该数据源定义的数据集。 展开数据集时，会显示其字段集合。 将这些数据项拖放到报表设计图面可将数据与报表页中的报表项链接。  
  
## <a name="options"></a>“常规”  
 **内置字段**  
 表示 Reporting Services 提供的在报表中常用的字段，例如报表名称或页码。 有关详细信息，请参阅[表达式中的内置集合（报表生成器和 SSRS）](../report-design/built-in-collections-in-expressions-report-builder.md)。  
  
 **Parameters**  
 表示报表参数的集合，每个参数都可为单值或多值参数。 有关详细信息，请参阅[报表参数（报表生成器和报表设计器）](../report-design/report-parameters-report-builder-and-report-designer.md)。  
  
 **映像**  
 表示报表中使用的图像集。 有关详细信息，请参阅[图像（报表生成器和 SSRS）](../report-design/images-report-builder-and-ssrs.md)。  
  
 **数据源**  
 表示对嵌入数据源或共享数据源的单个数据源引用。 在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，共享数据源显示在“共享数据源”文件夹下的解决方案资源管理器中。 数据源会指定 Reporting Services 支持的一种数据源类型。 数据源是基于其的数据集集合的父节点。 有关详细信息，请参阅[数据连接、 数据源和 Reporting Services 中的连接字符串](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)。  
  
 **数据集**  
 表示单个数据集。 数据集是查询指定的字段集合的父节点，包括所有计算字段。 Reporting Services 支持查询设计器，这将有助于您指定查询。 有关详细信息，请参阅[向报表添加数据&#40;报表生成器和 SSRS&#41; ](report-datasets-ssrs.md)并[报表设计器 SQL Server Data Tools 中的查询设计工具&#40;SSRS&#41;](query-design-tools-ssrs.md)。  
  
## <a name="see-also"></a>请参阅  
 [数据集字段集合（报表生成器和 SSRS）](dataset-fields-collection-report-builder-and-ssrs.md)   
 [“分组”窗格](../tools/grouping-pane.md)  
  
  
