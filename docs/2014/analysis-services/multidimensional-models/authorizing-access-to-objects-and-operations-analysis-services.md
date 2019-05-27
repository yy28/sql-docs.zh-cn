---
title: 授权访问权限的对象和操作 (Analysis Services) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.roledesignerdialog.membership.f1
- sql12.asvs.roledesignerdialog.general.f1
helpviewer_keywords:
- access rights [Analysis Services], users
- permissions [Analysis Services], users
- security [Analysis Services], user access
- user access rights [Analysis Services]
- granting permissions [Analysis Services], users
ms.assetid: af28524e-5eca-4dce-a050-da4f406ee1c7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d6962452b5615b9b2607007ed86c09eed495f6f1
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66077015"
---
# <a name="authorizing-access-to-objects-and-operations-analysis-services"></a>授予对对象和操作的访问权限 (Analysis Services)
  非管理用户对 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库内的多维数据集、维度和挖掘模型的访问权限可通过一个或多个数据库角色的成员身份获得。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 管理员创建这些数据库角色，从而授予对 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象的读取或读/写权限，然后向每个角色分配 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 用户和组。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 通过将与用户或组所属的每个数据库角色关联的权限组合起来，以此确定特定 Windows 用户或组的有效权限。 因此，如果一个数据库角色没有授予用户或组对维度、度量值或属性的查看权限，但另一个数据库角色授予了该用户或组此项权限，则该用户或组将有权查看对象。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务器管理员角色的成员和具有“完全控制”（管理员）权限的数据库角色成员可以访问数据库中的所有数据和元数据，并且查看特定对象时无需额外权限。 而且，不能拒绝 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务器角色的成员访问任何数据库中任何对象，也不能拒绝在数据库中具有“完全控制”（管理员）权限的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库角色的成员访问该数据库中的任何对象。 可通过具有较少权限的单独角色对专门的管理操作（如处理）进行授权。 有关详细信息，请参阅[授予处理权限 (Analysis Services)](grant-process-permissions-analysis-services.md)。  
  
## <a name="list-roles-defined-for-your-database"></a>列出为你的数据库所定义的角色  
 管理员可以在 SQL Server Management Studio 中运行一个简单的 DMV 查询，获取在服务器上定义的全部角色的列表。  
  
1.  在 SSMS 中，右键单击某个数据库，然后选择**新查询** | **MDX**。  
  
2.  键入以下查询并按下 F5 执行：  
  
    ```  
    Select * from $SYSTEM.DBSCHEMA_CATALOGS  
    ```  
  
     结果包括数据库名称、说明、角色名称和上次修改的日期。 将此信息用作起点，你可以继续进入到单独数据库以检查特定角色的成员身份和权限。  
  
