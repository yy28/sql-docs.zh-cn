---
title: "数据挖掘解决方案的相关项目 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: dc26489a-4c27-4b89-8215-6d245427c350
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 9376a1f4124a86fa7acc313c7985d0a7f1c450f3
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="related-projects-for-data-mining-solutions"></a>数据挖掘解决方案的相关项目
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]所需要的数据挖掘解决方案的最低要求是数据挖掘项目中，定义数据源、 数据源视图、 挖掘结构和挖掘模型。 但是，在使用数据挖掘模型做出日常决策时，将数据挖掘与预测分析解决方案的其他部分集成非常重要，其中可包含以下过程和组成部分：  
  
-   准备和选择数据和变量。 这一过程包括数据清除、元数据管理和多个数据源的集成，以及数据的转换、合并和数据到数据仓库的上载。  
  
-   报告分析、呈现预测和审核/跟踪数据挖掘活动。  
  
-   使用多维模型或表格模型浏览发现的内容。  
  
-   优化数据挖掘解决方案以支持新数据或根据当前分析在支持基础结构中进行的更改。  
  
 本主题介绍了 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的其他功能，这些功能通常是预测分析解决方案的一部分，用于支持数据准备和数据挖掘过程，或用于通过提供分析和操作工具为用户提供支持。  
  
 [Integration Services](#bkmk_SSIS)  
  
 [Reporting Services](#bkmk_SSRS)  
  
 [Data Quality Service](#bkmk_DQSetc)  
  
 [全文搜索](#bkmk_FTSetc)  
  
 [语义索引](#bkmk_SemSearch)  
  
##  <a name="bkmk_SSIS"></a> SQL Server Integration Services  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供数据挖掘项目的数据准备和定型阶段所需的组件和功能。 虽然您可使用其他工具（如脚本）执行很多数据清除或准备任务，但 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 在数据挖掘方面具有众多优势：  
  
-   将任务表示为工作流的一部分，可对其进行重复、自动化、分支或扩展。  
  
-   为审核提供了广泛支持，还为捕获错误和记录事件提供了多种方式。  
  
     除了捕获数据沿袭，还可通过数据转换管道监视数据的更改。  
  
     还可将 SSIS 工作流与支持变更数据捕获功能的 SQL Server 功能集成。  
  
-   可将数据挖掘合并到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 工作流中，以将传入数据合理地分离到多个表中。 例如，您可使用预测查询将新客户拆分为不同的组以在邮递活动中设定目标。  
  
 以下列表提供了指向 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 组件的链接，这些组件广泛用于支持数据挖掘。  
  
 **控制流组件**  
  
-   [Analysis Services 执行 DDL 任务](../../integration-services/control-flow/analysis-services-execute-ddl-task.md)  
  
-   [Analysis Services 处理任务](../../integration-services/control-flow/analysis-services-processing-task.md)  
  
-   [CDC 控制任务](../../integration-services/control-flow/cdc-control-task.md)  
  
-   [数据清理](../../data-quality-services/data-cleansing.md)  
  
-   [数据挖掘查询任务](../../integration-services/control-flow/data-mining-query-task.md)  
  
-   [数据事件探查任务](../../integration-services/control-flow/data-profiling-task.md)  
  
 **数据流组件**  
  
-   [CDC 流组件](../../integration-services/data-flow/cdc-flow-components.md)  
  
-   [有条件拆分转换](../../integration-services/data-flow/transformations/conditional-split-transformation.md)  
  
-   [数据转换](../../integration-services/data-flow/transformations/data-conversion-transformation.md)  
  
-   [数据挖掘模型定型目标](../../integration-services/data-flow/data-mining-model-training-destination.md)  
  
-   [数据挖掘查询转换](../../integration-services/data-flow/transformations/data-mining-query-transformation.md)  
  
-   [派生列转换](../../integration-services/data-flow/transformations/derived-column-transformation.md)  
  
-   [百分比抽样转换](../../integration-services/data-flow/transformations/percentage-sampling-transformation.md)  
  
-   [字词提取转换](../../integration-services/data-flow/transformations/term-extraction-transformation.md)  
  
-   [字词查找转换](../../integration-services/data-flow/transformations/term-lookup-transformation.md)  
  
##  <a name="bkmk_SSRS"></a> SQL Server Reporting Services  
 虽然 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 通常不会被视为数据挖掘解决方案的重要组件，但它提供的以下功能对演示数据挖掘解决方案很有用。  
  
-   在复杂报表中集成来自多个源的数据。 为分析人员创建对模型内容的查询，并创建为最终用户显示预测和趋势的报表。  
  
-   用于创建可让用户直接对现有挖掘模型进行查询的报表的功能。  
  
-   与 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]集成，以支持对从 OLAP 模型创建的数据挖掘维度和数据挖掘多维数据集的钻取和浏览。  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中可用的参数化和格式化功能。  
  
 有关如何将 Reporting Services 作为数据源与 DMX 查询一起使用的详细信息，请参阅以下链接：  
  
 [从数据挖掘模型检索数据 (DMX) (SSRS)](../../reporting-services/report-data/retrieve-data-from-a-data-mining-model-dmx-ssrs.md)  
  
 [Analysis Services DMX 查询设计器用户界面](../../reporting-services/report-data/analysis-services-dmx-query-designer-user-interface.md)  
  
 [针对 DMX 的 Analysis Services 连接类型 (SSRS)](../../reporting-services/report-data/analysis-services-connection-type-for-dmx-ssrs.md)  
  
 但是，不需要将 DMX 用作数据源。 用于数据挖掘的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 组件还支持将预测查询的结果保存到关系数据库中。 如果已建立用于使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]更新模型的工作流，则将预测和其他数据挖掘查询结果保存到 SQL Server 可使您能够使用 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 进行报告，并能使用其他不与 DMX 建立接口连接的工具。  
  
 有关将 Reporting Services 用作数据源的表示层的详细信息，请参阅 [Integrating Reporting Services into Applications](../../reporting-services/application-integration/integrating-reporting-services-into-applications.md)。  
  
##  <a name="bkmk_DQSetc"></a> Data Quality Services  
 Data Quality Services (DQS) 是 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]的新增功能。 由于数据问题会导致无法进行数据挖掘，因此执行重复分析或在具有复杂数据源的大型组织中工作的数据挖掘人员应会发现，使用 DQS 的规划良好的数据项目是一种支持数据挖掘的解决方案，它比使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 或其他脚本的即席数据清除更为可靠。  
  
 应考虑将以下 DQS 功能用于数据挖掘解决方案中的数据准备和数据集成。  
  
 **计算机辅助的数据清除过程，该过程可分析源数据并提出更改建议。**  
 DQS 会将源数据与数据质量提供程序维护和保护的基于云的引用数据进行比较。  
  
 DQS 还会分析原始源数据并从用户数据中创建知识库。 将对处理后的数据进行分类，然后向用户显示以供进一步处理。 清除过程是交互式的，意味着数据专员可批准、拒绝或修改计算机辅助的数据清除过程建议的数据。  
  
 可通过此过程获得一个知识库，可以持续改进该知识库或在多个数据增强阶段中重复使用它。  
  
 有关详细信息，请参阅 [Data Cleansing](../../data-quality-services/data-cleansing.md)。  
  
 **计算机辅助的匹配过程，该过程可分析源数据并提出更改建议。**  
 若要防止数据重复，您可对数据源执行额外清除，以标识精确匹配项和近似匹配项。 利用这些组件，您可指定匹配规则和应用规则的阈值。  
  
 通过查找数据匹配项，您可删除重复项，从而解决这一数据挖掘问题。 消除数据重复不会自动进行；数据专员和 IT 专业人员必须对知识库中的知识和要对数据进行的更改进行验证。  
  
 创建初始 DQS 项目之后，可使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 组件实现许多任务的自动化。  
  
 有关详细信息，请参阅 [Data Matching](../../data-quality-services/data-matching.md)。  
  
 在数据质量项目中执行清除和匹配活动时，可获得与 DQS 处理的数据有关的实时统计信息和其他信息。 数据事件探查可帮助您评估数据清除或数据匹配在多大程度上帮助提高数据质量，并理解已做的更改。 有关数据事件探查和通知的信息，请参阅 [Data Profiling and Notifications in DQS](../../data-quality-services/data-profiling-and-notifications-in-dqs.md)。  
  
 **一个表示以下三种类型的知识的知识库：现有知识、DQS 服务器生成的知识和用户生成的知识。**  
 创建知识库之后，您可使用它反复清除和验证其他数据。  
  
 您可将来自多个源的新数据导入知识库中，这些数据是来自引用提供程序的已知干净数据，或与知识库中现有数据匹配的原始数据。  
  
 有关数据质量项目中的清除活动的详细信息，请参阅数据清除 (DQS)。  
  
 还可将知识库中的知识应用于其他源，以在其他进程中执行数据清除。 此类数据清除可帮助标识用户输入错误、传输或存储过程中的数据损坏或不匹配的数据字典定义。  
  
 有关详细信息，请参阅 [DQS Knowledge Bases and Domains](../../data-quality-services/dqs-knowledge-bases-and-domains.md)。  
  
##  <a name="bkmk_FTSetc"></a> 全文搜索  
 SQL Server 中的全文搜索为应用程序和用户提供了对 SQL Server 表中基于字符的数据运行全文查询的功能。 启用全文搜索后，可对由有关多种形式的词或短语的语言特定的规则增强的文本数据执行搜索。 还可配置搜索条件（如多个字词之间的距离），使用函数约束按可能性顺序返回的结果。  
  
 由于全文查询是 SQL Server 引擎所提供的一项功能，因此，您可对文本数据源使用全文搜索来创建参数化查询、生成自定义数据集或字词向量，并在数据挖掘中使用这些源。  
  
 有关如何将全文查询用于全文检索的详细信息，请参阅 [使用全文搜索查询](../../relational-databases/search/query-with-full-text-search.md)。  
  
 使用 SQL Server 全文搜索功能的好处是，您可利用所有 SQL Server 语言附带的断字符和词干分析器中包含的语言智能。 通过使用提供的断字符和词干分析器，您可确保使用适用于每种语言的字符分隔字词，并且不会忽略基于标注字符或拼字变体（如日语中的多种数字格式）的同义词。  
  
 除了控制词边界的语言智能之外，每种语言的词干分析器还可基于对应语言中的语态和拼字变体规则的知识，将词的变体减少至单个字词。 每种语言的语言分析规则各不相同，这些规则是根据对实际公司所做的大量调研来制定的。  
  
 有关详细信息，请参阅 [配置和管理断字符和词干分析器以便搜索](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)。  
  
 全文检索后存储的词的版本是一个压缩格式的标记。 对全文检索进行的后续查询将基于相应的语言规则生成特定词的多种变形形式，以确保生成所有可能的匹配项。 例如，即使存储的标记可能为“run”，查询引擎也会查询词“running”、“ran”和“runner”，因为这些词都是根词“run”正常派生的语形学变体。  
  
 还可以创建和生成用户同义词库以存储同义词并获得更佳搜索结果，或对字词进行分类。 通过开发针对全文数据定制的同义词库，您可以有效地扩大对这些数据的全文查询的范围。 有关详细信息，请参阅 [为全文搜索配置和管理同义词库文件](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md)。  
  
 使用全文搜索的要求包括：  
  
-   数据库管理员必须对表创建全文检索。  
  
-   每个表只允许有一个全文索引。  
  
-   您为其编制索引的每个列均必须有一个唯一键。  
  
-   仅包含以下数据类型的列支持全文检索：char、varchar、nchar、nvarchar、text、ntext、image、xml、varbinary 和 varbinary(max)。 如果列为 varbinary、varbinary(max)、image 或 xml，则您必须在单独的类型列中指定可编制索引的文档的文件扩展名（.doc、.pdf、.xls 等）。  
  
##  <a name="bkmk_SemSearch"></a> 语义索引  
 语义搜索以 SQL Server 中现有的全文搜索功能为基础，但使用其他功能和统计信息来启用方案（如相关文档的自动关键字提取和发现）。 例如，您可以使用语义搜索来建立一个组织的基本分类，或对文档集进行分类。 您也可在聚类分析或决策树模型中将提取的字词和文档相似性得分组合使用。  
  
 在成功启用语义搜索并为数据列编制索引后，您可将本机提供的函数与语义索引一起使用来执行以下操作：  
  
-   返回单个词关键短语及其得分。  
  
-   返回包含指定的关键词短语的文档。  
  
-   返回相似性得分和影响得分的词语。  
  
 有关详细信息，请参阅 [使用语义搜索在文档中查找关键短语](../../relational-databases/search/find-key-phrases-in-documents-with-semantic-search.md) 和 [使用语义搜索查找相似和相关文档](../../relational-databases/search/find-similar-and-related-documents-with-semantic-search.md)。  
  
 有关支持语义索引的数据库对象的详细信息，请参阅 [对表和列启用语义搜索](../../relational-databases/search/enable-semantic-search-on-tables-and-columns.md)。  
  
 使用语义搜索的要求包括：  
  
-   同时启用全文搜索。  
  
-   安装语义搜索组件还会创建特殊系统数据库，不能重命名、更改或替换该数据库。  
  
-   使用该服务编制索引的文档必须存储到 SQL Server 上的支持全文检索（包括表和索引视图）的任何数据库对象中。  
  
-   不是所有的全文语言都支持语义索引。 有关支持的语言的列表，请参阅 [sys.fulltext_semantic_languages (Transact-SQL)](../../relational-databases/system-catalog-views/sys-fulltext-semantic-languages-transact-sql.md)。  
  
## <a name="see-also"></a>另请参阅  
 [多维模型解决方案 (SSAS)](../../analysis-services/multidimensional-models/multidimensional-model-solutions-ssas.md)   
 [表格模型解决方案（SSAS 表格）](../../analysis-services/tabular-models/tabular-model-solutions-ssas-tabular.md)  
  
  
