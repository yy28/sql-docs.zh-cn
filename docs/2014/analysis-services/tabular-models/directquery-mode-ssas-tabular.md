---
title: DirectQuery 模式 (SSAS 表格) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.realtime.f1
ms.assetid: 45ad2965-05ec-4fb1-a164-d8060b562ea5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9ab544235e842e38024ce98763094c300bb06275
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66067232"
---
# <a name="directquery-mode-ssas-tabular"></a>DirectQuery 模式（SSAS 表格）
  Analysis Services 能让你检索数据并从表格模型创建报表，通过直接从关系数据库系统检索数据和聚合使用*DirectQuery 模式下*。 本主题介绍仅驻留在内存中的标准表格模型和可查询关系数据源的表格模型之间的差异，并且说明如何创建和部署要在 DirectQuery 模式下使用的模型。  
  
 本主题的内容：  
  
-   [DirectQuery 模式的优点](#bkmk_Benefits)  
  
-   [创建模型以便用于 DirectQuery 模式](#bkmk_Design)  
  
    -   [用于 DirectQuery 模型的数据源](directquery-mode-ssas-tabular.md#bkmk_DataSources)  
  
    -   [验证和 DirectQuery 模式下的设计限制](#bkmk_Validation)  
  
    -   [用于 DirectQuery 模型的公式兼容性](#bkmk_FormulaCompat)  
  
    -   [在 DirectQuery 模式下的安全](#bkmk_Security)  
  
    -   [在 DirectQuery 模式下的安全](#bkmk_Security)  
  
-   [DirectQuery 属性](#bkmk_PropertyList)  
  
-   [相关的主题和任务](#bkmk_related_tasks)  
  
##  <a name="bkmk_Benefits"></a> DirectQuery 模式的优点  
 默认情况下，表格模型使用内存中缓存来存储和查询数据。 因为表格模型使用在内存中驻留的数据，所以，即使是复杂查询也可以非常快地执行。 但是，使用缓存数据存在以下缺点：  
  
-   在源数据发生变化时，数据不刷新。 您必须对模型进行处理，以便对数据进行更新。  
  
-   在您关闭承载模型的计算机时，缓存将保存到磁盘中，并且在您加载模型或打开 PowerPivot 文件时必须重新打开。 保存和加载操作可能需要很长时间。  
  
 相反，DirectQuery 模式使用在 SQL Server 数据库中存储的数据。  通常，在您创建模型时将全部数据或少量示例数据导入到缓存中，并且在您部署模型时，指定用于查询模型的数据源应该是 SQL Server 而非缓存的数据。 针对数据的任何 DAX 查询都将由 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 转换为针对指定关系数据源的等效 SQL 语句。  
  
 使用 DirectQuery 模式部署模型有很多优点：  
  
-   可能存在这样的模型：其数据集过大以至于 Analysis Services 服务器上的内存无法容纳。  
  
-   数据确保是最新的，并且没有不得不维护数据的单独副本的额外管理开销。 对于基础数据源的更改可立即反映在针对数据模型的查询中。  
  
-   DirectQuery 可以利用提供程序端的查询加速功能，例如，xVelocity 内存优化列索引提供的加速功能。  
  
-   后端数据库采用的任何安全性也保证会被采用，并且使用行级安全性。 相反，如果您在使用缓存的数据，可能很难确保能够以在服务器上保护数据的相同方式来保护缓存的安全。  
  
-   如果模型包含可能要求多个查询的复杂公式，则 Analysis Services 可以执行优化以便确保对后端数据库执行的查询的查询计划将尽可能高效。  
  
##  <a name="bkmk_Design"></a> 创建模型以便用于 DirectQuery 模式  
 表格模型是使用模型设计器 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 创建的。 模型设计器将在内存中创建所有模型，这意味着在您建模时，如果数据太大以至于无法放入内存中，则应该仅将一部分的数据导入到工作区数据库使用的缓存中。  
  
 在您做好切换到 DirectQuery 模式的准备后，可以更改启用 DirectQuery 模式的属性。 有关详细信息，请参阅[启用 DirectQuery 设计模式&#40;SSAS 表格&#41;](enable-directquery-mode-in-ssdt.md)。  
  
 在您执行此操作时，模型设计器自动配置工作区数据库以便在混合模式下运行，使您可以继续使用缓存的数据。 模型设计器还将通知您模型中与 DirectQuery 模式不兼容的任何功能。 下表总结了需要牢记的主要要求：  
  
-   **数据源：** DirectQuery 模型只能使用来自单个 SQL Server 数据源的数据。 如果已经为某一模型启用了 DirectQuery 模式，您将无法在模型设计器中使用任何其他数据类型，包括复制-粘贴操作添加的表。 所有其他导入选项都将被禁用。 在查询中包含的任何表都必须是 SQL Server 数据源的一部分。 请参阅[DirectQuery 模型的数据源](directquery-mode-ssas-tabular.md#bkmk_DataSources)有关详细信息。  
  
-   **对计算列的支持：** DirectQuery 模型不支持计算的列。 但是，您可以创建度量值和 KPI，它们都对数据集进行操作。 请参阅章节[验证](#bkmk_Validation)有关详细信息。  
  
-   **DAX 函数的受限的使用：** 不能在 DirectQuery 模式下，使用某些 DAX 函数，因此你必须使用其他函数代替它们，或创建数据源中使用派生的列的值。 模型设计器为您在创建与 DirectQuery 模式不兼容的公式时引发的任何错误提供设计时验证。 请参阅以下各节，有关详细信息：[验证](#bkmk_Validation)。  
  
-   **公式兼容性：** 在某些已知情况下，与仅使用关系数据存储的 DirectQuery 模型相比，相同的公式可能在缓存模型或混合模型下返回不同的结果。 这些差异是由 xVelocity 内存中分析 (VertiPaq) 引擎和 SQL Server 之间的语义差异造成的。 有关这些差异的详细信息，请参阅本部分中：[公式兼容性](#bkmk_FormulaCompat)。  
  
-   **安全性：** 可以使用不同的方法来保护模型根据部署方式。 通过使用 Analysis Services 实例的安全模型，确保缓存的表格模型数据的安全。 可使用角色确保 DirectQuery 模型的安全，但是，您也可以使用在关系数据存储区中定义的安全性。 可以配置模型，以便基于仅限 DirectQuery 模型打开报表的用户只能看到基于其在 SQL Server 中的权限允许该用户看到的数据。 请参阅此部分，了解详细信息：[安全](#bkmk_Security)。  
  
-   **客户端限制：** 当模型处于 DirectQuery 模式下时，只能通过使用 DAX 查询。 不能使用 MDX 来创建查询。 这意味着您不能使用 Excel 数据透视客户端，因为 Excel 使用 MDX。  
  
     但是，可以创建针对 DirectQuery 模型中的查询[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]如果将 DAX 表查询用作 XMLA Execute 语句的一部分有关详细信息，请参阅[DAX 查询语法参考](https://msdn.microsoft.com/library/ee634217.aspx)。  
  
 在您解决了所有设计问题并且对您的模型进行了测试后，就可以进行部署了。 此时，您可以设置用于响应针对模型的查询的首选方法。 您是希望用户有权访问缓存，还是始终仅使用关系数据源？  
  
 如果您在部署模型*混合模式*，缓存仍然可用，可用于查询。 混合模式为您提供许多选项：  
  
-   在缓存和关系数据源都可用时，您可以设置首选连接方法，但最终还是客户端使用 DirectQueryMode 连接字符串属性来控制所使用的源。  
  
-   您还可以配置缓存上的分区，以便永远不处理用于 DirectQuery 模式的主分区，并且主分区必须始终引用关系数据源。 有许多方法可以使用分区来优化模型设计和报表体验。 有关详细信息，请参阅[分区和 DirectQuery 模式&#40;SSAS 表格&#41;](define-partitions-in-directquery-models-ssas-tabular.md)。  
  
-   在部署了模型后，您可以更改首选连接方法。 例如，您可以使用混合模式来进行测试，并且仅在全面测试了使用该模型的所有报表或查询后，才将模型切换到“仅限 DirectQuery”  模式。 有关详细信息，请参阅 [设置或更改 DirectQuery 的首选连接方法](../set-or-change-the-preferred-connection-method-for-directquery.md)。  
  
###  <a name="bkmk_DataSources"></a> 用于 DirectQuery 模型的数据源  
 在您更改设计环境以便启用 DirectQuery 模式后，应立即对用于工作区数据库的数据源进行验证，以便确保它们来自单个 SQL Server 数据源。 DirectQuery 模型中不允许来自其他数据源的数据，包括复制-粘贴的数据。  
  
 如果您想要在 DirectQuery 模式下使用模型，必须确保报表所需的所有数据都存储于指定的 SQL Server 数据库中。 如果建模所需的数据在该数据源中不可用，则考虑使用 Integration Services 或其他数据仓库工具将数据导入到充当 DirectQuery 数据源的 SQL Server 数据库中。  
  
###  <a name="bkmk_Validation"></a> 验证和 DirectQuery 模式下的设计限制  
 当您为在 DirectQuery 模式下使用而创建模型时，最初必须将某些部分的数据加载到缓存中。 如果你最终将使用的数据而言太大而无法放入内存，则可以使用**预览并筛选**表导入向导来选择数据的子集或编写 SQL 脚本中的选项来获取所需的数据。  
  
> [!WARNING]  
>  因为 DirectQuery 模式不支持使用计算列，所以，如果存在您想要对其进行合并或执行其他操作的列，则应该提前计划并且将列定义作为您的数据导入查询或脚本的一部分创建。  
  
 若要查看和解决验证错误，请在 **中打开** “错误列表” [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]。 导致无法使用 DirectQuery 模式的错误将会显示在 **“错误”** 选项卡中。在切换到 DirectQuery 模式之前必须修复这些错误。 比较难解决的验证错误通常与 DirectQuery 模式下不支持的公式相关。 请参阅的部分[公式兼容性](#bkmk_FormulaCompat)，有关与公式和计算的列相关的错误的概述。  
  
 下表介绍了为 DirectQuery 访问创建模型时应注意的其他事项：  
  
-   处于“仅限 DirectQuery”  模式下时，报表中的结果取决于正在查看结果的用户的安全上下文。 您应该使用不同的凭据对模型进行测试，以便确保用户得到预期结果。  
  
-   如果您将模型配置为在混合模式下操作，这允许使用缓存或来自 SQL Server 的数据，则应该了解连接到各数据源的客户端可能会看到不同结果，这取决于连接字符串中指定的模式。 如果您需要确保您的报表用户仅看到来自 SQL Server 的数据，则必须清除缓存或者将模型更改为“仅限 DirectQuery”。  
  
###  <a name="bkmk_FormulaCompat"></a> 用于 DirectQuery 模型的公式兼容性  
 某些模型可能包含在 DirectQuery 模式下不支持的公式，因此必须对模型进行重新设计，以便防止验证错误。 下面是对在 DirectQuery 模式下支持的公式的限制：  
  
-   在启用了 DirectQuery 模式的任何表格模型中均不支持计算列，甚至是在混合模型中也不支持。 如果您需要针对某一模型的计算列，则考虑通过在您的导入定义中使用 Transact-SQL，将这些计算列转换为派生列。  
  
-   DirectQuery 模型支持在度量值中使用 DAX 公式，度量值将转换为针对关系数据存储区的基于集的操作。 支持通过使用隐式度量值创建的所有度量值。  
  
-   并非支持所有函数。 因为在查询 DirectQuery 模型时 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将所有 DAX 公式和度量值定义都转换为 SQL 语句，所以，包含无法转换为 Transact-SQL 的元素的任何公式都将触发针对模型的验证错误。 例如，不支持时间智能函数。 即使支持的函数在行为上也可能会不同，例如统计函数。 有关兼容性问题的完整列表，请参阅[公式在 DirectQuery 模式下的兼容性](../dax-formula-compatibility-in-directquery-mode-ssas-2014.md)。  
  
-   在你将模型切换到 DirectQuery 模式时，模型中的某些公式可能会进行验证，但在对缓存和关系数据存储执行验证时将返回不同的结果。 这是因为，针对缓存的计算使用 xVelocity 内存中分析 (VertiPaq) 引擎的语义，该引擎包含用于模拟 Excel 的行为的许多功能，而针对在关系数据存储区中存储的数据的查询需要使用 SQL Server 的语义。 实时可能返回不同的结果时部署模型的 DAX 函数的列表，请参阅[公式在 DirectQuery 模式下的兼容性](../dax-formula-compatibility-in-directquery-mode-ssas-2014.md)。  
  
###  <a name="bkmk_Connecting"></a> 连接到 DirectQuery 模型  
 使用 MDX 作为查询语言的客户端不能连接到使用 DirectQuery 模式的模型。 例如，如果您尝试创建针对 DirectQuery 模型的 MDX 查询，则系统会向您显示一条错误消息，指示找不到多维数据集，或者多维数据集尚未处理。 可以使用 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]、DAX 公式或 XMLA 查询创建针对 DirectQuery 模型的查询。 有关如何执行针对表格模型的即席查询的详细信息，请参阅[表格模型数据访问](tabular-model-data-access.md)。  
  
 如果您正在使用混合模型，则可通过指定连接字符串属性 DirectQueryMode 来指定用户是连接到缓存还是使用 DirectQuery 数据。  
  
###  <a name="bkmk_Security"></a> 在 DirectQuery 模式下的安全  
 在模型创建过程中，您将指定用于检索源数据的权限。 通常，这将是您自己的凭据或用于开发的帐户。 但是，在您将模型切换为使用 DirectQuery 模式时，安全上下文将更为复杂：  
  
-   考虑用户是否具有访问关系数据存储区中数据的所需访问级别。  
  
-   查看相同的模型或报表的用户可能会看到不同的数据，具体取决于用户的安全上下文。  
  
-   如果模型缓存已被预留，则使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 安全模型（角色）保护缓存安全。 缓存可能包含模型设计人员有权看到、但用户无权看到的数据。 模型和报表设计人员应或者清除缓存，或者通过用角色控制访问权限来保护这些数据。  
  
-   连接到数据源时，响应来自缓存的查询的模型不能模拟当前用户。 如果要在连接到数据源时模拟当前用户，必须使用 DirectQuery 模式。  
  
-   如果您的报表模型要求安全性，则您具有以下两个选项：使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 角色，或者对数据源设置行级权限。 关系数据源中的安全性用于控制对表的访问权限，并且不支持列级安全性。 因此，如果一个区域中的用户无权查看来自不同区域的销售数据，则包含基于 Sales 表的度量值的报表将返回空白或错误。  
  
 模拟设置属性指定使用 DirectQuery 连接到模型时使用的凭据，要么用于仅限 DirectQuery 模型，要么用于使用 DirectQuery 响应查询的混合模型。 该属性具有以下值：  
  
 **默认**  
 使用在导入向导中指定的凭据连接到数据源。 这可能是特定的 Windows 用户或服务帐户。  
  
 `ImpersonateCurrentUser`  
 使用当前用户的凭据连接到数据源。  
  
 有关如何设置这些属性的信息，请参阅[DirectQuery 部署方案&#40;SSAS 表格&#41;](../directquery-deployment-scenarios-ssas-tabular.md)。  
  
##  <a name="bkmk_PropertyList"></a> DirectQuery 属性  
 下表列出了可以在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 和 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中设置的一些属性，这些属性用于启用 DirectQuery 和控制用于针对模型的查询的数据源。  
  
|属性名称|Description|  
|-------------------|-----------------|  
|**DirectQueryMode 属性**|此属性在模型设计器中启用 DirectQuery 模式。 您必须将此属性设置为 `On`，才能更改任何其他 DirectQuery 属性。<br /><br /> 有关详细信息，请参阅[启用 DirectQuery 设计模式&#40;SSAS 表格&#41;](enable-directquery-mode-in-ssdt.md)。|  
|**QueryMode 属性**|此属性指定针对 DirectQuery 模型的默认查询方法。当您部署模型时，在模型设计器中设置此属性；不过，您可以在以后覆盖它。 该属性具有以下值：<br /><br /> **DirectQuery** -此设置指定模型的所有查询都应都使用的关系数据源。<br /><br /> **DirectQuery 以及内存中** - 此设置指定默认情况下应通过使用关系数据源响应查询，除非在客户端的连接字符串中指定了其他项。<br /><br /> **内存中** - 此设置指定应仅通过使用缓存响应查询。<br /><br /> **内存中以及 DirectQuery** - 此设置指定默认情况下 应该通过使用缓存来响应查询，除非在客户端的连接字符串中指定了其他项。<br /><br /> <br /><br /> 有关详细信息，请参阅 [设置或更改 DirectQuery 的首选连接方法](../set-or-change-the-preferred-connection-method-for-directquery.md)。|  
|**DirectQueryMode 属性**|在部署了模型后，您可以通过在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中更改此属性，更改 DirectQuery 模型的首选查询数据源。<br /><br /> 与以前的属性相似，此属性也指定模型的默认数据源并且具有以下值：<br /><br /> **InMemory**:查询可以使用仅缓存。<br /><br /> **DirectQuerywithInMemory**:查询默认使用关系数据源，除非在客户端的连接字符串中指定了其他项。<br /><br /> **InMemorywithDirectQuery**:查询默认使用缓存，除非在客户端的连接字符串中指定了其他项。<br /><br /> (**DirectQuery**:查询仅使用关系数据源。<br /><br /> <br /><br /> 有关详细信息，请参阅 [设置或更改 DirectQuery 的首选连接方法](../set-or-change-the-preferred-connection-method-for-directquery.md)。|  
|**模拟设置属性**|此属性定义用于在查询时连接到 SQL Server 数据源的凭据。 您可以在模型设计器中设置此属性，并且可以在部署了模型后，在以后更改该属性值。<br /><br /> 请注意，这些凭据仅用于响应针对关系数据存储区的查询；它们与用于处理混合模型的缓存的凭据不同。<br /><br /> 当模型仅用于内存中时，不能使用模拟。 `ImpersonateCurrentUser` 设置无效，除非模型正在使用 DirectQuery 模式。|  
  
 此外，如果您的模型包含分区，则您必须选择一个分区来用作 DirectQuery 模式中查询的源。 有关详细信息，请参阅[分区和 DirectQuery 模式&#40;SSAS 表格&#41;](define-partitions-in-directquery-models-ssas-tabular.md)。  
  
##  <a name="bkmk_related_tasks"></a> 相关的主题和任务  
  
|主题|Description|  
|-----------|-----------------|  
|[分区和 DirectQuery 模式下&#40;SSAS 表格&#41;](define-partitions-in-directquery-models-ssas-tabular.md)|说明如何在配置为 DirectQuery 模式的模型中使用分区。|  
|[DirectQuery 模式下的 DAX 公式兼容性](../dax-formula-compatibility-in-directquery-mode-ssas-2014.md)|说明可在配置为 DirectQuery 模式的模型中使用的公式的限制和兼容性要求。|  
|[启用 DirectQuery 设计模式&#40;SSAS 表格&#41;](enable-directquery-mode-in-ssdt.md)|说明如何更改设计时环境以便它支持使用 DirectQuery 模式|  
|[更改 DirectQuery 分区&#40;SSAS 表格&#41;](../change-the-directquery-partition-ssas-tabular.md)|说明如何更改 DirectQuery 分区。|  
|[设置或更改 DirectQuery 的首选连接方法](../set-or-change-the-preferred-connection-method-for-directquery.md)|说明如何设置或更改配置为 DirectQuery 的模型的连接方法。|  
|[DirectQuery 部署方案&#40;SSAS 表格&#41;](../directquery-deployment-scenarios-ssas-tabular.md)|说明 DirectQuery 部署方案。|  
|[为表格模型数据库配置内存中或 DirectQuery 访问](enable-directquery-mode-in-ssms.md)|了解 DirectQuery 配置|  
|[清除 Analysis Services 缓存](../instances/clear-the-analysis-services-caches.md)|清除表格模型的缓存|  
  
## <a name="see-also"></a>请参阅  
 [分区（SSAS 表格）](partitions-ssas-tabular.md)   
 [表格模型项目（SSAS 表格）](tabular-model-projects-ssas-tabular.md)   
 [在 Excel 中分析（SSAS 表格）](analyze-in-excel-ssas-tabular.md)  
