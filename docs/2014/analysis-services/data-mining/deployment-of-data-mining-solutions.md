---
title: 部署数据挖掘解决方案 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models [Analysis Services], deploying
- deploying [Analysis Services], production environments
- deploying [Analysis Services - data mining]
- solutions [Analysis Services], deploying
- models [Analysis Services], data mining
ms.assetid: d83effc7-437d-42e9-8ac3-b65f79e27043
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 50cd0b4e2336b20ab12b8c5e6fda6615af03abd5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62722683"
---
# <a name="deployment-of-data-mining-solutions"></a>部署数据挖掘解决方案
  数据挖掘过程的最后一步是将模型部署到生产环境中。 部署非常重要，这是因为它使用户可以利用模型，以便执行以任何任务：  
  
-   使用这些模型创建预测并做出业务决策。 可用于创建查询工具的信息，请参阅[数据挖掘查询接口](data-mining-query-tools.md)。  
  
-   直接将数据挖掘功能嵌入到应用程序。 您可以包括分析管理对象 (AMO) 或一个包含一组对象（应用程序可使用这组对象创建、更改、处理以及删除挖掘结构和挖掘模型）的程序集。  
  
-   创建可供用户用来请求预测、查看趋势或比较模型的报表。  
  
 本节提供有关部署选项的详细信息。  
  
 [部署数据挖掘解决方案的要求](#bkmk_Reqs)  
  
 [部署关系解决方案](#bkmk_RelationalSltn)  
  
 [部署多维解决方案](#bkmk_MDSltn)  
  
 [相关资源](#bkmk_Resources)  
  
## <a name="in-this-section"></a>本节内容  
 [将数据挖掘解决方案部署到以前版本的 SQL Server](deploy-a-data-mining-solution-to-previous-versions-of-sql-server.md)  
  
 [导出和导入数据挖掘对象](export-and-import-data-mining-objects.md)  
  
##  <a name="bkmk_Reqs"></a> 部署数据挖掘解决方案的要求  
 要将解决方案部署到的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例必须在支持多维对象和数据挖掘对象的模式下运行；即，您不能将数据挖掘对象部署到承载表格模型或 PowerPivot 数据的实例。  
  
 因此，在 Visual Studio 中创建数据挖掘解决方案时，请务必使用模板 **“Analysis Services 多维和数据挖掘项目”**。  
  
 在部署解决方案时，将在与解决方案文件同名的数据库中的指定 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例中创建用于数据挖掘的对象。  
  
###  <a name="bkmk_RelationalSltn"></a> 部署关系解决方案  
 在部署关系数据挖掘解决方案时，将在新的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库中创建所需的数据挖掘对象，并且默认情况下会处理这些对象。 可以使用配置属性 **“处理选项”** 更改处理选项。 有关详细信息，请参阅[配置 Analysis Services 项目属性 (SSDT)](../multidimensional-models/configure-analysis-services-project-properties-ssdt.md)。  
  
 默认情况下，每次只部署增量更改。 换句话说，您可以修改一个挖掘模型，并且在您重新部署项目时，只会更新该挖掘模型。 但是，如果有多个客户端同时在编辑 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库，则此操作可能会导致错误。 若要更改默认部署模式，以便在部署解决方案时刷新整个数据库，请更改 **“部署模式”** 属性。  
  
 在关系数据挖掘解决方案中，必须部署的唯一对象为数据源定义、已使用的任何数据源视图、挖掘结构和所有依赖挖掘模型。  
  
###  <a name="bkmk_MDSltn"></a> 部署多维解决方案  
 在部署一个多维数据挖掘解决方案时，该解决方案将在源多维数据集所在的数据库中创建数据挖掘对象。  
  
 在处理挖掘结构或挖掘模型时，您还必须处理源多维数据集。 为此，部署使用 OLAP 挖掘模型的解决方案所需的时间将多于部署关系数据挖掘解决方案所需的时间。  
  
 一般情况下，数据挖掘对象还使用对多维数据集使用的数据源和数据源视图。 不过，您可以添加专门用于数据挖掘的数据源和数据源视图。 例如，一般情况下，多维数据集将不会包含有关潜在客户端的数据，或多维对象中未使用的外部数据。  
  
##  <a name="bkmk_Resources"></a> 相关资源  
 [移动数据挖掘对象](moving-data-mining-objects.md)  
  
 如果模型仅基于关系数据，则使用 DMX 导出和导入对象是移动对象的最简单方式。  
  
 [移动 Analysis Services 数据库](../multidimensional-models/move-an-analysis-services-database.md)  
  
 当模型将多维数据集用作数据源时，请参考本主题以了解有关如何移动模型及其支持的多维数据集数据的详细信息。  
  
 [部署 Analysis Services 项目 (SSDT)](../multidimensional-models/deploy-analysis-services-projects-ssdt.md)  
  
 提供有关部署 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目的常规信息，并介绍可作为项目配置的一部分设置的属性。  
  
## <a name="see-also"></a>请参阅  
 [多维模型对象处理](../multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [数据挖掘查询接口](data-mining-query-tools.md)   
 [处理要求和注意事项（数据挖掘）](processing-requirements-and-considerations-data-mining.md)  
  
  
