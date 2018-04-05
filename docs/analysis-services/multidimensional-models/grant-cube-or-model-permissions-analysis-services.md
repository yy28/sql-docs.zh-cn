---
title: 授予多维数据集或模型权限 (Analysis Services) |Microsoft 文档
ms.custom: ''
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.asvs.roledesignerdialog.cubes.f1
helpviewer_keywords:
- user access rights [Analysis Services], cubes
- cubes [Analysis Services], security
- read/write permissions
- permissions [Analysis Services], cubes
ms.assetid: 55b1456e-2f6b-4101-b316-c926f40304e3
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: e15e73da6c4c4a064a6730873dd866b87d5727d6
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="grant-cube-or-model-permissions-analysis-services"></a>授予多维数据集或模型权限 (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]多维数据集或表格模型是 Analysis Services 数据模型中的主要查询对象。 为进行即席数据浏览从 Excel 连接到多维或表格数据时，用户通常选择一个特定多维数据集或表格模型作为透视报表对象背后的数据结构，以此开始。 本主题说明了如何授予对多维数据集或表格数据的访问权限。  
  
 默认情况下，无人（“服务器管理员”或“数据库管理员”除外）具有在数据库中查询多维数据集的权限。 非管理员访问多维数据集需要具备为包含此多维数据集的数据库创建的角色中的成员身份。 支持 Windows 用户或组帐户的成员身份，在 Active Directory 中或本地计算机上定义成员身份。 开始前，确定将向哪些帐户分配要创建的角色的成员身份。  
  
 具有对多维数据集的 **Read** 访问权限也就具有了对其中维度、度量值组和透视的权限。 大多管理员将授予单元级的读取权限并限制对特定对象、关联数据的权限，或根据用户身份限制权限。  
  
 要为连续的解决方案部署保留角色定义，最佳做法是将 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 中的角色定义为该模型的一个组成部分，然后让数据库管理员在数据库发布后在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中分配角色成员身份。 但可以对两个任务使用两个工具中的任一个。 为简化该练习，我们将同时对角色定义和成员身份使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 。  
  
> [!NOTE]  
>  只有具有“完全控制”权限的服务器管理员或数据库管理员可以将多维数据集从源文件部署到服务器，或创建角色和分配成员。 有关这些权限级别的详细信息，请参阅[向 Analysis Services 实例授予服务器管理员权限](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md)和[授予数据库权限 (Analysis Services)](../../analysis-services/multidimensional-models/grant-database-permissions-analysis-services.md)。  
  
#### <a name="step-1-create-the-role"></a>步骤 1：创建角色  
  
1.  在 SSMS 中，连接到 Analysis Services。 如果需要此步骤的帮助，请参阅[从客户端应用程序进行连接 (Analysis Services)](../../analysis-services/instances/connect-from-client-applications-analysis-services.md)。  
  
2.  在“对象资源管理器”中打开“数据库”  文件夹并选择一个数据库。  
  
3.  右键单击“角色”，然后选择“新角色”。 请注意，角色在数据库级别创建并应用于其范围内的对象。 你无法在数据库之间共享角色。  
  
4.  在“常规”  窗格中输入名称和（可选）描述。 此窗格也包含多个数据库权限，如完全控制、处理数据库和读取定义。 查询多维数据集或表格模型不需要这些权限。 有关这些权限的详细信息，请参阅[授予数据库权限 (Analysis Services)](../../analysis-services/multidimensional-models/grant-database-permissions-analysis-services.md)。  
  
5.  输入名称和（可选）描述后继续下一个步骤。  
  
#### <a name="step-2-assign-membership"></a>步骤 2：分配成员身份  
  
1.  在“成员身份”  窗格中，单击“添加”  以输入将使用此角色访问多维数据集的 Windows 用户或组帐户。 Analysis Services 仅支持 Windows 安全标识。 请注意，在此步骤中不创建数据库登录。 在 Analysis Services 中，用户通过 Windows 帐户进行连接。  
  
2.  继续下一个步骤“设置多维数据集权限”。  
  
     请注意，我们将跳过“数据源”窗格。 Analysis Services 数据的多数常规使用者无需具备对数据源对象的权限。 有关这些权限级别的详细信息，请参阅 [授予数据源对象的权限 (Analysis Services)](../../analysis-services/multidimensional-models/grant-permissions-on-a-data-source-object-analysis-services.md) 。  
  
#### <a name="step-3-set-cube-permissions"></a>步骤 3：设置多维数据集权限  
  
