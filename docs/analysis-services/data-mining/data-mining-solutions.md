---
title: 数据挖掘解决方案 |Microsoft 文档
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5e52afe834120b661bd885be4e00491385b8b917
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34015164"
---
# <a name="data-mining-solutions"></a>数据挖掘解决方案
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  数据挖掘解决方案是一个包含一个或多个数据挖掘项目的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 解决方案。  
  
 本节中的主题提供了有关如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]设计和实现集成数据挖掘解决方案的信息。 有关数据挖掘设计过程和相关工具的概述，请参阅 [Data Mining Concepts](../../analysis-services/data-mining/data-mining-concepts.md)。  
  
 有关对数据挖掘有用的其他项目类型的详细信息，请参阅[数据挖掘解决方案的相关项目](../../analysis-services/data-mining/related-projects-for-data-mining-solutions.md)。  
  
 [关系 vs。多维解决方案](#bkmk_RelMD)  
  
 [部署数据挖掘解决方案](#bkmk_Deploy)  
  
 [解决方案演练](#bkmk_Walkthru)  
  
##  <a name="bkmk_RelMD"></a>关系 vs。多维解决方案  
 数据挖掘解决方案可基于多维数据（即现有多维数据集）、纯关系数据（例如，数据仓库中的表和视图）、文本文件、Excel 工作簿或其他外部数据源。  
  
-   可以在现有多维数据库解决方案中创建数据挖掘对象。  
  
     通常，如果您已创建一个多维数据集，并希望通过将该多维数据集用作数据源来执行数据挖掘，则您需要创建一个与此类似的解决方案。 当您基于一个多维数据集移动和备份模型时，该多维数据集也将被移动或复制。  
  
-   可以创建仅包含数据挖掘对象（包括支持的数据源和数据源视图）的数据挖掘解决方案和仅使用关系数据源的数据挖掘解决方案。  
  
     这是创建数据挖掘模型的首选方法，因为通常针对关系数据源的处理和查询的速度最快。 还可以使用 EXPORT 和 IMPORT 命令在服务器间轻松移动和备份模型。  
  
##  <a name="bkmk_Deploy"></a> 部署数据挖掘解决方案  
 要将解决方案部署到的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例必须在支持多维对象和数据挖掘对象的模式下运行；即，你不能将数据挖掘对象部署到承载表格模型或 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据的实例。  
  
 因此，在 Visual Studio 中创建数据挖掘解决方案时，请务必使用模板 **“Analysis Services 多维和数据挖掘项目”**。  
  
 在部署解决方案时，将在与解决方案文件同名的数据库中的指定 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例中创建用于数据挖掘的对象。  
  
 有关如何同时部署关系解决方案和多维解决方案的详细信息，请参阅 [部署数据挖掘解决方案](../../analysis-services/data-mining/deployment-of-data-mining-solutions.md)。  
  
##  <a name="bkmk_Walkthru"></a> 解决方案演练  
 概述了如何使用数据挖掘向导创建数据挖掘解决方案。  
  
 [创建关系挖掘结构](../../analysis-services/data-mining/create-a-relational-mining-structure.md)  
 从可组合到数据源视图中的关系数据、文本文件和其他源创建挖掘结构。  
  
 [创建 OLAP 挖掘结构](../../analysis-services/data-mining/create-an-olap-mining-structure.md)  
 基于 OLAP 多维数据集中的数据创建挖掘结构。 可将从 OLAP 数据创建的模型另存为数据挖掘维度，也可将数据和模型集另存为新的多维数据集。  
  
## <a name="in-this-section"></a>本节内容  
 [数据挖掘项目](../../analysis-services/data-mining/data-mining-projects.md)  
  
 [处理数据挖掘对象](../../analysis-services/data-mining/processing-data-mining-objects.md)  
  
 [数据挖掘解决方案的相关的项目](../../analysis-services/data-mining/related-projects-for-data-mining-solutions.md)  
  
 [部署数据挖掘解决方案](../../analysis-services/data-mining/deployment-of-data-mining-solutions.md)  
  
## <a name="related-tasks-and-topics"></a>相关任务和主题  
 在创建一个基本数据挖掘解决方案（包括数据源和挖掘结构）后，可通过添加新模型、测试并比较模型、创建预测和试用数据子集来基于该解决方案进行生成。  
  
 有关更多信息，请参见下列链接：  
  
|“任务”|主题|  
|-----------|------------|  
|测试您创建的模型，验证定型数据的质量并创建代表数据挖掘模型的准确性的图表。|[测试和验证 & #40; 数据挖掘 & #41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md)|  
|通过用数据填充结构及相关模型来定型模型。 使用新数据更新和扩展模型。|[处理数据挖掘对象](../../analysis-services/data-mining/processing-data-mining-objects.md)|  
|通过对定型数据应用筛选器、选择其他算法或设置高级算法参数来自定义挖掘模型。|[自定义挖掘模型和结构](../../analysis-services/data-mining/customize-mining-models-and-structure.md)|  
|通过对在定型模式下使用的数据应用筛选器来自定义挖掘模型。|[将挖掘模型添加到结构 & #40;Analysis Services-数据挖掘 & #41;](../../analysis-services/data-mining/add-mining-models-to-a-structure-analysis-services-data-mining.md)|  
|更新和管理数据挖掘解决方案。|链接 TBD|  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘教程 & #40;Analysis Services & #41;](../../analysis-services/data-mining-tutorials-analysis-services.md)  
  
  
