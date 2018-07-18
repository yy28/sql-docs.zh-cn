---
title: 自动执行 Analysis Services Administrative Tasks with SSIS |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c750c0e8ee9f13c4b4751af872b02f4ed9ee419a
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34015644"
---
# <a name="automate-analysis-services-administrative-tasks-with-ssis"></a>使用 SSIS 自动执行 Analysis Services 管理任务
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]使你能够自动执行 DDL 脚本、 多维数据集和挖掘模型处理任务，以及数据挖掘查询任务。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 可被视为控制流和维护任务（这些任务可链接起来以形成顺序和并行执行的数据处理作业）的集合。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 用于在数据处理任务期间执行清除操作并将数据从不同的数据源集合到一起。 使用多维数据集和挖掘模型时， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 可以将非数值数据转换为数值数据，并且可以确保数据值处于期望的范围内，如此便创建了用来填充事实数据表和维度的干净数据。  
  
## <a name="integration-services-tasks"></a>Integration Services 任务  
 任何 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 任务或作业都有两个主要元素：控制流元素和数据流元素。 控制流元素通过应用优先约束来定义作业进行的逻辑顺序。 数据流元素则考虑一个组件的输出和下一个组件的输入之间的接续性，以及其间可能对数据执行的任何数据转换。 为了对数据的流向作出决策，优先约束包含了用来指定哪个组件接收输出的逻辑。 与 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 任务包括执行 DDL 任务、Analysis Services 处理任务和数据挖掘查询任务。 对于这些任务中的每一个，都可以使用发送邮件任务向管理员发送一个包含任务结果的电子邮件。  
  
## <a name="the-execute-ddl-task"></a>执行 DDL 任务  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中的执行 DDL 任务允许您直接将 DDL 脚本发送到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务器并自动运行这些脚本。 这就使得 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 管理员可以在一个 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包内执行备份、还原或同步操作。 包由前面所介绍的控制和数据流元素组成，这些元素必须是 **run regularly**的，其他可以添加到任务中的 DDL 语句也是如此。 因为此处讨论的任务通常在夜间运行，所以使用可从任何计划应用程序方便地运行的包尤其有用。 可以使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 代理在任何时间调度要运行的包。 有关如何执行此任务的详细信息，请参阅 [Analysis Services 执行 DDL 任务](../../integration-services/control-flow/analysis-services-execute-ddl-task.md)。  
  
## <a name="analysis-services-processing-task"></a>Analysis Services 处理任务  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中的 Analysis Services 处理任务可以在源关系数据库进行定期更新时使用新信息自动填充多维数据集。 可以使用 Analysis Services 处理任务对维度、多维数据集或分区进行处理。 处理本身可以为 **incremental** 或 **full**类型，您可以根据作业要求来选择类型。 增量处理将添加新数据并执行足够的重新计算以保持目标最新，而完全处理则删除现有的数据以进行完全重新加载和重新计算。 完全处理需要更多时间，但处理得更彻底。 有关如何执行此任务的详细信息，请参阅 [Analysis Services Processing Task](../../integration-services/control-flow/analysis-services-processing-task.md)。  
  
## <a name="data-mining-query-task"></a>数据挖掘查询任务  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中的数据挖掘查询任务允许您提取和存储来自挖掘模型的信息。 该信息通常存储在一个关系数据库中并且可用于特定的用途，例如，用于找出目标市场活动的一组潜在客户。 数据挖掘可以标识客户的值和客户响应特定市场推销的概率。 您可以使用数据挖掘查询任务提取数据并将数据修改为您偏爱的格式。 有关如何执行此任务的详细信息，请参阅 [Data Mining Query Task](../../integration-services/control-flow/data-mining-query-task.md)。  
  
## <a name="see-also"></a>另请参阅  
 [分区处理目标](../../integration-services/data-flow/partition-processing-destination.md)   
 [维度处理目标](../../integration-services/data-flow/dimension-processing-destination.md)   
 [数据挖掘查询转换](../../integration-services/data-flow/transformations/data-mining-query-transformation.md)   
 [处理多维模型 (Analysis Services)](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
  
  
