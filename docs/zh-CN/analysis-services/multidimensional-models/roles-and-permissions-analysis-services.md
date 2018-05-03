---
title: 角色和权限 (Analysis Services) |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1791061952a2e003ed88b4d17c7f57539d3ea763
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="roles-and-permissions-analysis-services"></a>角色和权限 (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]提供授予对操作、 对象和数据访问权限的基于角色的授权模型。 访问 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例或数据库的所有用户都必须在某一角色范畴内执行操作。  
  
 作为 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 系统管理员，你将负责将成员身份授予 **服务器管理员角色** ，从而提供对服务器上的操作不受限制的访问权限。 此角色具有固定权限，不能自定义。 默认情况下，本地 Administrators 组的成员将自动是 Analysis Services 系统管理员。  
  
 执行查询或处理数据的非管理用户通过 **数据库角色**获得访问权限。 系统管理员和数据库管理员都可以创建描述给定数据库内不同访问级别的角色，然后将成员身份分配给要求访问的每个用户。 每个角色都有一组自定义的权限，用于访问特定数据库内的对象和操作。 您可以在以下级别分配权限：数据库、内部对象（例如多维数据集和维度，但不包括透视）和行。  
  
 创建角色和分配成员身份通常将作为单独的操作。 通常情况下，模型设计者在设计阶段添加角色。 这样，所有角色定义都将反映在定义该模型的项目文件中。 角色成员身份通常在以后在数据库进入生产阶段时实现，并且通常由创建了可被开发、测试和作为独立操作运行的脚本的数据库管理员执行。  
  
 所有授权都基于有效的 Windows 用户标识。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 使用专用于验证用户身份的 Windows 身份验证。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]提供任何专有身份验证方法。请参阅[Analysis Services 支持的身份验证方法](../../analysis-services/instances/authentication-methodologies-supported-by-analysis-services.md)。  
  
> [!IMPORTANT]  
>  在数据库中的所有角色中，对于每个 Windows 用户或组，权限都是可以累加的。 如果某个角色拒绝用户或用户组执行特定任务或查看特定数据的权限，但是另一个角色为该用户或用户组授予相应的执行或查看权限，则该用户或用户组将具有执行任务或查看数据的权限。  
  
## <a name="in-this-section"></a>在本节中  
  
-   [授权访问对象和操作 & #40;Analysis Services & #41;](../../analysis-services/multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md)  
  
-   [Grant 数据库权限 & #40;Analysis Services & #41;](../../analysis-services/multidimensional-models/grant-database-permissions-analysis-services.md)  
  
-   [授予多维数据集或模型权限 & #40;Analysis Services & #41;](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md)  
  
-   [授予处理权限 & #40;Analysis Services & #41;](../../analysis-services/multidimensional-models/grant-process-permissions-analysis-services.md)  
  
-   [授予读取定义权限对象元数据 & #40;Analysis Services & #41;](../../analysis-services/multidimensional-models/grant-read-definition-permissions-on-object-metadata-analysis-services.md)  
  
-   [授予对数据源对象 & #40; 的权限Analysis Services & #41;](../../analysis-services/multidimensional-models/grant-permissions-on-a-data-source-object-analysis-services.md)  
  
-   [授予对数据挖掘结构和模型 & #40; 的权限Analysis Services & #41;](../../analysis-services/multidimensional-models/grant-permissions-on-data-mining-structures-and-models-analysis-services.md)  
  
-   [授予对维度 & #40; 的权限Analysis Services & #41;](../../analysis-services/multidimensional-models/grant-permissions-on-a-dimension-analysis-services.md)  
  
-   [授予维度数据 & #40; 的自定义访问权限Analysis Services & #41;](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md)  
  
-   [授予单元数据 & #40; 的自定义访问权限Analysis Services & #41;](../../analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services.md)  
  
## <a name="see-also"></a>另请参阅  
 [创建和管理角色](../../analysis-services/tabular-models/create-and-manage-roles-ssas-tabular.md)  
  
  
