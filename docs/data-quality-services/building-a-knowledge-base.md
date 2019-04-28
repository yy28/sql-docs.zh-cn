---
title: 生成知识库 | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2012
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 51eff161-6ecd-4ee4-8187-1dd8ef4814bd
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 45570669c6e1f0d42eb4af8960f84bf70adff891
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62862202"
---
# <a name="building-a-knowledge-base"></a>生成知识库

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 中的知识库是有关数据的知识的存储库，通过它您可以了解自己的数据并维护其完整性。 知识库由域构成，每个域都表示一个数据字段中的数据。 DQS 使用知识库来对数据库执行数据清理和消除重复。 若要为数据清理对知识库进行准备，您可以对数据示例运行计算机辅助分析，并且以交互方式管理域中的值。 通过 DQS，您可以导入知识、创建规则和关系、直接更改数据值以及利用默认数据库。  
  
## <a name="in-this-section"></a>本节内容  
 您可以对知识库执行以下操作：  
  
|||  
|-|-|  
|从头开始、从现有知识库或从一个 .dqs 数据文件创建新的知识库。|[创建知识库](../data-quality-services/create-a-knowledge-base.md)|  
|打开一个现有知识库以便执行知识发现、域管理或者添加匹配策略。|[打开知识库](../data-quality-services/open-a-knowledge-base.md)|  
|对知识库执行管理操作，包括打开知识库、取消锁定知识库、放弃您对知识库所做的工作、重命名知识库、删除知识库或查看知识库的属性。|[管理知识库](../data-quality-services/manage-a-knowledge-base.md)|  
|通过知识发现向知识库添加知识；域值管理；添加匹配策略；导入知识、域或值；或者使用默认知识库（即 DQS 数据）。|[将知识添加到知识库](../data-quality-services/adding-knowledge-to-a-knowledge-base.md)|  
|根据数据质量条件分析数据样本。|[执行知识发现](../data-quality-services/perform-knowledge-discovery.md)|  
  
## <a name="related-tasks"></a>Related Tasks  
  
|任务说明|主题|  
|----------------------|-----------|  
|将知识导入知识库，或从知识库中导出知识。|[导入和导出知识](../data-quality-services/importing-and-exporting-knowledge.md)|  
|创建单一域，并将知识添加到该域中。|[管理域](../data-quality-services/managing-a-domain.md)|  
|创建一个复合域，并将知识添加到该域中。|[管理复合域](../data-quality-services/managing-a-composite-domain.md)|  
  
  
