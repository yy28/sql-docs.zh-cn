---
title: 授予对存储过程的权限（Analysis Services） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 01793166-a3e5-4856-8302-21b82d494e69
author: minewiskan
ms.author: owend
ms.openlocfilehash: 960b0ef3f050b780998a0f86dcd7b7edf121676d
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84544309"
---
# <a name="grant-permissions-on-stored-procedures-analysis-services"></a>授予对存储过程的权限 (Analysis Services)
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中的存储过程或程序集是使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] .NET 编程语言编写的外部例程，扩展了 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 的功能。 通过程序集，开发人员可以利用跨语言集成、异常处理、版本支持、部署支持以及调试支持。  
  
 你必须是服务器管理员才能注册程序集。 请参阅[&#40;Analysis Services&#41;授予服务器管理员权限](instances/grant-server-admin-rights-to-an-analysis-services-instance.md)。  
  
## <a name="security-context-for-stored-procedure-execution"></a>存储过程执行的安全上下文  
 任何用户都可以调用存储过程。 根据存储过程配置方式的不同，该过程既可以在调用它的用户的上下文中运行，也可以在匿名用户的上下文中运行。 由于匿名用户没有安全上下文，因此可使用此功能将 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例配置为允许进行匿名访问。  
  
 在用户调用存储过程之后但在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 运行存储过程之前，[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 会评估存储过程内的操作。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 根据授予用户的权限和用于运行过程的权限集的交集来评估存储过程内的操作。 如果存储过程包含任意无法由用户的数据库角色执行的操作，则不会执行该操作。  
  
 下面便是用于运行存储过程的权限集：  
  
-   **Safe**使用 Safe 权限集，存储过程无法访问 .NET Framework 中的受保护资源 [!INCLUDE[msCoName](../includes/msconame-md.md)] 。 此权限集仅允许执行计算。 它是最安全的权限集；不会将信息泄露到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 之外，不能评估权限，并且最大限度地减低了数据篡改攻击的风险。  
  
-   **外部访问**使用外部访问权限集，存储过程可以使用托管代码访问外部资源。 将存储过程设置为此权限集不会导致可引起服务器不稳定的编程错误。 但是，此权限集可能导致信息泄露到服务器之外，并可能导致权限提升以及数据篡改攻击。  
  
-   **无限制**使用无限制权限集，存储过程可以使用任何代码访问外部资源。 在使用此权限集时，存储过程没有安全性或可靠性保证。  
  
## <a name="see-also"></a>另请参阅  
 [多维模型程序集管理](multidimensional-models/multidimensional-model-assemblies-management.md)  
  
  
