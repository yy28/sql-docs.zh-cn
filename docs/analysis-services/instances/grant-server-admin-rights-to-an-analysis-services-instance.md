---
title: 授予对 Analysis Services 实例的服务器管理员权限 |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e437507d139959c21f723f8a674ca4879570339f
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/26/2018
ms.locfileid: "50145672"
---
# <a name="grant-server-admin-rights-to-an--analysis-services-instance"></a>向 Analysis Services 实例授予服务器管理员权限
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  对于 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例中的所有 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象和数据，该实例中的服务器管理员角色的成员具有无限访问权限。 用户必须是服务器管理员角色的成员才能执行任何服务器范围内的任务，如创建或处理数据库、修改服务器属性或启动跟踪（处理事件除外）。  
  
 安装 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 时将建立角色成员身份。 运行安装程序的用户可以将自己添加到该角色，或添加其他用户。 必须指定至少一个管理员，安装程序才能继续。  
  
 默认情况下，还将为本地 Administrators 组的成员授予 Analysis Server 中的管理权限。 虽然未显式授予本地组 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务管理员角色中的成员身份，但是本地管理员可创建数据库、添加用户和权限以及执行系统管理员允许的任何其他任务。 管理员权限的隐式授权可配置。 它由 **BuiltinAdminsAreServerAdmins** 服务器属性确定，该属性默认情况下设置为 **true** 。 您可在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中更改此属性。 有关详细信息，请参阅 [Security Properties](../../analysis-services/server-properties/security-properties.md)。  
  
 安装后，可以修改角色成员身份，以添加需要对该服务拥有完全权限的任何其他用户。 您还可以使用分析管理对象 (AMO) 来管理服务器角色。 有关详细信息，请参阅[使用分析管理对象 (AMO) 进行开发](https://docs.microsoft.com/bi-reference/amo/developing-with-analysis-management-objects-amo)。  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 提供粒度越来越细的角色在服务器、数据库和对象级处理和查询的进度。 有关如何使用这些角色的说明，请参阅[角色和权限 (Analysis Services)](../../analysis-services/multidimensional-models/roles-and-permissions-analysis-services.md)。  
  
## <a name="modify-server-role-membership"></a>修改服务器角色成员身份  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，连接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例，在对象资源管理器中右键单击实例名称，然后单击“属性”。  
  
2.  在 **“选择页”** 窗格中单击 **“安全性”** ，然后单击页底部的 **“添加”** 以将一个或多个 Windows 用户或组添加到服务器角色中。  
  
     ![在 management studio 中的添加用户对话框](../../analysis-services/instances/media/ssas-serveradminadd.png "在 management studio 中的添加用户对话框")  
  
### <a name="add-computer-accounts"></a>添加计算机帐户  
 可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 让计算机帐户成为 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 管理员组的成员。  
  
1.  在“选择用户或组”  对话框中，单击“位置” 。  
  
2.  选择你要添加的计算机是其成员的域，或者选择“整个目录”  ，然后单击“确定” 。  
  
3.  单击 **“对象类型”**。  
  
4.  单击“计算机”  ，并单击“确定” 。  
  
     ![将计算机帐户添加为 ssas 管理员](../../analysis-services/instances/media/ssas-in-ssms-computerobjects.png "将计算机帐户添加为 ssas 管理员")  
  
5.  在“输入选择的对象名称”  文本框中，键入计算机名称，然后单击“检查名称”  以验证当前位置是否有该计算机帐户。 如果找不到该计算机帐户，请验证计算机名称以及该计算机是其成员的正确域。  
  
## <a name="nt-servicessastelemetry-account"></a>NT Service\SSASTelemetry 帐户  
 “NT Service/SSASTelemetry”是在安装过程中创建的低特权计算机帐户，专门用于运行客户体验改善计划 (CEIP) 服务的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实现。 此服务需要 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的管理员权限来运行多个发现命令。 有关详细信息，请参阅 [Customer Experience Improvement Program for SQL Server Data Tools](../../sql-server/customer-experience-improvement-program-for-sql-server-data-tools.md) 和 [Microsoft SQL Server Privacy Statement](http://go.microsoft.com/fwlink/?LinkID=868444) 。  
  
## <a name="see-also"></a>另请参阅  
 [授予对对象和操作的访问权限 (Analysis Services)](../../analysis-services/multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md)   
 [安全角色（Analysis Services - 多维数据）](../../analysis-services/multidimensional-models/olap-logical/security-roles-analysis-services-multidimensional-data.md)  
  
  
