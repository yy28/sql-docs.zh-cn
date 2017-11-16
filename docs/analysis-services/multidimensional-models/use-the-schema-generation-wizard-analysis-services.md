---
title: "使用架构生成向导 (Analysis Services) |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Schema Generation Wizard, steps
- relational schema [Analysis Services], Schema Generation Wizard
ms.assetid: 8c710745-d41d-4c31-b6a2-2956229df75a
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3ebce1becae5b9133d577a81234ee5d2f8fa37a8
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="use-the-schema-generation-wizard-analysis-services"></a>使用架构生成向导 (Analysis Services)
  架构生成向导在生成阶段需要数量有限的信息。 架构生成向导在生成关系架构时所需的大多数信息都是从您已在项目中创建的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 多维数据集和维度中提取的。 此外，您可以自定义主题区域数据库架构的生成方式以及架构中对象的命名方式。  
  
## <a name="start-the-wizard"></a>启动向导  
 您可以使用下列几种不同的方法从 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中打开架构生成向导：  
  
-   右键单击 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目对象，然后在上下文菜单中单击“生成关系架构”。  
  
-   单击 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目对象，然后在 **“数据库”** 菜单中单击 **“生成关系架构”** 。  
  
-   通过单击向导的最后一页中的 **“立即生成架构”** 复选框，从维度向导内启动该向导。  
  
## <a name="step-1-specify-targets"></a>步骤 1：指定目标  
 必须指定架构生成向导要在其中生成主题区域数据库架构的数据源视图 (DSV)。 尽管您可以选择某个现有的 DSV，但通常您将基于数据源创建一个新的 DSV。 您可以根据现有或新的连接创建数据源，也可以根据其他对象创建数据源。 架构生成向导既可以在数据源引用的数据库中生成主题区域数据库架构，也可以在数据源视图中生成该架构。 架构生成向导不会创建主题区域数据库本身；相反，该向导在您指定的现有数据库中创建关系架构以支持多维数据集和维度。  
  
 当架构生成向导生成基础对象时，它便会使用数据源视图样式的绑定将 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 维度和多维数据集绑定到生成的表和列上。  
  
> [!NOTE]  
>  若要从先前生成的对象取消绑定 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 维度和多维数据集，请删除 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 多维数据集和维度绑定到的数据源视图，然后使用架构生成向导为多维数据集和维度定义新的数据源视图。  
  
## <a name="step-3-specify-schema-options-for-the-subject-area-database"></a>步骤 3：指定用于主题区域数据库的架构选项  
 架构生成向导提供大量选项，用于定义为主题区域数据库生成的架构。 您可以在该向导的 **“主题区域数据库架构选项”** 页中指定这些选项。  
  
### <a name="specifying-the-schema-owner"></a>指定架构所有者  
 您可以通过将 **“所属架构”** 的值设置为有效字符串来指定架构的所有者。 架构的默认所有者为 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目，但是您可以按照需要任意指定架构所有者。  
  
### <a name="specifying-primary-keys-indexes-and-constraints"></a>指定主键、索引和约束  
 架构生成向导会默认在主题区域数据库内的每个维度表中创建主键约束。 主键与指定为相应 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 维度中键属性的属性相对应。 此约束以最小的开销提高了多数环境中的处理性能。 逻辑主键始终在数据源视图中创建，即使您不选择在主题区域数据库中创建主键也是如此。 若要定义维度表的主键约束，请选择 **“创建维度表的主键”**。  
  
 该向导还会默认创建每个事实数据表中各外键列的索引。 这些索引提高了多数环境中的处理性能。 性能通常提高的原因是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 生成的用来从主题区域数据库中检索新数据的处理查询通常在事实数据表和维度表之间包含大量联接语句。 若要定义每个事实数据表中各外键列的索引，请选择 **“创建索引”**。  
  
 最后，该向导会默认在事实数据表和每个维度表之间强制实施引用完整性。 如果您不选择强制实施引用完整性，则架构生成向导仍会在数据库和数据源视图中创建这些关系。 若要强制实施引用完整性，请选择 **“强制引用完整性”**。  
  
### <a name="preserving-data-for-incremental-generation"></a>保留用于增量生成的数据  
 架构生成向导会默认在重新生成数据库架构时尝试保留数据。 如果架构生成向导因架构更改而必须删除一些行，则您会在删除行之前收到一则警告。 例如，由于您删除了维度，或者数据类型在更改维度属性时发生更改，那么行可能必须被删除以解决引用完整性问题。 若要在重新生成数据库架构时保留数据，请选择 **“重新生成时保留数据”**。  
  
## <a name="step-4-specify-naming-conventions"></a>步骤 4：指定命名约定  
 您可以定义架构生成向导在其 **“指定命名约定”** 页中的主题区域数据库内生成特定对象时使用的命名约定。 有关“指定命名约定”页上可用选项的详细信息，请参阅[指定命名约定（架构生成向导）（Analysis Services - 多维数据）](http://msdn.microsoft.com/library/02d830ea-5b1f-4485-9f94-d64b8bea592b)。  
  
  

