---
title: 表格模型 |Microsoft 文档
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8e85a618379b5b3c6da010c8b25782ed6836edb4
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="tabular-models"></a>表格模型
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  表格模型是在内存中或在 DirectQuery 模式下运行，并直接从后端关系数据源访问数据的 Analysis Services 数据库。 通过使用最先进的压缩算法和多线程的查询处理器，分析引擎提供快速访问，对表格模型对象和数据通过报告客户端应用程序，如 Power BI 和 Excel。  
  
 默认内存中模型时，DirectQuery 是备选查询模式的模型都是太大，无法适应在内存中，或因数据易变性排除合理处理策略。 DirectQuery 实现通过支持多种不同的数据源能够处理计算的表和列在 DirectQuery 模型中，通过的 DAX 表达式。 到达后端数据库，以及如何查询的行级别安全性的内存中模型的奇偶校验导致更快的生产率的优化。
  
 在中创建表格模型[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]使用表格模型项目模板提供用于创建模型、 表、 关系和 DAX 表达式的设计图面。 你可以从多个源导入数据，然后添加关系、计算的表和列、度量值、KPI、层次结构和翻译，使模型更加丰富。  
  
 模型然后可部署到 Azure Analysis Services 或 SQL Server Analysis Services 的实例配置为表格服务器模式。 可以在 SQL Server Management Studio 中管理已部署的表格模型。 当您的模型增多时，它们可以进行优化处理分区和使用基于角色的安全性保护到行级别。  

  
  
