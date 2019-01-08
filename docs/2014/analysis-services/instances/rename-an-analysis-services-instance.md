---
title: 重命名 Analysis Services 实例 |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- instances of Analysis Services, renaming
- renaming instances of Analysis Services
- names [Analysis Services], renaming instances
- names [Analysis Services]
ms.assetid: 87494741-4a2e-4fed-8061-418fd1e111c3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 88a87802574290dee1cf0faaea2474e9fce408ce
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2018
ms.locfileid: "52401442"
---
# <a name="rename-an-analysis-services-instance"></a>重命名 Analysis Services 实例
  您可以重命名的现有实例[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]通过使用**重命名实例**对话框。  
  
> [!IMPORTANT]  
>  重命名该实例时， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例重命名工具将以提升的权限运行，更新与该实例关联的 Windows 服务名称、安全帐户和注册表项。 为确保执行这些操作，请务必以本地系统管理员身份运行此工具。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例重命名工具不会修改为原始实例创建的程序文件夹。 请不要修改该程序文件夹名称以便与要重命名的实例匹配。 更改程序文件夹名称会妨碍安装程序修复或卸载安装软件。  
  
> [!NOTE]  
>  群集环境中不支持 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例重命名工具。  
  
### <a name="to-rename-an-instance-of-analysis-services"></a>重命名 Analysis Services 的实例  
  
1.  启动**实例重命名**工具**asinstancerename.exe**，从 C:\Program Files\Microsoft SQL Server\110\Tools\Binn\ManagementStudio。  
  
2.  在 **“重命名实例”** 对话框中，从 **“要重命名的实例”** 列表中选择要重命名的实例。  
  
3.  在 **“新实例名”** 框中，输入实例的新名称。  
  
4.  验证用户名和密码是否正确，然后单击 **“重命名”**。  
  
     在名称更改过程中，Analysis Services 实例将会停止并重新启动。  
  
### <a name="post-rename-checklist"></a>重命名之后的核对清单  
  
1.  若要恢复对重命名的实例上运行的数据库的访问，您将需要在 Excel 或其他客户端应用程序中手动更新数据连接。 还需要检查所有预定义的连接，如可能引用您刚重命名的实例的 Reporting Services 共享数据源、Excel ODC 文件或 BI 语义模型连接文件。 有关详细信息，请参阅 [连接到 Analysis Services](connect-to-analysis-services.md)。  
  
2.  更新定期用于备份、同步或处理数据库的 PowerShell 脚本或 AMO 脚本。  
  
3.  更新在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中使用的 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]项目的项目属性。 对于表格模式服务器实例，务必要更新 model.bim 文件中的 Workspace Server 属性以及项目的 Server 属性。  
  
4.  根据您指定服务帐户的方式，您可能需要更新授予对服务的数据访问权限的数据库登录名或文件权限（例如，如果您使用服务帐户来处理数据或访问其他服务器上的链接对象）。  
  
     如果您使用虚拟帐户来设置服务，则需要更新数据库登录名或文件权限。 虚拟帐户基于实例名称，所以如果您将该实例重命名，虚拟帐户也会同时更新。 这意味着您为之前实例创建的所有以前的登录名或权限都不再有效。  
  
     下例对此进行了说明。 假设作为名为"Tabular"使用默认虚拟帐户，从而导致以下配置的实例安装在表格模式服务器：  
  
    1.  实例名称 =\<服务器 > \TABULAR  
  
    2.  服务名称 = MSOLAP$TABULAR  
  
    3.  虚拟帐户 = NT Service\ MSOLAP$TABULAR  
  
     现在假设您重命名为"TAB2"的实例。 更改名称后将生成如下配置：  
  
    1.  实例名称 =\<服务器 > \TAB2  
  
    2.  服务名称 = MSOLAP$TAB2  
  
    3.  虚拟帐户 = NT Service\ MSOLAP$TAB2  
  
     正如您所看到的以前授予"NT Service\ MSOLAP$ TABULAR"的数据库和文件权限都不再有效。 若要确保任务和服务执行的操作运行之前，就像现在需要向"NT Service\ MSOLAP$ TAB2"授予新的数据库和文件权限。  
  
  
