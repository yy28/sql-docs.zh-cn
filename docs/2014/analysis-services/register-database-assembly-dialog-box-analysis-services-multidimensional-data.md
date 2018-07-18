---
title: 注册数据库程序集对话框 (Analysis Services-多维数据) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidevstudio.assembly.registerassembly.f1
ms.assetid: 0c07cc87-fc94-456f-b878-7b23e39772b9
caps.latest.revision: 18
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bf8c949083c15216f0655c7753f426de77f289e2
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37196867"
---
# <a name="register-database-assembly-dialog-box-analysis-services---multidimensional-data"></a>“注册数据库程序集”对话框（Analysis Services - 多维数据）
  使用 **中的** “注册服务器程序集” [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 对话框，可以设置 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库中程序集引用的属性。 右键单击“对象资源管理器”中的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例或数据库的程序集文件夹，并选择“新建程序集”，可以显示“注册服务器程序集”。  
  
## <a name="options"></a>“常规”  
  
|术语|定义|  
|----------|----------------|  
|**类型**|选择程序集引用的类型。 可用值如下：<br /><br /> **.NET 程序集**： <br />                      该程序集引用表示对 [!INCLUDE[msCoName](../includes/msconame-md.md)] .NET Framework 程序集的引用。<br /><br /> **COM DLL**： <br />                      该程序集引用表示对 COM 库的引用。<br /><br /> <br /><br /> **\*\* 安全说明\* \***  COM 程序集可能会带来安全风险。 由于此风险和其他注意事项， [!INCLUDE[ssASversion10](../includes/ssasversion10-md.md)]中不推荐使用 COM 程序集。 未来版本可能不支持 COM 程序集。|  
|**文件名**|输入 .NET 程序集或 COM 库的完整路径和文件名。|  
|**...**|单击此项将显示 **“打开”** 对话框，选择 .NET 程序集或 COM 库的完整路径和文件名。|  
|**程序集名称**|键入以设置程序集引用的名称。<br /><br /> 注意：更改此值不会更改程序集引用所表示引用的程序集的名称，但会更改 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例或数据库在表示程序集引用时所使用的名称。|  
|**包含调试信息**|如果可用，请选择此选项，以包含 .NET 程序集或 COM 库的调试信息。|  
|**创建时间戳**|显示程序集引用的创建日期和时间。|  
|**上次架构更新时间**|显示上次更新程序集引用的元数据的日期和时间。|  
|**数据源**|显示程序集引用的源。 此属性通常包含程序集引用所引用的程序集的完整路径和文件名。|  
|**Safe**|选择此选项可以对程序集引用使用此权限集。 如果选择了此选项，将只允许该程序集进行内部计算和本地数据访问。 具有此选项的程序集所执行的代码将无法访问外部系统资源，如文件、网络、环境变量或注册表。<br /><br /> **\*\* 安全说明\* \*** 此选项是推荐的权限设置的程序集，而无需访问外部资源执行计算和数据管理任务[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]。 此选项表示最严格的权限集。|  
|**外部访问**|选择此选项可以对程序集引用使用此权限集。 如果选择了此选项，将只允许该程序集进行内部计算和本地数据访问。 具有此权限集的程序集所执行的代码可以访问外部系统资源，如文件、网络、环境变量和注册表。<br /><br /> **\*\* 安全说明\* \*** 访问外部资源的程序集建议使用此选项[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]。 默认情况下，使用此选项的程序集会使用服务帐户的安全凭据执行。 程序集内的代码可以显式地模拟调用方的 [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows 身份验证安全上下文。 因为默认情况是作为服务帐户执行，所以对于执行具有此选项的程序集的权限，只应该授予作为服务帐户运行的可信角色。 此选项表示一个不如 **“安全”** 严格的权限集，但是比 **“无限制”** 要严格。|  
|**不受限制**|选择此选项可以对程序集引用使用此权限集。 如果选择此选项，则程序集可以无限制访问内部和外部资源。 通过具有此选项的程序集执行代码可以调用非托管的代码。<br /><br /> **\*\* 安全说明\* \*** 除非程序集需要无限制访问权限，否则不建议使用此选项。 从安全的角度来看，此选项等同于 **“外部访问”**。 但是，使用 **“外部访问”** 选项的程序集提供了使用此选项的程序集所不具备的可靠性和强有力保护。 指定此选项将允许程序集中的代码对进程空间执行非法操作，因此可能危及 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]的可靠性和可伸缩性。 此选项表示受限制最少的权限集，因此使用时要特别小心。|  
|**使用特定用户名和密码**|选择此选项将使 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 对象使用指定用户帐户的安全凭据。|  
|**用户名**|键入所选 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 对象将使用的用户帐户的域和名称。 用户帐户的域和名称使用的格式如下：<br /><br /> *\<域名 >* **\\** *\<用户帐户名 >*<br /><br /> 注意：只有在选中“使用特定名称和密码”  后，才能启用此选项。|  
|**密码**|键入所选 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 对象将使用的用户帐户的域和名称。|  
|**使用服务帐户**|选择此选项将使 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 对象使用与管理该对象的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 服务相关联的安全凭据。|  
|**使用当前用户的凭据**|选择此选项将使 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 对象使用当前用户的安全凭据。|  
|**Default**|选择此选项后，将使用 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]的默认用户帐户。 选择此选项等效于选择 **“使用当前用户的凭据”** 选项。|  
|**Description**|键入以设置程序集引用的说明。|  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 设计器和对话框&#40;多维数据&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [多维模型程序集管理](multidimensional-models/multidimensional-model-assemblies-management.md)  
  
  