## <a name="top-down-overview-of-analysis-services-authorization"></a>Analysis Services 授权的自上而下的概述  
 本节涵盖了配置权限的基本工作流。  
  
 **步骤 1：服务器管理**  
  
 作为第一步，请决定谁将具有服务器级别的管理员权限。 安装过程中，安装 SQL Server 的本地管理员根据要求需指定一个或多个 Windows 账户作为 Analysis Services 服务器管理员。 服务器管理员具有对服务器的全部可能的权限，包括查看、修改和删除服务器上的任何对象，或查看关联数据的权限。 安装完成后，服务器管理员可以添加或删除账户以更改此角色的成员身份。 请参阅[授予服务器管理员权限&#40;Analysis Services&#41; ](../instances/grant-server-admin-rights-to-an-analysis-services-instance.md)有关此权限级别的详细信息。  
  
 **步骤 2：数据库管理**  
  
 接下来，创建了表格或多维解决方案后，将其作为数据库部署至服务器。 服务器管理员可以通过定义具有对所讨论数据库的完全控制权限的角色来委托数据库管理任务。 此角色的成员可以处理或查询该数据库中的对象，以及创建其他角色以访问数据库自身内的多维数据集、维度和其他对象。 有关详细信息，请参阅[授予数据库权限 (Analysis Services)](grant-database-permissions-analysis-services.md)。  
  
 **步骤 3：启用多维数据集或模型访问以查询和处理工作负荷**  
  
 默认情况下，仅服务器和数据库管理员拥有对多维数据集或表格模型的访问权限。 将这些数据结构提供给组织中的其他人员需要能够将 Windows 用户和组帐户映射到多维数据集或模型的其他角色分配以及可以指定 `Read` 特权的权限。 有关详细信息，请参阅[授予多维数据集或模型权限 (Analysis Services)](grant-cube-or-model-permissions-analysis-services.md)。  
  
 处理任务可与其他管理功能隔离，允许服务器和数据库管理员将此任务委派给其他人员，或通过指定运行计划软件的服务帐户配置无人参与的处理。 有关详细信息，请参阅[授予处理权限 (Analysis Services)](grant-process-permissions-analysis-services.md)。  
  
> [!NOTE]  
>  用户不需要对基础关系数据库（ [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 从该数据库加载其数据）中的关系表的任何权限，也不需要对运行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的计算机的任何文件级别权限。  
  
 **步骤 4 （可选）：允许或拒绝访问内部多维数据集对象**  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 为设置单个对象的权限提供了安全设置，其中包括数据模型中的维度成员和单元。 有关详细信息，请参阅[授予对维度数据的自定义访问权限 (Analysis Services)](grant-custom-access-to-dimension-data-analysis-services.md) 和[授予单元格数据的自定义访问权限 (Analysis Services)](grant-custom-access-to-cell-data-analysis-services.md)。  
  
 你还可以根据用户标识更改权限。 通常这称为动态安全，可使用 [UserName (MDX)](/sql/mdx/username-mdx) 函数实现  
  
## <a name="best-practices"></a>最佳做法  
 要更好地管理权限，建议采取类似于以下所述的方法：  
  
1.  按函数（例如，dbadmin、cubedeveloper、processadmin）创建角色，这样，维护这些角色的任何人都可以一眼看出角色所允许的权限。 正如其他地方所述，你可以在模型定义中定义角色，从而在后续解决方案的部署中保留这些角色。  
  
2.  在 Active Directory 中创建相应的 Windows 安全组，然后在 Active Directory 中维护此安全组，确保它包含适当的个人帐户。 这就使安全组的成员身份的责任落实到熟悉组织中用于帐户维护的工具和流程的安全专家身上。  
  
3.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中生成脚本，这样，当模型从其源文件重新部署到服务器时就可以快速复制角色分配。 有关如何快速生成脚本的详细信息，请参阅[授予多维数据集或模型权限 (Analysis Services)](grant-cube-or-model-permissions-analysis-services.md)。  
  
4.  采用反映角色范围和成员身份的命名约定。 只有在设计和管理工具中才能看到角色名，因此请使用适合多维数据集安全专家的命名约定。 例如， **processadmin-windowsgroup1** 表示组织中人员的读取访问和处理权限，他们的个人 Windows 用户帐户是 **windowsgroup1** 安全组的成员。  
  
     包含帐户信息有助于跟踪各种角色中所用的帐户。 由于角色可累加，因此与 **windowsgroup1** 关联的组合角色构成了为属于该安全组的人员设置的有效权限。  
  
5.  多维数据集开发人员需具有对开发中的模型和数据库的“完全控制”权限，但当数据库推广到生产服务器后，只需具有“读取”权限即可。 请务必为所有方案（包括开发、测试和生产部署）开发角色定义和分配。  
  
 使用与此类似的方法最大限度减少改动模型中的角色定义和角色成员身份，使角色分配可视化，从而轻松实现和维护多维数据集权限。  
  
## <a name="see-also"></a>请参阅  
 [授予服务器管理员权限&#40;Analysis Services&#41;](../instances/grant-server-admin-rights-to-an-analysis-services-instance.md)   
 [角色和权限 (Analysis Services)](roles-and-permissions-analysis-services.md)   
 [Analysis Services 支持的身份验证方法](../instances/authentication-methodologies-supported-by-analysis-services.md)  
  
  
