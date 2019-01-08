---
title: 使用基于策略的管理来管理服务器 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- facet See facets
- Declarative Management Framework See Policy-Based Management
- surface area configuration [SQL Server], Policy-Based Management
- Policy-Based Management
- facets [Policy-Based Management]
- Policy-Based Management, administering
- conditions [Policy-Based Management]
- facets [Policy-Based Management], about facets
- PolicyAdministratorRole role
ms.assetid: ef2a7b3b-614b-405d-a04a-2464a019df40
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: cb9d48156ecd1ca98dc36c10c2680883160582c1
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/13/2018
ms.locfileid: "53377479"
---
# <a name="administer-servers-by-using-policy-based-management"></a>使用基于策略的管理来管理服务器
  基于策略的管理是一种用于管理一个或多个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的系统。 当 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 策略管理员使用基于策略的管理时，他们使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 创建策略以管理服务器上的实体，例如，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例、数据库或其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对象。  
  
## <a name="benefits-of-policy-based-management"></a>基于策略的管理的优点  
 基于策略的管理有助于解决在以下情况下出现的问题：  
  
-   公司策略禁止启用数据库邮件或 SQL Mail。 创建了一个策略以检查这两个功能的服务器状态。 管理员将服务器状态与策略进行比较。 如果服务器状态不符合策略，管理员将选择“配置”模式，并且使服务器状态符合策略。  
  
-   [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库的命名约定要求所有存储过程以字母 AW_ 开头。 创建了一个策略以强制实施此策略。 管理员对此策略进行测试，并找到一组不符合策略的存储过程。 如果将来的存储过程不符合此命名约定，这些存储过程的创建语句将会失败。  
  
> [!NOTE]  
>  注意策略会影响某些 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能的工作方式。 例如，变更数据捕捉和事务复制都使用没有索引的 systranschemas 表。 如果启用所有表都必须有索引的策略，则强制策略的兼容会导致这些功能都失效。  
  
 策略是使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]创建和管理的。 此过程包括以下步骤：  
  
1.  选择一个基于策略的管理方面，其中包含要配置的属性。  
  
2.  定义一个条件以指定管理方面状态。  
  
3.  定义一个策略，其中包含该条件、用于筛选目标集的附加条件以及评估模式。  
  
4.  检查 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例是否符合该策略。  
  
 对于失败的策略，对象资源管理器以红色图标的形式指示严重运行状态警告，此图标位于该目标以及对象资源管理器树中此目标上面的节点旁边。  
  
