---
title: "数据定义查询 （数据挖掘） |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 49e02de1-4ffa-401c-8eee-471a9c25b86a
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 04237bba7622a7b6745ff8768ea7a1bc5feda2b5
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="data-definition-queries-data-mining"></a>数据定义查询（数据挖掘）
  对于数据挖掘，“数据定义查询”  类别是指执行以下操作的 DMX 语句或 XMLA 命令：  
  
-   创建、更改或操作数据挖掘对象（如模型）。  
  
-   定义要用于定型或预测的数据的源。  
  
-   导出或导入挖掘模型和挖掘结构。  
  
 [创建数据定义查询](#bkmk_Create)  
  
-   [SQL Server Data Tools 中的数据定义查询](#bkmk_ssdt)  
  
-   [SQL Server Management Studio 中的数据定义查询](#bkmk_SSMS)  
  
 [脚本数据定义语句](#bkmk_Scripts)  
  
 [脚本数据定义语句](#bkmk_Export)  
  
##  <a name="bkmk_Create"></a> 创建数据定义查询  
 可以使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 和 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的预测查询生成器或使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的 DMX 查询窗口来创建数据定义查询（语句）。 DMX 中的数据定义语句属于 Analysis Services 数据定义语言 (DDL)。  
  
 有关特定数据定义语句的语法的信息，请参阅[数据挖掘扩展插件 (DMX) 引用](../../dmx/data-mining-extensions-dmx-reference.md)。  
  
###  <a name="bkmk_ssdt"></a> SQL Server Data Tools 中的数据定义查询  
 数据挖掘向导是 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中用来执行以下操作的首选工具：创建和修改挖掘模型和挖掘结构，以及定义用于预测查询和定型的数据源。  
  
 但是，如果您想知道该向导向服务器发送了哪些语句来创建数据结构或挖掘模型，则可使用 SQL Server Profiler 来捕获数据定义语句。 有关详细信息，请参阅 [Use SQL Server Profiler to Monitor Analysis Services](../../analysis-services/instances/use-sql-server-profiler-to-monitor-analysis-services.md)。  
  
 若要查看在定义用于定型或预测的数据源时使用的语句，可以使用预测查询生成器中的 **“SQL 视图”** 。 有时，使用预测查询生成器来生成用于定型和测试模型的基本查询对于建立正确的语法会很有用。 您可以切换到 **“SQL 视图”** 并手动编辑查询。 有关详细信息，请参阅 [Manually Edit a Prediction Query](../../analysis-services/data-mining/manually-edit-a-prediction-query.md)。  
  
###  <a name="bkmk_SSMS"></a> SQL Server Management Studio 中的数据定义查询  
 对于数据挖掘对象，可以使用数据定义查询来执行以下操作：  
  
-   使用 [CREATE MINING MODEL (DMX)](../../dmx/create-mining-model-dmx.md) 创建特定类型的模型，如聚类分析模型或决策树模型。  
  
-   通过添加模型或使用 [ALTER MINING STRUCTURE (DMX)](../../dmx/alter-mining-structure-dmx.md) 更改列来更改现有挖掘结构。 请注意，无法使用 DMX 更改挖掘模型；只能向现有结构中添加新模型。  
  
-   创建挖掘模型的副本，然后使用 [SELECT INTO (DMX)](../../dmx/select-into-dmx.md) 更改该副本。  
  
-   通过将 [INSERT INTO (DMX)](../../dmx/insert-into-dmx.md) 与数据源查询（如 OPENROWSET）结合使用来定义用于定型的数据集。  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 提供了可帮助您创建数据定义查询的查询模板。 有关详细信息，请参阅 [Use Analysis Services Templates in SQL Server Management Studio](../../analysis-services/instances/use-analysis-services-templates-in-sql-server-management-studio.md)。  
  
 通常， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中为 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 提供的模板只包含常规语法定义，您必须使用 **“查询”** 窗口或用于输入参数的对话框来自定义该模板。  
  
 有关如何使用接口输入参数的示例，请参阅 [通过模板创建单独预测查询](../../analysis-services/data-mining/create-a-singleton-prediction-query-from-a-template.md)。  
  
###  <a name="bkmk_Scripts"></a> 脚本数据定义语句  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 提供了多种脚本语言和编程语言，可以用来创建或更改数据挖掘对象，也可以用来定义数据源。  虽然 DMX 旨在加快执行数据挖掘任务，但您也可以同时使用 XMLA 和 AMO 来操作脚本或自定义代码中的对象。  
  
 用于 Excel 的数据挖掘外接程序还包含了多个查询模板，并提供了“高级查询编辑器”，有助于编写复杂的 DMX 语句。 可以通过交互方式生成查询，然后切换到 SQL 视图以捕获 DMX 语句。  
  
##  <a name="bkmk_Export"></a> 导出和导入模型  
 可以使用 DMX 中的数据定义语句来导出模型的定义及其所需的结构和数据源，然后再将该定义导入其他服务器。 使用导出和导入是在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]实例之间移动数据挖掘模型和挖掘结构的最快且最便捷的方法。 有关详细信息，请参阅 [管理数据挖掘解决方案和对象](../../analysis-services/data-mining/management-of-data-mining-solutions-and-objects.md)。  
  
> [!WARNING]  
>  如果模型基于多维数据集数据源中的数据，则您无法使用 DMX 导出模型，而应改用备份和还原功能。  
  
##  <a name="bkmk_Tasks"></a> 相关任务  
 下表提供了一些链接，这些链接指向与数据定义查询相关的任务。  
  
|||  
|-|-|  
|使用 DMX 查询模板。|[Use Analysis Services Templates in SQL Server Management Studio](../../analysis-services/instances/use-analysis-services-templates-in-sql-server-management-studio.md)|  
|使用预测查询生成器来设计所有类型的查询。|[使用预测查询生成器创建预测查询](../../analysis-services/data-mining/create-a-prediction-query-using-the-prediction-query-builder.md)|  
|使用 SQL Server Profiler 捕获查询定义，并使用跟踪来监视 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。|[Use SQL Server Profiler to Monitor Analysis Services](../../analysis-services/instances/use-sql-server-profiler-to-monitor-analysis-services.md)|  
|了解有关为 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]提供的脚本语言和编程语言的详细信息。|[XML for Analysis (XMLA) 参考](../../analysis-services/xmla/xml-for-analysis-xmla-reference.md)<br /><br /> [使用分析管理对象 (AMO) 进行开发](../../analysis-services/multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md)|  
|了解如何管理 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 和 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中的模型。|[导出和导入数据挖掘对象](../../analysis-services/data-mining/export-and-import-data-mining-objects.md)<br /><br /> [EXPORT (DMX)](../../dmx/export-dmx.md)<br /><br /> [IMPORT (DMX)](../../dmx/import-dmx.md)|  
|了解有关 OPENROWSET 和用于查询外部数据的其他方法的详细信息。|[<源数据查询>](../../dmx/source-data-query.md)。|  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘向导（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/data-mining-wizard-analysis-services-data-mining.md)  
  
  
