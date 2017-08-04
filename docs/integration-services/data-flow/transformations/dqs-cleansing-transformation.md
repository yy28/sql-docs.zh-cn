---
title: "DQS 清理转换 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data correction
- correct data
ms.assetid: d2ec1b1a-c745-4741-b57c-6fdb524a154c
caps.latest.revision: 35
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2851f1310e241dd921e0777408e000eb37836a81
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="dqs-cleansing-transformation"></a>DQS 清除转换
  DQS 清除转换使用 Data Quality Services (DQS)，通过应用为连接的数据源或类似数据源创建的已批准规则来更正来自连接的数据源的数据。 有关数据更正规则的详细信息，请参阅 [DQS Knowledge Bases and Domains](../../../data-quality-services/dqs-knowledge-bases-and-domains.md)。 有关 DQS 的详细信息，请参阅 [Data Quality Services Concepts](../../../data-quality-services/data-quality-services-concepts.md)。  
  
 为了确定是否必须更正数据，DQS 清除转换在满足以下条件时处理输入列中的数据：  
  
-   该列已选定用于数据更正。  
  
-   数据更正支持该列数据类型。  
  
-   该列映射到的域具有兼容数据类型。  
  
 该转换还包括您配置为处理行级错误的错误输出。 若要配置错误输出，请使用 **“DQS 清理转换编辑器”**。  
  
 您可以在数据流中包含 [Fuzzy Grouping Transformation](../../../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md) 来标识可能为重复项的数据行。  
  
## <a name="data-quality-projects-and-values"></a>数据质量项目和值  
 使用 DQS 清理转换处理数据时，会在数据质量服务器上创建一个清理项目。 使用数据质量客户端管理项目。 此外，您还可以使用数据质量客户端将项目值导入 DQS 知识库域。 只能将值导入配置为使用 DQS 清理转换的域（或链接域）。  
  
## <a name="related-tasks"></a>相关任务  
  
-   [在数据质量客户端中打开 Integration Services 项目](../../../data-quality-services/open-integration-services-projects-in-data-quality-client.md)  
  
-   [将清理项目值导入到域中](../../../data-quality-services/import-cleansing-project-values-into-a-domain.md)  
  
-   [将数据质量规则应用于数据源](../../../integration-services/data-flow/transformations/apply-data-quality-rules-to-data-source.md)  
  
## <a name="related-content"></a>相关内容  
  
-   [打开、解锁、重命名和删除数据质量项目](https://msdn.microsoft.com/library/hh510417.aspx)  
  
-   social.technet.microsoft.com 上的文章： [使用复合域清理复杂数据](http://social.technet.microsoft.com/wiki/contents/articles/13324.using-dqs-cleansing-complex-data-using-composite-domains.aspx)。  
  
  