> [!NOTE]  
>  在系统计算某一策略的对象集时，默认情况下将排除系统对象。  例如，如果该策略的对象集引用所有表，则该策略将不适用于系统表。 如果用户想要评估针对系统对象的策略，可以显式向对象集添加系统对象。 但是，尽管 **“按计划检查”** 评估模式支持所有策略，但出于性能原因， **“更改时检查”** 并不支持具有任意对象集的所有策略。 有关详细信息，请参阅 [https://blogs.msdn.com/b/sqlpbm/archive/2009/04/13/policy-evaluation-modes.aspx](https://blogs.msdn.com/b/sqlpbm/archive/2009/04/13/policy-evaluation-modes.aspx)  
  
## <a name="policy-based-management-concepts"></a>基于策略的管理概念  
 基于策略的管理包含以下三个组件：  
  
-   策略管理  
  
     策略管理员创建策略。  
  
-   显式管理  
  
     管理员选择一个或多个管理目标，并显式地检查这些目标是否符合特定策略，或者显式地使这些目标符合策略。  
  
-   评估模式  
  
     共有四种评估模式，其中的三种模式可以自动执行：  
  
    -   **按需**。 当此模式由用户直接指定时，将对策略进行评估。  
  
    -   **更改时: 禁止**。 这种自动模式使用 DDL 触发器来防止违反策略。  
  
        > [!IMPORTANT]  
        >  如果禁用了嵌套触发器服务器配置选项，“更改时: 禁止”将不会正常工作。 基于策略的管理依靠 DDL 触发器来检测和回滚不符合使用此评估模式的策略的 DDL 操作。 删除基于策略的管理 DDL 触发器或禁用嵌套触发器将导致此评估模式失败或意外执行。  
  
    -   **更改时: 仅记录**。 当做出相关更改时，这种自动模式使用事件通知对策略进行评估。  
  
    -   **按计划**。 这种自动模式使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业定期对策略进行评估。  
  
     在未启用自动策略时，基于策略的管理不会影响系统性能。  
  
## <a name="policy-based-management-terms"></a>基于策略的管理术语  
 基于策略的管理目标  
 基于策略的管理所管理的实体，例如，[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]实例、数据库、表或索引。 服务器实例中的所有目标构成了目标层次结构。 目标集是将一组目标筛选器应用于目标层次结构后得到的一组目标，例如，HumanResources 架构所拥有的数据库中的所有表。  
  
 基于策略的管理方面  
 一组逻辑属性，用于模拟某些类型的管理目标的行为或特征。 这些属性的数量和特征内置在方面中，只能由方面创建者添加或删除这些内容。 一种目标类型可以实现一个或多个管理方面，而一个管理方面可以由一种或多种目标类型进行实现。 方面的某些属性仅适用于特定版本。  
  
 基于策略的管理条件  
 一个布尔表达式，用于针对管理方面指定基于策略的管理托管目标的一组允许状态。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在评估条件时尝试遵守排序规则。 当 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 排序规则与 Windows 排序规则不完全匹配时，请测试您的条件，以确定该算法如何解决冲突。  
  
 基于策略的管理策略  
 基于策略的管理条件和预期行为，例如，评估模式、目标筛选器以及计划。 每个策略只能包含一个条件。 您可以启用或禁用策略。 策略存储在 msdb 数据库中。  
  
 基于策略的管理策略类别  
 用于帮助管理策略的用户定义类别。 用户可以将策略划分到不同的策略类别。 每个策略属于一个策略类别，且仅属于一个策略类别。 策略类别应用于数据库和服务器。 在数据库级别，应用以下条件：  
  
-   数据库所有者可以为数据库订阅一组策略类别。  
  
-   仅订阅类别中的策略能够控制数据库。  
  
-   所有数据库隐式订阅默认策略类别。  
  
 在服务器级别，策略类别可以应用于所有数据库。  
  
 有效策略  
 目标的有效策略是那些控制此目标的策略。 仅当满足所有以下条件时，策略才对目标有效：  
  
-   已启用此策略。  
  
-   目标属于此策略的目标集。  
  
-   目标或目标祖先之一订阅了包含此策略的策略组。  
  
## <a name="policy-based-management-tasks"></a>基于策略的管理任务  
 基于策略的管理是一个基于策略的系统，用于管理一个或多个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例。 可以使用基于策略的管理来创建包含条件表达式的条件。 然后创建一些策略，将这些条件应用于数据库目标对象。  
  
|任务说明|主题|  
|----------------------|-----------|  
|介绍如何存储基于策略的管理策略。|基于策略的管理存储|  
|介绍如何配置警报以通知策略管理员策略失败情况。|[配置警报以通知策略管理员策略失败情况](configure-alerts-to-notify-policy-administrators-of-policy-failures.md)|  
|介绍如何创建、查看、修改和删除基于策略的管理条件。|[创建新的基于策略的管理条件](create-a-new-policy-based-management-condition.md)<br /><br /> [删除基于策略的管理条件](delete-a-policy-based-management-condition.md)<br /><br /> [查看或修改基于策略的管理条件的属性](view-or-modify-the-properties-of-a-policy-based-management-condition.md)|  
|介绍如何创建、查看、修改和删除基于策略的管理策略。|[创建基于策略的管理策略](create-a-policy-based-management-policy.md)<br /><br /> [删除基于策略的管理策略](delete-a-policy-based-management-policy.md)<br /><br /> [查看或修改基于策略的管理策略的属性](view-or-modify-the-properties-of-a-policy-based-management-policy.md)|  
|介绍如何导出和导入基于策略的管理策略。|[导出基于策略的管理策略](export-a-policy-based-management-policy.md)<br /><br /> [导入基于策略的管理策略](import-a-policy-based-management-policy.md)|  
|介绍如何验证服务器实例、数据库、服务器对象或数据库对象符合策略。|[评估来自对象的基于策略的管理策略](evaluate-a-policy-based-management-policy-from-an-object.md)<br /><br /> [从基于策略的管理策略评估该策略](evaluate-a-policy-based-management-policy-from-that-policy.md)<br /><br /> [定期评估基于策略的管理策略](evaluate-a-policy-based-management-policy-on-a-schedule.md)|  
|介绍如何查看基于策略的管理方面状态并将其复制到文件中。|[使用基于策略的管理方面](working-with-policy-based-management-facets.md)|  
|提供一组可以作为最佳实践策略导入的策略文件，然后介绍如何针对包含实例、实例对象、数据库或数据库对象的目标集评估策略。|[使用基于策略的管理来监视和强制执行最佳做法](monitor-and-enforce-best-practices-by-using-policy-based-management.md)|  
|提供 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中对象资源管理器的“策略管理”节点的 F1 帮助主题。|[策略管理节点&#40;对象资源管理器&#41;](../../ssms/object/object-explorer.md)|  
  
## <a name="see-also"></a>请参阅  
 [基于策略的管理视图 (Transact-SQL)](/sql/relational-databases/system-catalog-views/policy-based-management-views-transact-sql)  
  
  
