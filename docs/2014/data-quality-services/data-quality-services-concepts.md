---
title: Data Quality Services 概念 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 837c71ee-48fa-4044-8744-2be9119aaa04
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: b1f6eb37de996e8956468efb54fa74535e419f44
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36138722"
---
# <a name="data-quality-services-concepts"></a>Data Quality Services 概念
  本文简要概括知识管理、数据质量项目和数据质量管理中的 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 概念。  
  
##  <a name="Knowledge"></a> 知识管理概念  
 DQS 知识库是一种元数据存储库，它由数据专员或 IT 专业人员创建，旨在通过数据清理或数据匹配提高数据质量。 DQS 知识管理包括用于在计算机辅助方式和交互式方式中创建和管理知识库的过程。  
  
 **知识发现**  
  
 知识发现是分析您组织的数据样本以建立有关数据的知识的计算机辅助过程。 一旦得到了分析结果，您就可以验证并改进知识，然后应用知识来执行数据清理、数据匹配和事件探查。 有关详细信息，请参阅 [DQS Knowledge Bases and Domains](../../2014/data-quality-services/dqs-knowledge-bases-and-domains.md)。  
  
 **域管理**  
  
 通过域管理过程，您可以更改或增加由知识发现过程生成的知识。 您可以通过交互方式编辑、更新和查看知识库中的知识。 知识库由数据域构成，这些数据域包含域值及其状态、域规则、基于字词的关系以及引用数据。 在域管理中，您可以更改域属性、将引用数据附加到域、管理域规则、管理域值并输入数据关系以及创建、删除、导入或导出域。 还可以使用聚合多个单一域的复合域。 有关详细信息，请参阅 [DQS Knowledge Bases and Domains](../../2014/data-quality-services/dqs-knowledge-bases-and-domains.md)。  
  
 **匹配策略**  
  
 匹配策略包含用于消除数据重复的匹配规则。 通过匹配策略过程，您可以创建匹配规则、基于匹配结果和事件探查数据优化规则，并将策略添加到知识库。 有关详细信息，请参阅 [Data Matching](../../2014/data-quality-services/data-matching.md)。  
  
 **Reference Data Services**  
  
 可以使用引用数据来验证、更正和丰富您的数据，同时利用可保证其引用数据质量的公司所提供的服务。 您可以使用 Microsoft Azure 市场的服务连接到引用数据提供程序，也可以直接连接到提供程序。 有关详细信息，请参阅 [Reference Data Services in DQS](../../2014/data-quality-services/reference-data-services-in-dqs.md)。  
  
 有关 DQS 中的知识管理的详细信息，请参阅[DQS 知识库和域](../../2014/data-quality-services/dqs-knowledge-bases-and-domains.md)。  
  
##  <a name="Projects"></a> 数据质量项目概念  
 数据专员在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 应用程序中使用数据质量项目来执行数据质量操作（清理和匹配）。  
  
 **数据清理**  
  
 DQS 中的数据清理需要根据 DQS 知识库中的知识来执行。 DQS 中的数据清理是一个两步过程：  
  
-   **计算机辅助清理**：DQS 对清理项目使用所选知识库中的知识，用来对数据源中的值提出更正/建议。  
  
-   **交互式清理**：数据专员可以执行交互式清理过程，以更改或增强由计算机辅助数据清理过程提出的数据更正。 为此，数据专员将使用由数据清理过程确定的置信度和统计信息，或在项目中手动输入自己的更改。  
  
 完成数据清理后，数据专员可以将已处理的数据导出到 SQL Server 数据库、.csv 文件或 Excel 文件。 有关详细信息，请参阅 [Data Cleansing](../../2014/data-quality-services/data-cleansing.md)。  
  
 **数据匹配**  
  
 借助匹配过程，数据专员可以比较数据，以便通过消除重复过程整理类似但稍有不同的数据。 DQS 基于知识库中包含的匹配规则执行消除重复操作；数据专员从数据质量项目中为匹配过程指定参数。 有关详细信息，请参阅 [Data Matching](../../2014/data-quality-services/data-matching.md)。  
  
 **事件探查和通知**  
  
 数据事件探查可为数据专员提供有关正由 DQS 处理的数据的实时统计信息和其他信息，可帮助在运行数据质量项目期间执行清理和匹配活动。 数据事件探查可帮助您评估数据质量项目中的清理或匹配活动的有效性，并且提供通知，帮助用户采取措施来改善数据清理和数据匹配活动。 有关详细信息，请参阅[Data Profiling and Notifications in DQS](../../2014/data-quality-services/data-profiling-and-notifications-in-dqs.md)。  
  
 有关 DQS 中的数据质量项目的详细信息，请参阅[数据质量项目 (DQS)](../../2014/data-quality-services/data-quality-projects-dqs.md)。  
  
##  <a name="Admin"></a> 数据质量管理概念  
 DQS 管理员可以使用 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 应用程序执行各种管理任务。  
  
 **活动监视**  
  
 活动监视可显示在数据范围内执行的每个活动的状态，提供每个活动的数据，并使 DQS 管理员能够控制活动。 有关详细信息，请参阅[Monitor DQS Activities](../../2014/data-quality-services/monitor-dqs-activities.md)。  
  
 **Configuration**  
  
 配置选项支持您：  
  
-   配置引用数据服务设置。 有关详细信息，请参阅[Configure DQS to Use Reference Data](../../2014/data-quality-services/configure-dqs-to-use-reference-data.md)。  
  
-   设置清理和匹配活动的阈值。 有关详细信息，请参阅 [配置清理和匹配活动的阈值](../../2014/data-quality-services/configure-threshold-values-for-cleansing-and-matching.md)。  
  
-   启用/禁用事件探查通知。 有关详细信息，请参阅[在 DQS 中启用或禁用事件探查通知](../../2014/data-quality-services/enable-or-disable-profiling-notifications-in-dqs.md)。  
  
-   在基于活动的级别或基于更高级模块的级别配置 DQS 日志文件的严重性级别。 有关详细信息，请参阅[Configure Severity Levels for DQS Log Files](../../2014/data-quality-services/configure-severity-levels-for-dqs-log-files.md)。  
  
 **DQS 安全性**  
  
 您可以使用 SQL Server 安全机制中的角色来确保 DQS 安全。 有三种 DQS 角色决定 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 应用程序中用户的访问级别：dqs_administrator、dqs_kb_editor 和 dqs_kb_operator。 您不能使用 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 应用程序向用户授予角色；角色是通过 SQL Server Management Studio 授予的。 有关详细信息，请参阅[DQS Security](../../2014/data-quality-services/dqs-security.md)。  
  
 有关 DQS 管理的详细信息，请参阅[DQS 管理](../../2014/data-quality-services/dqs-administration.md)。  
  
## <a name="see-also"></a>请参阅  
 [Data Quality Services](../../2014/data-quality-services/data-quality-services.md)  
  
  