1.  在“多维数据集”窗格中，选择一个多维数据集，然后单击“读取”或“读/写”访问权限。  
  
     “读取” 权限已经足以进行多数操作。 “读/写”仅用于回写，而非处理。 有关此功能的详细信息，请参阅 [Set Partition Writeback](../../analysis-services/multidimensional-models/set-partition-writeback.md) 。  
  
     请注意，你可以选择多个多维数据集以及“创建角色”对话框中的其他可选对象。 授予对多维数据集的权限也就授予了对与此多维数据集关联的维度和透视的权限。 无需手动添加此多维数据集中已存在的对象。  
  
     如果要根据对象或用户改变授权，例如：要使某些度量值不可用，可以用原子方式允许或拒绝对特定对象（甚至对单元）的访问权限。 有关详细信息，请参阅[授予对维度数据的自定义访问权限 (Analysis Services)](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md) 和[授予单元数据的自定义访问权限 (Analysis Services)](../../analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services.md)。  
  
2.  此时，单击“确定” 后，此角色的所有成员均具有对这些多维数据集的访问权限，权限级别为你所指定。  
  
     请注意，在“多维数据集”  窗格上，你可以通过“钻取和本地多维数据集” 向用户授予从服务器多维数据集创建本地多维数据集的权限，或者通过“钻取”  权限仅允许钻取。  
  
     最后，此窗格使你可以授予对该多维数据集的“处理数据库”  权限，从而给予此角色所有成员处理此多维数据集的能力。 由于处理通常是受限操作，我们建议将此任务交由管理员来完成，或为此任务专门定义单独的角色。 有关处理权限最佳做法的详细信息，请参阅[授予处理权限 (Analysis Services)](../../analysis-services/multidimensional-models/grant-process-permissions-analysis-services.md)。  
  
#### <a name="step-4-test"></a>步骤 4：测试  
  
1.  使用 Excel 测试多维数据集访问权限。 你也可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，接着使用后述方法：作为非管理员用户运行应用程序。  
  
    > [!NOTE]  
    >  如果你是一名 Analysis Services 管理员，管理员权限将与具有较低权限的角色相结合，这使得单独测试角色权限变得困难。 要简化测试，我们建议使用分配给正在测试的角色的帐户，打开 SSMS 的第二个实例。  
  
2.  按住 Shift 键并右键单击 **Excel** 快捷方式，以便访问“以其他用户身份运行”选项。 输入一个具有此角色成员身份的 Windows 用户或组帐户。  
  
3.  Excel 打开时，使用“数据”选项卡连接到 Analysis Services。 由于你是作为不同的 Windows 用户运行 Excel，因此“使用 Windows 身份验证”  选项是测试角色时应使用的正确凭据类型。 如果需要此步骤的帮助，请参阅[从客户端应用程序进行连接 (Analysis Services)](../../analysis-services/instances/connect-from-client-applications-analysis-services.md)。  
  
     如果连接发生错误，请检查 Analysis Services 的端口配置并验证服务器接受远程连接。 有关端口配置的信息，请参阅 [将 Windows 防火墙配置为允许 Analysis Services 访问](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md) 。  
  
#### <a name="step-5-script-role-definition-and-assignments"></a>步骤 5：脚本角色定义和分配  
  
1.  作为最后一步，应生成一个捕捉刚才创建的角色定义的脚本。  
  
     从 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 重新部署一个项目将覆盖任何不是在项目内定义的角色或角色成员身份。 在重新部署后重新生成角色和角色成员身份的最快方式是通过脚本。  
  
2.  在 SSMS 中，导航到“角色”文件夹，右键单击一个现有角色。  
  
3.  选择“编写角色脚本为” | “CREATE TO” | “文件”。  
  
4.  以 .xmla 文件扩展名保存文件。 要测试脚本，删除当前角色，在 SSMS 中打开文件，按 F5 执行该脚本。  
  
## <a name="next-step"></a>下一步  
 你可以优化多维数据集权限来限制对单元或纬度数据的访问。 有关详细信息，请参阅[授予对维度数据的自定义访问权限 (Analysis Services)](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md) 和[授予单元数据的自定义访问权限 (Analysis Services)](../../analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services.md)。  
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 支持的身份验证方法](../../analysis-services/instances/authentication-methodologies-supported-by-analysis-services.md)   
 [授予对数据挖掘结构和模型 &#40; 的权限Analysis Services &#41;](../../analysis-services/multidimensional-models/grant-permissions-on-data-mining-structures-and-models-analysis-services.md)   
 [授予数据源对象的权限 (Analysis Services)](../../analysis-services/multidimensional-models/grant-permissions-on-a-data-source-object-analysis-services.md)  
  
  
