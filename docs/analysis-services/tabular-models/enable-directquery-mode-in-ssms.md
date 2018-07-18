---
title: 启用在 SSMS 中的 DirectQuery 模式 |Microsoft 文档
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e643f90a5df9b113f2fd59a2328868131bf9c63d
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34045121"
---
# <a name="enable-directquery-mode-in-ssms"></a>在 SSMS 中启用 DirectQuery 模式
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  你可以更改已部署表格模型的数据访问属性，启用针对后端关系数据源（而不是缓存数据驻留在其中的内存）执行查询的 DirectQuery 模式。  
  
 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中，DirectQuery 配置步骤取决于模型的兼容级别。 下面是适用于所有兼容级别的步骤。  
  
 本文假定你已创建并验证在兼容性级别为 1200年或更高版本，并仅需要启用 DirectQuery 访问并更新连接字符串的内存中表格模型。 若从较低的兼容级别开始，则首先需要手动升级。 有关步骤，请参阅 [升级 Analysis Services](../../database-engine/install-windows/upgrade-analysis-services.md) 。  
  
> [!IMPORTANT]  
>  建议使用 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 而非 Management Studio 来切换数据存储模式。 当你使用  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 来更改模型，然后又进行部署到服务器的操作时，该模型与数据库将保持同步。此外，在模型中更改存储模式后，你就可以查看已发生的验证错误。 按本文说明使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 时，不报告验证错误。  
  
## <a name="requirements"></a>需求  
 在表格模型中启用 DirectQuery 模式是一个多步骤过程：  
  
-   确保模型的功能不会在 DirectQuery 模式中导致验证错误，然后将模型中的数据存储模式从内存中更改为 DirectQuery。  
  
     中记录的功能限制列表[DirectQuery 模式下](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)。  
  
-   查看已部署数据库使用的连接字符串和凭据，以便从后端外部数据库检索数据。 确保只有一个连接，且其设置适合执行查询。  
  
     不是专为 DirectQuery 设计的表格数据库可能有多个连接，这些连接现在需要根据 DirectQuery 模式的要求削减成一个。  
  
     最初用于处理数据的凭据现在将用于查询数据。 在 DirectQuery 配置过程中，请查看帐户情况并在可能情况下对帐户进行更改，以便使用不同的帐户来执行各种专用操作。  
  
     Analysis Services 仅在 DirectQuery 模式下执行受信任委派。 如果你的解决方案要求通过委派来获取特定于用户的查询结果，则必须允许用于连接到后端数据库的帐户来委派提出请求的用户的标识，而用户标识则必须具有对后端数据库的读取权限。  
  
-   最后一步是通过执行查询来确认 DirectQuery 模式是可以操作的。  
  
## <a name="step-1-check-the-compatibility-level"></a>步骤 1：查看兼容级别  
 用于定义数据访问权限的属性在不同兼容级别是不同的。 预备步骤是查看数据库属于什么兼容级别。  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中，连接到具有表格模型的实例。  
  
2.  在对象资源管理器中，右键单击数据库 >“属性” > “兼容级别”。  
  
     值可以是“SQL Server 2016 (1200)”或更早的级别，例如“SQL Server 2012 SP1 或更高版本 (1103)”。 下一步是根据兼容级别的相应说明进行操作。  
  
 将表格模型更改为 DirectQuery 模式时，新的数据存储模式会立即生效。  
  
## <a name="step-2a-switch-a-tabular-1200-database-to-directquery-mode"></a>步骤 2a：将表格 1200 数据库切换成 DirectQuery 模式  
  
1.  在对象资源管理器中，右键单击数据库 >“属性” > “模型” > “默认模式”。  
  
2.  将模式设置为“DirectQuery”。   
  
    |||  
    |-|-|  
    |**有效值**|**Description**|  
    |**DirectQuery**|将针对后端关系数据库来执行查询，使用的数据源连接是为模型定义的。<br /><br /> 系统会将对模型进行的查询转换为本机数据库查询，并将其重定向到数据源。<br /><br /> 处理已设置为 DirectQuery 模式的模型时，仅编译和部署元数据。 数据本身是在模型外部，位于操作性数据源的数据库文件中。|  
    |**导入**|将按 MDX 或 DAX 格式针对表格数据库来执行查询。<br /><br /> 处理已设置为“导入”模式的模型时，将从后端数据源检索数据并将其存储在磁盘上。 加载数据库时，会将数据整个复制到内存中进行极快速的表扫描和查询。<br /><br /> 这是表格模型的默认模式，是某些（非关系）数据源的唯一模式。|  
  
## <a name="step-2b-switch-a-tabular-1100-1103-database-to-directquery-mode"></a>步骤 2b：将表格 1100-1103 数据库切换成 DirectQuery 模式  
  
