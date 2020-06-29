---
title: DQS 清除转换 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- data correction
- correct data
ms.assetid: d2ec1b1a-c745-4741-b57c-6fdb524a154c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6df48dd9d90802b5694dcc6b7f73a65aee46b5e9
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85430684"
---
# <a name="dqs-cleansing-transformation"></a>DQS 清除转换
  DQS 清除转换使用 Data Quality Services (DQS)，通过应用为连接的数据源或类似数据源创建的已批准规则来更正来自连接的数据源的数据。 有关数据更正规则的详细信息，请参阅 [DQS Knowledge Bases and Domains](../../../data-quality-services/dqs-knowledge-bases-and-domains.md)。 有关 DQS 的详细信息，请参阅 [Data Quality Services Concepts](../../../data-quality-services/data-quality-services-concepts.md)。  
  
 为了确定是否必须更正数据，DQS 清除转换在满足以下条件时处理输入列中的数据：  
  
-   该列已选定用于数据更正。  
  
-   数据更正支持该列数据类型。  
  
-   该列映射到的域具有兼容数据类型。  
  
 该转换还包括您配置为处理行级错误的错误输出。 若要配置错误输出，请使用 **“DQS 清理转换编辑器”** 。  
  
 您可以在数据流中包含 [Fuzzy Grouping Transformation](fuzzy-grouping-transformation.md) 来标识可能为重复项的数据行。  
  
## <a name="data-quality-projects-and-values"></a>数据质量项目和值  
 使用 DQS 清理转换处理数据时，会在数据质量服务器上创建一个清理项目。 使用数据质量客户端管理项目。 此外，您还可以使用数据质量客户端将项目值导入 DQS 知识库域。 只能将值导入配置为使用 DQS 清理转换的域（或链接域）。  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [在 Data Quality Client 中打开 Integration Services 项目](../../../data-quality-services/open-integration-services-projects-in-data-quality-client.md)  
  
-   [将清理项目值导入域](../../../data-quality-services/import-cleansing-project-values-into-a-domain.md)  
  
-   [将数据质量规则应用于数据源](apply-data-quality-rules-to-data-source.md)  
  
## <a name="related-content"></a>相关内容  
  
-   [管理数据质量项目&#41; &#40;打开、解锁、重命名和删除](../../../data-quality-services/manage-open-unlock-rename-and-delete-a-data-quality-project.md)  
  
-   social.technet.microsoft.com 上的文章： [使用复合域清理复杂数据](https://social.technet.microsoft.com/wiki/contents/articles/13324.using-dqs-cleansing-complex-data-using-composite-domains.aspx)。  
  
  
