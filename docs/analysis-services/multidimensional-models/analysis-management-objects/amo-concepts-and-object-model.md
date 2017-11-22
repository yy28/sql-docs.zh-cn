---
title: "AMO 概念和对象模型 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- AMO, classes
- Analysis Management Objects, classes
- objects [Analysis Management Objects]
- AMO, objects
- classes [AMO]
- AMO
- Analysis Management Objects
- Analysis Management Objects, objects
ms.assetid: 3b0cdf8e-46d5-4dfe-8b2c-233c27e1473e
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4943e1ff3c3c18814993a85bd108bb473e644726
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="amo-concepts-and-object-model"></a>AMO 概念和对象模型
  本主题提供的分析管理对象 (AMO) 的定义如何与其他工具和库中的体系结构提供相关 AMO [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]，以及在 AMO 中的所有主对象的概念说明。  
  
 AMO 是 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 的管理类的完整集合，可在托管环境中，在 <xref:Microsoft.AnalysisServices> 命名空间下以编程方式使用。 类包含在 AnalysisServices.dll 文件中，通常可找到 where[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]安装程序安装文件，在文件夹 \100\SDK\Assemblies\\。 若要使用 AMO 类，请将对此程序集的引用包含在项目中。  
  
 通过使用你将能够创建的 AMO，修改和删除对象，例如多维数据集、 维度、 挖掘结构和[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]数据库; 在所有这些对象，可以从.NET Framework 中应用程序执行操作。 您还可以处理和更新存储在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 数据库中的信息。  
  
 无法通过 AMO 来查询数据。 若要查询你的数据，使用[使用 ADOMD.NET 开发](../../../analysis-services/multidimensional-models/adomd-net/developing-with-adomd-net.md)。  
  
 本主题包含以下各节：  
  
 [AMO 中的 Analysis Services 体系结构](#AMOintheAnalysisServicesArchitecture)  
  
 [AMO 体系结构](#AMOArchitecture)  
  
 [使用 AMO](#bkmk_UsingAMO)  
  
 [自动执行使用 AMO 的管理任务](#AutomatingAdministrativeTaskswithAMO)  
  
##  <a name="AMOintheAnalysisServicesArchitecture"></a>AMO 中的 Analysis Services 体系结构  
 按照设计，AMO 只用于对象管理，而不用于查询数据。 如果用户需要查询[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]从客户端应用程序的数据，客户端应用程序应使用[使用 ADOMD.NET 开发](../../../analysis-services/multidimensional-models/adomd-net/developing-with-adomd-net.md)。  
  
##  <a name="AMOArchitecture"></a>AMO 体系结构  
 AMO 是用于管理的实例的类的完整库[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]从客户端应用程序在.NET Framework 2.0 版的托管代码中。  
  
 AMO 类库具有类层次结构，特定的类必须在其他类之前实例化才能在代码中使用。 此外，还有可随时在代码中实例化的辅助类，但是在使用任一辅助类之前，您可能已经实例化了类层次结构中的一个或多个类。  
  
 下图是 AMO 层次结构的高级视图，它包含该层次结构中的主要类。 该图显示各类在其容器和同级之间的位置。 <xref:Microsoft.AnalysisServices.Dimension> 属于 <xref:Microsoft.AnalysisServices.Database> 和 <xref:Microsoft.AnalysisServices.Server>，可与 <xref:Microsoft.AnalysisServices.DataSource> 和 <xref:Microsoft.AnalysisServices.MiningStructure> 同时创建。 在同一级别上，某些类必须先实例化，然后才能使用该级别的其他类。 例如，必须先创建 <xref:Microsoft.AnalysisServices.DataSource> 的实例，然后才能添加新的 <xref:Microsoft.AnalysisServices.Dimension> 或 <xref:Microsoft.AnalysisServices.MiningStructure>。  
  
 ![AMO 类高级别视图](../../../analysis-services/multidimensional-models/analysis-management-objects/media/amo-highlevelview-majorobjectshighlighted.gif "AMO 类高级视图")  
  
 A*主要对象*是为整个实体而不是另一个对象的一部分代表整个对象的类。 主要对象包括 <xref:Microsoft.AnalysisServices.Server>、<xref:Microsoft.AnalysisServices.Cube>、<xref:Microsoft.AnalysisServices.Dimension> 和 <xref:Microsoft.AnalysisServices.MiningStructure>，因为它们是独立的实体。 但是，<xref:Microsoft.AnalysisServices.Level> 不是主要对象，因为它是 <xref:Microsoft.AnalysisServices.Dimension> 的一个组成部分。 主要对象的创建、删除、修改或处理可以独立于其他对象。 次要对象是只能作为创建父级主要对象的一部分才能创建的对象。 次要对象通常在创建主要对象时创建。 次要对象的值应在创建时定义，因为次要对象没有默认创建值。  
  
 下图显示 <xref:Microsoft.AnalysisServices.Server> 对象包含的主要对象。  
  
 ![AMO 主对象突出显示](../../../analysis-services/multidimensional-models/analysis-management-objects/media/amo-majorobjects.gif "AMO 主对象突出显示")  
  
 ![AMO 主对象突出显示 (2)](../../../analysis-services/multidimensional-models/analysis-management-objects/media/amo-majorobjects-02.gif "AMO 主对象突出显示 (2)")  
  
 用 AMO 进行编程时，类和包含类之间的关联使用集合类型属性，例如 <xref:Microsoft.AnalysisServices.Server> 和 <xref:Microsoft.AnalysisServices.Dimension>。 若要使用包含类的一个实例，请先获取对含有或能够含有该包含类的集合对象的引用。 然后，在该集合中找到要查找的特定对象，接着可以获得该对象的引用，以便开始使用该对象。  
  
### <a name="amo-classes"></a>AMO 类  
 AMO 是一个类库，用于通过客户端应用程序管理 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例。 可以将 AMO 库视为用于完成特定任务的逻辑相关对象组。 AMO 类可以按照以下方式进行分类：  
  
|类集|用途|  
|---------------|-------------|  
|[AMO Fundamental 类](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-fundamental-classes.md)|使用任何其他类集所必需的类。|  
|[AMO OLAP 类](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-olap-classes.md)|用于管理 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 中的 OLAP 对象的类。|  
|[AMO Data Mining 类](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-data-mining-classes.md)|用于管理 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 中的数据挖掘对象的类。|  
|[AMO 安全类](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-security-classes.md)|用于控制对其他对象的访问权限以及维护安全性的类。|  
|[AMO 其他类和方法](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-other-classes-and-methods.md)|用于帮助 OLAP 或数据挖掘管理员完成其日常任务的类。|  
  
##  <a name="bkmk_UsingAMO"></a>使用 AMO  
 AMO 对于自动执行重复任务来说特别有用，例如，基于事实数据表中的新数据在度量值组中创建新分区，或者基于新数据为挖掘模型重新定型。 这些创建新对象的任务经常按月、周或季度执行，并且应用程序可以很容易地基于新数据命名这些新对象。  
  
##### <a name="analysis-services-administrators"></a>Analysis Services 管理员  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 管理员可以使用 AMO 自动执行 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 数据库的处理。 设计和部署 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 数据库则应使用 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]。  
  
##### <a name="developers"></a>开发人员  
 开发人员可以使用 AMO 为特定用户组开发管理界面。 这些界面可以限制对 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 对象的访问，还可以限制用户只能执行特定任务。 例如，使用 AMO 可以创建一个备份应用程序，用户使用该应用程序可以查看所有数据库对象，可以选择其中的任何一个数据库，还可以将该数据库备份到指定设备组中的任何一个设备中。  
  
 开发人员还可以在其应用程序中嵌入 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 逻辑。 为此，开发人员可以基于用户输入和其他因素创建多维数据集、维度、挖掘结构和挖掘模型。  
  
##### <a name="olap-advanced-users"></a>OLAP 高级用户  
 OLAP 高级用户通常是数据分析人员或者其他有很强的编程背景以及想要进一步使用数据对象以改善其数据分析的丰富经验的数据用户。 对于需要脱机工作的用户，AMO 可以在脱机之前自动创建本地多维数据集，因而非常有用。  
  
##### <a name="data-mining-advanced-users"></a>数据挖掘高级用户  
 对于数据挖掘高级用户，如果您有必须定期重新定型的大型模型集，则 AMO 是最有用的。  
  
##  <a name="AutomatingAdministrativeTaskswithAMO"></a>自动执行使用 AMO 的管理任务  
 对于大多数重复性的任务来说，与使用任何您选择的语言将其开发为应用程序相比，使用 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 进行开发可以更好地设计、部署和维护这些任务。 但是，对于不能使用 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 自动执行的重复性任务，可以使用 AMO。 如果您想用 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 开发专用的商业智能应用程序，AMO 也很有用。  
  
##### <a name="automatic-object-management"></a>自动对象管理  
 使用 AMO，可以很容易地基于用户输入或获取的新数据来创建、更新或删除 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 对象（例如，<xref:Microsoft.AnalysisServices.Database>、<xref:Microsoft.AnalysisServices.Dimension>、<xref:Microsoft.AnalysisServices.Cube>、挖掘 <xref:Microsoft.AnalysisServices.MiningStructure> 和 <xref:Microsoft.AnalysisServices.MiningModel> 或 <xref:Microsoft.AnalysisServices.Role>）。 AMO 非常适合用于必须将已开发的解决方案从独立软件提供商部署到最终客户的安装应用程序。 安装应用程序可以验证是否存在早期版本，如果存在，则可以更新结构，删除不再有用的对象，并创建新对象。 如果不存在早期版本，它可以从头开始创建所有内容。  
  
 AMO 可以非常方便地基于新数据创建新分区，并且可以删除已经超出项目范围的旧分区。 例如，对于使用最近 36 个月数据的财务分析解决方案，当接收到新的一个月的数据时，之前第 37 个月的旧数据即可立即被删除。 为了优化性能，可以基于使用情况设计新聚合并应用于最近的 12 个月。  
  
##### <a name="automatic-object-processing"></a>自动对象处理  
 使用 AMO 可以实现对象处理和更新的可用性，从而响应一些特定的事件，而对这些事件进行响应是通常的流数据和使用 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 的计划任务无法胜任的。  
  
##### <a name="automatic-security-management"></a>自动安全管理  
 可以自动执行安全管理操作，向新用户分配角色和权限或者当其他用户过期时立即将其删除。 可以创建新界面以简化安全管理员的安全管理工作。 这比使用 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 更容易。  
  
##### <a name="automatic-backup-management"></a>自动备份管理  
 使用 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 任务或者创建自动运行的专用 AMO 应用程序可以自动进行备份管理。 使用 AMO 可以为操作员开发帮助他们完成日常工作的备份界面。  
  
##### <a name="tasks-amo-is-not-intended-for"></a>不适合使用 AMO 的任务  
 AMO 不能用于查询数据。 若要查询 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 数据，包括多维数据集和挖掘模型，请在用户应用程序中使用 ADOMD.NET。 有关详细信息，请参阅[使用 ADOMD.NET 开发](../../../analysis-services/multidimensional-models/adomd-net/developing-with-adomd-net.md)。  
  
  
