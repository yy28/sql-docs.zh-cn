---
title: 将知识添加到知识库 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: da148a7f-55bc-4990-a157-e61968b831d7
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: c0cbd22ac2de86b068990f9cecc5385f9133e482
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84938058"
---
# <a name="adding-knowledge-to-a-knowledge-base"></a>将知识添加到知识库
  本主题介绍可在 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 中将知识添加到知识库的方法。 您必须具备有关数据的知识才可以执行数据质量操作。 您可以通过生成和维护数据质量知识库，并向知识库添加与特定类型的数据源相关的知识，以获得知识。 知识库是有关数据的知识的存储库，通过它您可以了解自己的数据并维护其完整性。  
  
 知识库包含与数据源相关的数据域。 对于每个数据域，DQKB 存储所有标识的字词、拼写错误、验证和业务规则，以及可用于对数据源执行数据质量操作的引用数据。 DQS 使用该知识来标识不正确或无效的数据，或执行匹配。  
  
 您可以采用以下计算机辅助方法或交互式方法将知识添加到知识库。  
  
-   [执行知识发现](#Discovery)  
  
-   [管理域中的数据值](#ManageDomain)  
  
-   [从 .dqs 文件导入知识](#DQSFile)  
  
-   [从 Excel 文件导入知识](#Excel)  
  
-   [将知识从项目导入回知识库](#Project)  
  
-   [使用默认 DQS 知识库](#Default)  
  
##  <a name="perform-knowledge-discovery"></a><a name="Discovery"></a>执行知识发现  
 知识发现将分析数据样本以确定是否满足数据质量标准，然后将获得的知识添加到知识库中。 这是一个计算机辅助过程，用于标识数据不一致和语法错误，随后提出数据更改建议。 知识发现活动是一个向导，其中包括可以按交互方式管理域值的页面。  
  
-   有关文档的详细信息，请参阅 [Perform Knowledge Discovery](../../2014/data-quality-services/perform-knowledge-discovery.md)。  
  
-   有关演示如何执行知识发现的视频，请单击 [此处](https://msdn.microsoft.com/sqlserver/hh323825.aspx)。  
  
##  <a name="manage-data-values-in-a-domain"></a><a name="ManageDomain"></a>管理域中的数据值  
 通过 DQS 可以按交互方式更改和增加由计算机辅助知识发现活动生成的元数据。 在域管理活动中执行此操作，从中您可以向特定数据值应用更改。  
  
-   有关文档的详细信息，请参阅 [Change Domain Values](../../2014/data-quality-services/change-domain-values.md)。  
  
-   有关演示如何执行域管理的视频，请单击 [此处](https://msdn.microsoft.com/sqlserver/hh323825.aspx)。 请注意，在此视频中，您将在知识发现向导的“管理域值”页中更改域值。 还可以在域管理活动的“域值”页中执行这些步骤。  
  
##  <a name="import-knowledge-from-a-dqs-file"></a><a name="DQSFile"></a>从 dqs 文件导入知识  
 可以将域从 .dqs 数据文件导入到现有知识库，也可以将整个知识库从 .dqs 导入到新的知识库。 为此，您首先需要将现有域或知识库导出到 .dqs 文件。 包含域的 dqs 文件包含所有域数据；包含知识库的 .dqs 文件将包含所有知识库信息，其中包括域和匹配策略。  
  
-   有关文档的详细信息，请参阅[从 .dqs 文件导入域](../../2014/data-quality-services/import-a-domain-from-a-dqs-file.md)或[从 .dqs 文件导入知识库](../../2014/data-quality-services/import-a-knowledge-base-from-a-dqs-file.md)。  
  
##  <a name="import-knowledge-from-an-excel-file"></a><a name="Excel"></a>从 Excel 文件导入知识  
 您可以将域值从 Excel 电子表格文件导入到现有域或知识库。 为此，您必须首先创建一个容纳要导入的域值的 Excel 电子表格，并确保 Excel 安装在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 计算机上，以便您能够使用 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]导入值。 您不能将域值从域或知识库中导出到 Excel 文件。  
  
-   有关文档的详细信息，请参阅[将值从 Excel 文件导入到域](../../2014/data-quality-services/import-values-from-an-excel-file-into-a-domain.md)或[在知识发现中从 Excel 文件中导入域](../../2014/data-quality-services/import-domains-from-an-excel-file-in-knowledge-discovery.md)。  
  
##  <a name="import-knowledge-from-a-project-back-into-the-knowledge-base"></a><a name="Project"></a>将知识从项目导入回知识库  
 在使用知识库运行清理或匹配数据质量项目之后，可以将在清理或匹配过程中创建的知识导入回该知识库。 这样，您就可以保留在项目过程中生成的知识，并在知识库中不断地生成知识。  
  
-   有关文档的详细信息，请参阅[将清理项目值导入到域中](../../2014/data-quality-services/import-cleansing-project-values-into-a-domain.md)。  
  
##  <a name="use-the-default-dqs-knowledge-base"></a><a name="Default"></a>使用默认 DQS 知识库  
 DQS 附带一个预生成的知识库（称为 DQS 数据），其中包含针对美国公司和地址数据的域。 可以使用此知识库快速启动项目，而无需创建新的知识库。 DQS 数据知识库是只读的，但数据专员可以基于该知识库创建新的知识库。  
  
-   有关文档的详细信息，请参阅 [Using the DQS Default Knowledge Base](../../2014/data-quality-services/using-the-dqs-default-knowledge-base.md)。  
  
  