1.  在对象资源管理器中，右键单击数据库 >“属性” > “数据库” > “DirectQueryMode”。  
  
2.  将模式设置为“DirectQuery”。   
  
     默认模式属性包含下列项：  
  
    |||  
    |-|-|  
    |**有效值**|**Description**|  
    |**InMemory**|查询只使用缓存的内存中数据。|  
    |**InMemorywithDirectQuery**|查询默认使用缓存，除非在客户端的连接字符串中指定了其他项。<br /><br /> 这是一种混合模式，可将分区逐个配置为使用内存中模式或 DirectQuery 模式。|  
    |**DirectQuery**|查询仅使用关系数据源。|  
    |**DirectQuerywithInMemory**|查询默认使用关系数据源，除非在客户端的连接字符串中指定了其他项。<br /><br /> 这是一种混合模式，可将分区逐个配置为使用内存中模式或 DirectQuery 模式。|  
  
 **混合数据存储**  
  
 组合使用内存中访问和基于磁盘的访问时，缓存仍可使用，并可用于查询。 混合模式为您提供许多选项：  
  
-   在缓存和关系数据源都可用时，您可以设置首选连接方法，但最终还是客户端使用 DirectQueryMode 连接字符串属性来控制所使用的源。  
  
-   你可以将缓存上的分区配置为从不处理用于 DirectQuery 模式的主分区，并且主分区必须始终引用关系数据源。 有许多方法可以使用分区来优化模型设计和报表体验。 有关详细信息，请参阅[在 DirectQuery 模型中定义分区](../../analysis-services/tabular-models/define-partitions-in-directquery-models-ssas-tabular.md)。  
  
-   在部署了模型后，您可以更改首选连接方法。 例如，您可以使用混合模式来进行测试，并且仅在全面测试了使用该模型的所有报表或查询后，才将模型切换到“仅限 DirectQuery”  模式。 有关详细信息，请参阅[设置或更改 DirectQuery 的首选连接方法](http://msdn.microsoft.com/library/f10d5678-d678-4251-8cce-4e30cfe15751)。  
  
## <a name="step-3-check-the-connection-properties-on-the-database"></a>步骤 3：查看数据库的连接属性  
 切换为 DirectQuery 可能会更改连接的安全上下文，具体取决于数据源连接的设置情况。 更改数据访问模式时，请查看模拟和连接字符串属性，确保登录名可以用于连接到后端数据库。  
  
 查看 **Configure Analysis Services for Kerberos constrained delegation** 中的 [配置 Analysis Services 以实现可信委托](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md) 部分，了解针对 DirectQuery 方案委派用户身份时的背景信息。  
  
1.  在对象资源管理器中，展开“连接”，然后双击某个连接以查看其属性。  
  
     使用 DirectQuery 模型时，只应为数据库定义一个连接，数据源必须是关系数据源，且类型必须是支持的数据库类型。 请参阅[支持的数据源](../../analysis-services/tabular-models/data-sources-supported-ssas-tabular.md)。  
  
2.  **连接字符串** ：应指定在 DirectQuery 操作中使用的服务器、数据库名称和身份验证方法。 如果使用 SQL Server 身份验证，则可在此处指定数据库登录名。  
  
3.  **模拟信息** ：用于 Windows 身份验证。 适用于表格模型的 DirectQuery 模式的选项包括：  
  
    -   **使用服务帐户**。 如果 Analysis Services 服务帐户具有对关系数据库的读取权限，则可选择此选项。  
  
    -   **使用特定用户名和密码**。 指定 Windows 用户帐户，该帐户具有对关系数据库的读取权限。  
  
 请注意，这些凭据仅用于响应针对关系数据存储区的查询；它们与用于处理混合模型的缓存的凭据不同。  
  
 当模型仅用于内存中时，不能使用模拟。 **ImpersonateCurrentUser**设置无效，除非模型正在使用 DirectQuery 模式。  
  
## <a name="step-4-validate-directquery-access"></a>步骤 4：验证 DirectQuery 访问  
  
1.  在连接到 SQL Server 上的关系数据库的 Management Studio 中使用 SQL Server Profiler 或 xEvents 启动一个跟踪。  
  
     如果你使用的是 Oracle 或 Teradata，请使用适合这些数据库平台的跟踪工具。  
  
2.  在 Management Studio 中，输入并执行简单的 MDX 查询，例如 `select <some measure> on 0 from model.`。  
  
3.  在跟踪中，你会看到针对关系数据库执行查询的证据。  
  
## <a name="see-also"></a>另请参阅  
 [兼容性级别](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)   
 [支持的数据源](../../analysis-services/tabular-models/data-sources-supported-ssas-tabular.md)   
 [扩展的事件](../../relational-databases/extended-events/extended-events.md)   
 [监视 Analysis Services 实例](../../analysis-services/instances/monitor-an-analysis-services-instance.md)  
  
  
