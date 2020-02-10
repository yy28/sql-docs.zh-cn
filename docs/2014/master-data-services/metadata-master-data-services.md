---
title: Metadata （Master Data Services） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- user-defined metadata [Master Data Services], about user-defined metadata
- metadata [Master Data Services], about metadata
- metadata [Master Data Services]
- user-defined metadata [Master Data Services]
ms.assetid: ac1aabe3-d8d4-4d7a-8954-50ee3c185d81
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 2bbb98653dbbaad577f9a48d7a778b41d19fbf37
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66054039"
---
# <a name="metadata-master-data-services"></a>元数据 (Master Data Services)
  在[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，用户定义元数据是您用于描述模型对象的信息。 例如，您可能要跟踪特定模型或实体的所有者，或者跟踪向实体提供数据的源系统。  
  
 用户定义元数据由名为**元数据**的模型管理。 此模型在安装时[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]自动包含，并且与所有其他 MDS 模型相似，不同之处在于你不能创建它的版本。  
  
 在使用用户定义元数据填充元数据模型之后，可以在订阅视图中包含该模型，以便它可由订阅系统使用。  
  
## <a name="metadata-entities"></a>元数据实体  
 “元数据”模型包括五个实体，每个实体都表示支持用户定义元数据的一种主数据模型对象。 例如，"**模型元数据定义**" 实体包含表示模型的成员，而 "**属性元数据定义**" 实体包含表示所有模型中所有属性的成员。  
  
 为了定义某一模型对象的元数据，您填充其中一个成员的属性。 例如，在 "**实体元数据定义**" 实体中，可以使用以下文本填充 Price 成员的 Description 属性：**销售给客户时的产品价格**。  
  
 只要添加或删除支持用户定义元数据的模型对象，元数据模型中的成员就会自动更新。  
  
 不能对元数据模型进行版本控制，添加或更改版本标志，也不能将该模型另存为模型部署包。 但是，该模型具有可用于其他主数据模型的其他所有功能。 例如，您可以对元数据模型实现一组业务规则，以便强制执行数据策略。  
  
## <a name="customizing-your-metadata-model"></a>自定义元数据模型  
 每个元数据定义实体都包括 Name、Code 和 Description 属性。 您可能要创建附加的属性以便进一步描述您的模型对象。  
  
 例如，您可以创建：  
  
-   名为 Owner 的基于域的属性，可用于跟踪各模型对象的所有者。  
  
-   名为 Last Review Date 的自由格式的属性，可用于跟踪所有者上次审核某一对象的日期。  
  
-   一个名为 "源" 的基于域的属性，可用于跟踪和管理与[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]实例交互的源系统。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|任务说明|主题|  
|----------------------|-----------|  
|向模型对象添加元数据。|[Master Data Services&#41;添加元数据 &#40;](add-metadata-master-data-services.md)
|&nbsp;|&nbsp;|
  
## <a name="related-content"></a>相关内容  
  
-   [将数据导出 &#40;Master Data Services&#41;](overview-exporting-data-master-data-services.md)  
  
  
