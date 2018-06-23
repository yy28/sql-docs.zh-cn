---
title: 管理复合域 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 47821eff-800b-4053-8d36-e42bbc267f54
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 106eee996bf361f706279aa81c8d15b08aaef5b5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36127154"
---
# <a name="managing-a-composite-domain"></a>管理复合域
  本主题描述如何在 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 中使用复合域。 有时候，单一域不会令人满意地表示字段中的数据，并且您只能通过组合单一域来表示这些数据。 为此，您创建复合域。 一个复合域由两个或更多的单一域构成，并且映射到一个由多个相关字词构成的数据字段，这些相关字词未进行分析，但包括在单个复合值中。 该值中的每个字词都将由不同的单一域表示。 在您将单一域包括在复合域中，然后将复合域映射到数据字段后，可以通过在单一域中生成知识，在知识库中生成与该字段中的数据有关的知识。 复合域（与单一域相似）是单个数据字段中数据的语义表示形式。  
  
 复合域中的单一域必须具有一个共同的知识范畴。 一个例子是具有街道、城市、省/市/自治区、国家/地区和邮政编码数据的地址字段。 此字段中不同字词可能具有不同的数据类型。 为处理这种情况，您将这些字词映射到不同的单一域。 另一个例子是具有名字、中间名和姓氏数据的全名字段。 若要使用某一复合域，您必须能够将字段中的数据分析到不同的单一域中，为字段创建复合域并且为字段部分创建单一域。  
  
 复合域具有与单一域不同的功能。 您不能更改复合域中的值 - 必须在单一域中进行更改。 对于复合域，您可以使用跨域规则来测试复合域中单一域的值。 此外，还可以查看在复合域中找到的值的组合。  
  
## <a name="in-this-section"></a>本节内容  
 通过使用复合域，您可以执行以下操作：  
  
|||  
|-|-|  
|为由多个未进行分析的相关字词构成的数据字段创建语义表示形式|[创建复合域](../../2014/data-quality-services/create-a-composite-domain.md)|  
|在您将复杂数据映射到复合域时，可以基于知识对数据进行分析，并且可以对分隔符进行分析。 DQS 将首先尝试使用与单一域有关的知识来确定复杂字符串的部分如何属于单一域。|[创建复合域](../../2014/data-quality-services/create-a-composite-domain.md)|  
|将引用数据服务（例如用于处理地址数据的服务）附加到复合域。|[将域或复合域附加到参考数据](../../2014/data-quality-services/attach-a-domain-or-composite-domain-to-reference-data.md)|  
|在复合域中某个域的值影响其他域的值时，创建一个跨域规则。|[创建跨域规则](../../2014/data-quality-services/create-a-cross-domain-rule.md)|  
|标识值的组合，以便 DQS 可以报告其频率。|[在复合域中使用值关系](../../2014/data-quality-services/use-value-relations-in-a-composite-domain.md)|  
  
## <a name="related-tasks"></a>Related Tasks  
  
|任务说明|主题|  
|----------------------|-----------|  
|通过运行知识发现并以交互方式管理知识来生成知识库|[生成知识库](../../2014/data-quality-services/building-a-knowledge-base.md)|  
|将知识导入知识库，或从知识库中导出知识。|[导入和导出知识](../../2014/data-quality-services/importing-and-exporting-knowledge.md)|  
|创建单一域，并将知识添加到该域中。|[管理域](../../2014/data-quality-services/managing-a-domain.md)|  
  
  