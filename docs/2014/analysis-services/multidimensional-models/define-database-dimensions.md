---
title: 定义数据库维度，|Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- dimensions [Analysis Services], defining
ms.assetid: fe84588b-66a3-4100-a1cf-59b21b7adf01
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6225e17feef079fba352b0656fb8fc9d28c86748
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52518979"
---
# <a name="define-database-dimensions"></a>定义数据库维度
  可以使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中的维度设计器，在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目或数据库中配置现有数据库维度。 可以使用维度设计器执行下列任务：  
  
-   配置维度级别属性。  
  
-   添加和配置维度特性。  
  
-   定义和配置用户定义层次结构。  
  
-   定义和配置特性之间的关系。  
  
-   定义维度翻译。  
  
-   对于已处理的维度，您可以浏览维度结构并查看数据。  
  
 修改维度、属性或层次结构后，必须处理该维度才能查看更改。 在项目模式下工作时，应在开始处理前部署对 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的更改。  
  
 有关如何在维度设计器中打开维度的详细信息，请参阅 [在解决方案资源管理器中修改或删除数据库维度](database-dimensions-modify-or-delete-a-database-dimension-in-solution-explorer.md)。  
  
 维度设计器中有三个不同的选项卡，下表对这些选项卡进行了说明。  
  
|Tab|Description|  
|---------|-----------------|  
|**维度结构**|使用此选项卡上，若要使用的维度到结构检查或创建数据源视图架构对于维度，以处理特性，以及组织中用户定义的层次结构的属性。|  
|**属性关系**|使用此选项卡可以创建、修改或删除维度的属性关系。|  
|**翻译**|使用此选项卡可以不同的语言添加和编辑维度元数据的翻译。|  
|**浏览者**|使用此选项卡可检查已处理维度的成员和审查维度元数据的翻译。|  
  
 以下主题介绍了您可以在维度设计器中执行的任务。  
  
 [维度特性属性参考](dimension-attribute-properties-reference.md)  
 说明如何定义和配置维度属性。  
  
 [创建用户定义层次结构](user-defined-hierarchies-create.md)  
 说明如何定义和配置用户定义层次结构。  
  
 [定义属性关系](attribute-relationships-define.md)  
 说明如何定义和配置属性关系。  
  
 [使用商业智能向导增强维度](../use-the-business-intelligence-wizard-to-enhance-dimensions.md)  
 说明如何使用商业智能向导增强维度。  
  
  
