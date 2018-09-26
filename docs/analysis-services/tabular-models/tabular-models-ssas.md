---
title: 表格模型 |Microsoft Docs
ms.date: 09/17/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1f894ad30f6344eb832cb9549a60c7f60071188c
ms.sourcegitcommit: e34e9cd1b1ec02393dc88b1f0471023a7f7f278b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/21/2018
ms.locfileid: "46506126"
---
# <a name="tabular-models"></a>表格模型
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]

  Analysis Services 中的表格模型是在内存中或在 DirectQuery 模式下，连接到数据直接从后端关系数据源中运行的数据库。 通过使用最先进的压缩算法和多线程的查询处理器，Analysis Services Vertipaq 分析引擎可以快速访问表格模型对象和数据报表 Power BI 和 Excel 等客户端应用程序。  
  
 默认内存中模型时，DirectQuery 是备选查询模式的模型因过大而无法放在内存中，或因数据易变性而排除合理处理策略。 DirectQuery 实现通过了很多的数据源，并可处理计算的表和列在 DirectQuery 模型中，通过访问后端数据库，并进行查询的 DAX 表达式的行级别安全性对支持内存中模型的奇偶校验优化会导致更快的吞吐量。
  
 表格模型中创建[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]使用表格模型项目模板。 项目模板提供了用于创建语义模型对象，如表、 分区、 关系、 层次结构、 度量值和 Kpi 的设计图面。 
  
 表格模型可以部署到 Azure Analysis Services 或 SQL Server Analysis Services 配置为使用表格服务器模式的实例。 可以在 SQL Server Management Studio 中管理已部署的表格模型。 

此处包括的表格建模文档适用，在大多数情况下，SQL Server Analysis Services 和 Azure Analysis Services。 文章特定于 Azure Analysis Services 与其他 Azure 文档一起发布。 若要了解详细信息，请参阅[Azure Analysis Services 文档](https://docs.microsoft.com/azure/analysis-services/)。
  
