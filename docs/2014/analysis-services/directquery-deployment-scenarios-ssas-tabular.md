---
title: DirectQuery 部署方案（SSAS 表格） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 2aaf5cb8-294b-4031-94b3-fe605d7fc4c7
author: minewiskan
ms.author: owend
ms.openlocfilehash: 23f7debc1d2253938f235461279f39bb085c2b2f
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2020
ms.locfileid: "84528543"
---
# <a name="directquery-deployment-scenarios-ssas-tabular"></a>DirectQuery 部署方案（SSAS 表格）
  本主题提供 DirectQuery 模型的设计和部署过程的演练。 您可以将 DirectQuery 配置为只使用关系数据（仅限 DirectQuery），也可以将模型配置为在仅使用缓存数据或仅使用关系数据之间进行切换（混合模式）。 本主题说明了两种模式的实现过程，并根据模式和安全配置描述有关查询结果的可能的差异。  
  
 [设计和部署步骤](#bkmk_DQProcedure)  
  
 [比较 DirectQuery 配置](#bkmk_Configurations)  
  
##  <a name="design-and-deployment-steps"></a><a name="bkmk_DQProcedure"></a>设计和部署步骤  
 **步骤1。创建解决方案**  
  
 不论您使用哪种模式，都必须查看描述有关可用于 DirectQuery 模型的数据的限制信息。 例如，所有用于模型和报表的数据必须来自单个 SQL Server 数据库。 有关详细信息，请参阅 [DirectQuery 模式（SSAS 表格）](tabular-models/directquery-mode-ssas-tabular.md)。  
  
 也可以查看对度量值和计算列的限制，并确定您要使用的公式是否与 DirectQuery 模式兼容。 您可能需要删除或修改以下元素：  
  
-   不支持计算列。  
  
-   不能使用复制粘贴的数据。 如果您导入 PowerPivot 模型来开始您的解决方案，请确保在导入该解决方案之前删除链接表，因为该数据无法删除且将阻止 DirectQuery 验证。  
  
 **步骤2。在模型设计器中启用 DirectQuery 模式**  
  
 默认情况下，DirectQuery 将被禁用。 因此，您必须配置设计环境以便支持 DirectQuery 模式。  
  
 在解决方案资源管理器中右键单击 " **model.bim** " 节点，并将属性 " **DirectQuery 模式**" 设置为 `On` 。  
  
 您可以随时启用 DirectQuery；但是，为了确保您不会创建与 DirectQuery 模式不兼容的列或公式，我们建议您从一开始就启用 DirectQuery 模式。  
  
 最初，甚至始终在内存中创建 DirectQuery 模型。 工作区数据库的默认查询模式也设置为 **“DirectQuery 以及内存中”**。 使用此混合工作模式，您可以在对照 DirectQuery 要求验证模型的同时，继续使用导入数据的缓存，以便在模型设计过程中提高性能。  
  
 **步骤3。解决验证错误**  
  
 如果您在启用 DirectQuery 时或在添加新的数据或公式时遇到验证错误，则打开 Visual Studio 的 **“错误列表”**，然后执行所需操作。  
  
-   根据错误消息中的说明，更改针对 DirectQuery 模式的所有所需的属性设置。  
  
-   删除计算列。 如果需要特定度量值的计算列，则始终可以通过使用 "表导入向导" 中提供的 "[关系查询设计器 &#40;SSAS&#41;](relational-query-designer-ssas.md)来创建列。  
  
-   修改或删除与 DirectQuery 模式不兼容的公式。 如果您需要特定函数来进行计算，可考虑采用可通过使用 Transact-SQL 来提供等效值的方法。  
  
-   根据需要添加数据。  如果您的模型之前使用复制粘贴数据或来自 SQL Server 之外的访问接口的数据，您可以在现有连接内创建新的视图和派生列，或者使用分布式查询。  DirectQuery 模型中使用的所有数据必须可通过单个 SQL Server 数据源进行访问。  
  
 **步骤4。设置用于响应模型查询的首选方法**  
  
|||  
|-|-|  
|**仅限 DirectQuery**|将属性设置为 **DirectQuery**。|  
|**混合模式**|将属性设置为 **“内存中以及 DirectQuery”** 或 **“DirectQuery 以及内存中”**。<br /><br /> 稍后您可以更改此值以使用不同的首选项。<br /><br /> 请注意，客户端可能覆盖连接字符串中的首选方法。|  
  
 **步骤5。指定 DirectQuery 分区**  
  
|||  
|-|-|  
|**仅限 DirectQuery**|可选。 仅 DirectQuery 模型无需分区。<br /><br /> 但是，如果您在设计阶段在模型中创建了分区，请注意仅有一个分区可用作数据源。 默认情况下，创建的第一个分区将用作 DirectQuery 分区。<br /><br /> 若要确保模型所需的所有数据可以从 DirectQuery 分区中获取，请选择一个 DirectQuery 分区，并编辑 SQL 语句以获得整个数据集。|  
|**混合模式**|如果您的模型中的任意表包含多个分区，您必须选择单个分区作为“DirectQuery 分区” **。 如果您没有指派分区，则默认情况下，创建的第一个分区将用作 DirectQuery 分区。<br /><br /> 设置除 DirectQuery 以外的所有分区的处理选项。 通常，始终不处理 DirectQuery 分区，因为数据是通过关系源传递的。<br /><br /> 有关详细信息，请参阅[&#40;SSAS 表格&#41;的分区和 DirectQuery 模式](tabular-models/define-partitions-in-directquery-models-ssas-tabular.md)。|  
  
 **步骤6。配置模拟**  
  
 仅 DirectQuery 模型支持模拟。 模拟选项（ **“模拟设置”**）定义在查看来自指定的 SQL Server 数据源的数据时使用的凭据。  
  
|||  
|-|-|  
|**仅限 DirectQuery**|对于  **“模拟设置”** 属性，请指定将用于连接到 SQL Server 数据源的帐户。<br /><br /> 如果您使用值 **ImpersonateCurrentUser**，则承载该模型的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例会将模型的当前用户的凭据传递到 SQL Server 数据库。|  
|**混合模式**|对于 **“模拟设置”** 属性，请指定将用于访问 SQL Server 数据源中的数据的帐户。<br /><br /> 此设置并不影响用于处理模型使用的缓存的凭据。|  
  
 **步骤7。部署模型**  
  
 准备好部署模型时，请打开 Visual Studio 的 "**项目**" 菜单，然后选择 "**属性**"。 将 **QueryMode** 属性设置为如下表所示的值之一：  
  
 有关详细信息，请参阅[&#40;SSAS 表格&#41;中 SQL Server Data Tools 部署](tabular-models/deploy-from-sql-server-data-tools-ssas-tabular.md)。  
  
|||  
|-|-|  
|**仅限 DirectQuery**|**DirectQueryOnly**<br /><br /> 因为您仅指定了直接查询，所以，模型元数据将部署到服务器，但不对模型进行处理。<br /><br /> 请注意，将不自动删除工作区数据库使用的缓存。 如果您想要确保用户无法看到缓存数据，则最好清除设计时缓存。 有关详细信息，请参阅[清除 Analysis Services 缓存](instances/clear-the-analysis-services-caches.md)。|  
|**混合模式**|**“DirectQuery 以及内存中”**<br /><br /> **内存中的 DirectQuery**<br /><br /> 这两个值都允许您根据需要使用缓存或关系数据源。 其顺序将定义在响应针对模型的查询时默认使用哪一数据源。<br /><br /> 在混合模式中，必须在将模型元数据部署到服务器的同时处理缓存。<br /><br /> 您可以在部署后更改此设置。|  
  
 **步骤8。验证部署的模型**  
  
 在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]中，打开部署了该模型的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例。 右键单击数据库名称并选择 **“属性”**。  
  
-   当您在定义部署属性时，设置属性 **DirectQueryMode**。  
  
-   当您在定义用户模拟选项时，设置属性 **“数据源模拟信息”**。 有关详细信息，请参阅[设置模拟选项（SSAS - 多维）](multidimensional-models/set-impersonation-options-ssas-multidimensional.md)。  
  
-   在部署了模型后，您可以随时更改这些属性。  
  
##  <a name="comparing-directquery-options"></a><a name="bkmk_Configurations"></a>比较 DirectQuery 选项  
 **仅限 DirectQuery**  
 在您想要确保单个数据源时，或者您的数据太大以致内存中容纳不下时，此选项是首选选项。 如果您在设计时使用非常大的关系数据源，则可以通过使用数据的某个子集创建模型。 当您在仅 DirectQuery 模式下部署模型时，可以编辑数据源定义以包含所有所需数据。  
  
 如果您想要使用关系数据源提供的安全性来控制用户对数据的访问，此选项也是首选选项。 通过缓存的表格模型，您还可以使用 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 角色控制数据访问，但还必须确保缓存中存储的数据的安全。 如果您的安全上下文要求数据应该永远不缓存，则您应该始终使用此选项。  
  
 下表描述了有关仅 DirectQuery 模式的可能的部署结果：  
  
|||  
|-|-|  
|**无缓存的 DirectQuery**|不向缓存中加载任何数据。 永远不能处理模型。<br /><br /> 只能通过使用支持 DAX 查询的客户端对模型进行查询。 查询结果始终从原始数据源返回。<br /><br /> **DirectQueryMode** = `On`<br /><br /> **QueryMode**  = **DirectQuery**|  
|**DirectQuery 并且查询仅针对缓存**|部署失败。 不支持该配置。<br /><br /> **DirectQueryMode** = `On`<br /><br /> **QueryMode**  = **内存中**|  
  
 **混合模式**  
 在混合模式中部署您的模型具有许多好处：您可以根据需要从 SQL Server 数据源获取最新数据，但通过保留缓存，您能够使用内存中的数据以便在设计报表或测试模型时提高速度。  
  
 如果您的模型非常大，DirectQuery 混合模式也很有用。 您可以在正在进行处理时将模型切换到 DirectQuery 模式，而不是让用户获取陈旧数据或在处理缓存时让模型不可用。 用户可能会体验到速度稍慢的性能，但将能够直接从关系存储区获取数据，这确保结果是最新的。  
  
 下表比较 DirectQuery 选项的每种组合的部署结果。  
  
|||  
|-|-|  
|**缓存为首选的混合模式**|可以处理模型，并且可以将数据加载到缓存中。 默认情况下，查询使用缓存。  如果某一客户端想要使用 DirectQuery 源，则一个参数必须插入到连接字符串中。<br /><br /> **DirectQueryMode** = `On`<br /><br /> **QueryMode**  = **内存中的 DirectQuery**|  
|**DirectQuery 为首选的混合模式**|对模型进行处理，并且可以将数据加载到缓存中。 但是，查询在默认情况下使用 DirectQuery。 如果某一客户端想要使用缓存数据，则一个参数必须插入到连接字符串中。 如果对模型中的表进行了分区，则缓存的主分区也设置为 **“内存中以及 DirectQuery”**。<br /><br /> **DirectQueryMode** = `On`<br /><br /> **QueryMode**  = **DirectQuery 以及内存中**|  
  
## <a name="see-also"></a>另请参阅  
 [DirectQuery 模式 &#40;SSAS 表格&#41;](tabular-models/directquery-mode-ssas-tabular.md)   
 [表格模型数据访问](tabular-models/tabular-model-data-access.md)  
  
  
