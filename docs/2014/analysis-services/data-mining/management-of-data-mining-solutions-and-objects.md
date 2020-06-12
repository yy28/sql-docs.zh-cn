---
title: 管理数据挖掘解决方案和对象 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining [Analysis Services], managing
- managing mining models
ms.assetid: 06fc61dd-925c-4347-8677-7046ee5d2f6f
author: minewiskan
ms.author: owend
ms.openlocfilehash: ae3e672932dd320c6b369f23f03c1f056d30d4ba
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2020
ms.locfileid: "84522173"
---
# <a name="management-of-data-mining-solutions-and-objects"></a>管理数据挖掘解决方案和对象
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 提供可用于管理现有挖掘结构和挖掘模型的客户端工具。 本节介绍使用每种环境可以执行的管理操作。  
  
 除了这些工具之外，还可以使用 AMO 以编程方式管理数据挖掘对象，或使用连接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库的其他客户端，如 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 2007 的数据挖掘外接程序。  
  
## <a name="in-this-section"></a>本节内容  
 [移动数据挖掘对象](moving-data-mining-objects.md)  
  
 [处理要求和注意事项（数据挖掘）](processing-requirements-and-considerations-data-mining.md)  
  
 [使用 SQL Server 事件探查器监视数据挖掘（Analysis Services - 数据挖掘）](using-sql-server-profiler-to-monitor-data-mining-analysis-services-data-mining.md)  
  
## <a name="location-of-data-mining-objects"></a>数据挖掘对象的位置  
 已处理的挖掘结构和挖掘模型通常存储在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的实例中。  
  
 如果在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] `Immediate` 开发数据挖掘对象时在模式下创建了与数据库的连接，则在工作时，所创建的任何对象都会立即添加到服务器中。 但是，如果在 **“脱机”** 模式下设计数据挖掘对象，这也是在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中工作时的默认设置，则您创建的挖掘对象在部署到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]实例之前只是一些元数据容器。 因此，无论任何时候，只要对对象进行了更改，则就必须将对象重新部署到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务器。 有关数据挖掘体系结构的详细信息，请参阅[物理体系结构（Analysis Services - 数据挖掘）](physical-architecture-analysis-services-data-mining.md)。  
  
> [!NOTE]  
>  诸如 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 2007 数据挖掘外接程序之类的客户端还可用于创建会话挖掘模型和挖掘结构，它们使用到实例的连接，但只在会话期间在服务器中存储挖掘结构和挖掘模型。 您仍然可以通过客户端管理这些模型，就如同管理 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库中存储的结构和模型一样，但断开与 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]实例的连接后，不会持久化这些对象。  
  
## <a name="managing-data-mining-objects-in-sql-server-data-tools"></a>在 SQL Server Data Tools 中管理数据挖掘对象  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 提供便于创建、浏览和编辑数据挖掘对象的功能。  
  
 以下链接提供有关如何使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]修改数据挖掘对象的信息：  
  
-   [编辑用于挖掘结构的数据源视图](edit-the-data-source-view-used-for-a-mining-structure.md)  
  
-   [更改挖掘结构的属性](change-the-properties-of-a-mining-structure.md)  
  
-   [更改挖掘模型的属性](change-the-properties-of-a-mining-model.md)  
  
-   [查看或更改建模标志（数据挖掘）](modeling-flags-data-mining.md)  
  
-   [查看或更改算法参数](view-or-change-algorithm-parameters.md)  
  
 通常，您将使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 作为工具来开发新项目和添加到现有项目，然后管理已使用诸如 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的工具进行部署的项目和对象。  
  
 但是，您可以使用 `Immediate` 选项并在联机模式下连接到 ssASnoversion 实例，直接修改已部署到该服务器的对象。 有关详细信息，请参阅 [Connect in Online Mode to an Analysis Services Database](../multidimensional-models/connect-in-online-mode-to-an-analysis-services-database.md)。  
  
> [!WARNING]  
>  所有对挖掘结构或挖掘模型的更改，包括对元数据（如名称或说明）的更改，都要求重新处理结构或模型。  
  
 如果您没有用于创建数据挖掘项目或对象的解决方案文件，则可以使用 Analysis Services 导入向导从服务器导入现有项目，对该对象进行修改，然后使用 `Incremental` 选项重新进行部署。 有关详细信息，请参阅 [使用 Analysis Services 导入向导导入数据挖掘项目](import-a-data-mining-project-using-the-analysis-services-import-wizard.md)。  
  
## <a name="managing-data-mining-objects-in-sql-server-management-studio"></a>在 SQL Server Management Studio 中管理数据挖掘对象  
 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，可以编写挖掘结构和挖掘模型的脚本、处理或删除挖掘结构和挖掘模型。 使用对象资源管理器仅可以查看有限的一组属性；但是，您可以通过打开 **“DMX 查询”** 窗口并选择挖掘结构，以查看有关挖掘模型的其他元数据。  
  
-   [在 SQL Server Management Studio 中创建一个 DMX 查询](create-a-dmx-query-in-sql-server-management-studio.md)  
  
## <a name="managing-data-mining-objects-programmatically"></a>以编程方式管理数据挖掘对象  
 使用以下编程语言可创建、更改、处理和删除数据挖掘对象。 每种语言都是针对不同任务设计的，因此，对您可执行的操作类型可能有一些限制。 例如，数据挖掘对象的某些属性不能通过使用数据挖掘扩展插件 (DMX) 进行更改，而必须使用 XMLA 或 AMO。  
  
### <a name="analysis-management-objects-amo"></a>分析管理对象 (AMO)  
 Analysis Management Objects (AMO) 是一个构建在 XMLA 之上的对象模型，它使您可以完全控制数据挖掘对象。 通过使用 AMO，您可以创建、部署和监视挖掘结构和挖掘模型。  
  
-   [AMO 概念和对象模型](https://docs.microsoft.com/bi-reference/amo/amo-concepts-and-object-model)  
  
-   <xref:Microsoft.AnalysisServices>  
  
 **限制：** 无。  
  
### <a name="data-mining-extensions-dmx"></a>数据挖掘扩展插件 (DMX)  
 数据挖掘扩展插件 (DMX) 可以与其他命令接口（如 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 或 ADOMD.Net）配合使用来创建、删除和查询挖掘结构和挖掘模型。  
  
-   [数据挖掘扩展插件 (DMX) 数据定义语句](/sql/dmx/dmx-statements-data-definition)  
  
 **限制：** 使用 DMX 无法更改某些属性。  
  
### <a name="xml-for-analysis-xmla"></a>XML for Analysis (XMLA)  
 XML for Analysis (XMLA) 是用于所有 Analysis Services 的数据定义语言。 XMLA 使您可以控制大多数数据挖掘对象和服务器操作。 客户端和服务器之间的所有管理操作都可通过使用 XMLA 来执行。 为了方便，可以使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 脚本语言 (ASSL) 对 XML 进行换行。  
  
 **限制：** [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 生成的某些 XMLA 语句仅支持在内部使用，而不能在 XML DDL 脚本中使用。  
  
## <a name="see-also"></a>另请参阅  
 [开发人员指南 &#40;Analysis Services&#41;](../analysis-services-developer-documentation.md)  
  
  
