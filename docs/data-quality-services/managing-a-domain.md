---
title: "管理域 | Microsoft Docs"
ms.custom: ""
ms.date: "07/31/2012"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "data-quality-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c5ab71a3-0dac-45b1-be8e-93bf7e0e03ce
caps.latest.revision: 13
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 13
---
# 管理域
  本主题介绍如何在 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 中使用域。 域包含要分析的数据源的特定字段中数据的语义表示。 域是您为数据源创建的知识库的一部分，并且，通过分析样本数据源或导入数据而逐步建立的知识将添加到在该知识库中定义的域。 这些域中的知识随后用于在数据质量项目中执行清除和匹配。 域是 Data Quality Services 中所有活动的核心。  
  
 域映射到数据源字段，并在知识发现、域管理和匹配活动中进行填充。 如何从数据源加载数据以及如何在报表中输出数据是在域属性中定义的。 当您使用引用数据提供程序清理数据时，您会将引用数据服务附加到单一域或复合域。 创建要应用于域中数据的规则，并且可以为域创建基于字词的关系。 您可以查看并更正域中的数据。  
  
 还可以创建复合域，该域包含两个或更多单一域，而每个单一域包含有关共用数据的知识。 有关详细信息，请参阅 [管理复合域](../data-quality-services/managing-a-composite-domain.md)。  
  
## 域属性  
 当您创建域时，您具有以下有关如何从源数据填充域以及如何输出域值的选项。 有关详细信息，请参阅 [Set Domain Properties](../data-quality-services/set-domain-properties.md)。  
  
-   选择您用来填充域的数据的类型。 有关每个域数据类型的支持的数据类型的信息，请参阅 [Supported SQL Server and SSIS Data Types for DQS Domains](../data-quality-services/supported-sql-server-and-ssis-data-types-for-dqs-domains.md)。  
  
-   指定仅从域中输出前导值，而不输出它们的同义词。  
  
-   指定使用特定的格式输出域值，具体取决于数据类型。  
  
-   如果数据类型为字符串，则可以通过在将该字符串从数据源加载到域时删除特殊字符来规范化该字符串。  
  
-   如果数据类型为字符串，您可以运行 DQS 拼写检查器检查字符串值的语法、拼写和句子结构，并在 **“域管理”** 的 **“域值”**页中指示可能存在的错误。 这包括指定运行拼写检查器的语言。  
  
-   如果数据类型是字符串，当您知道字符串中不会出现语法错误时，您可以指定 DQS 不标识语法错误。  
  
## 本节内容  
 通过使用域，您可以执行以下操作：  
  
|||  
|-|-|  
|为具有特定数据类型的数据字段创建语义表示，指定如何填充域以及如何设置域的输出格式|[创建域](../data-quality-services/create-a-domain.md)|  
|将某个域链接到另一个域，使其能够共享相同的设置和值|[创建链接域](../data-quality-services/create-a-linked-domain.md)|  
|将引用数据服务附加到单一域或复合域|[将域或复合域附加到引用数据](../data-quality-services/attach-domain-or-composite-domain-to-reference-data.md)|  
|更改或增加知识库中的值|[更改域值](../data-quality-services/change-domain-values.md)|  
|使用验证和标准化规则|[创建域规则](../data-quality-services/create-a-domain-rule.md)|  
|使用关系更正作为域中值的一部分的字词|[创建基于字词的关系](../data-quality-services/create-term-based-relations.md)|  
|完成、关闭或取消域管理活动|[结束域管理活动](../Topic/End%20the%20Domain%20Management%20Activity.md)|  
  
## 相关任务  
  
|任务说明|主题|  
|----------------------|-----------|  
|通过运行知识发现并以交互方式管理知识来生成知识库|[生成知识库](../data-quality-services/building-a-knowledge-base.md)|  
|将知识导入知识库，或从知识库中导出知识。|[导入和导出知识](../data-quality-services/importing-and-exporting-knowledge.md)|  
|创建一个复合域，并将知识添加到该域中。|[管理复合域](../data-quality-services/managing-a-composite-domain.md)|  
  
  