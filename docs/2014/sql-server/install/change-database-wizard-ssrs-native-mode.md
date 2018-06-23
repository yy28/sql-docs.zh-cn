---
title: 更改数据库向导 （SSRS 本机模式） |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- SQL12.rsconfigtool.changedatabase.F1
helpviewer_keywords:
- Change Database Wizard
- report server database, create
ms.assetid: 1a2e8d18-5997-482f-a9c1-87d99f7407b8
caps.latest.revision: 10
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: 256d91789d4bc1413580fde6f5c40ff8151f309a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36027576"
---
# <a name="change-database-wizard-ssrs-native-mode"></a>更改数据库向导（SSRS 本机模式）
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]配置管理器提供更改数据库向导，可指导您完成创建新的报表服务器数据库或选择现有的报表服务器数据库与当前报表服务器实例一起使用的步骤。  
  
 如果您选择来自早期版本的报表服务器数据库，所选数据库将进行升级，以便与其连接的报表服务器实例的版本匹配。 服务启动时，它会检查数据库版本并自动将其升级到当前架构。  
  
 若要启动向导，请单击**更改数据库**中的数据库页上[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]Configuration Manager。 有关说明如何启动[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]配置管理器中，请参阅[Reporting Services 配置管理器&#40;纯模式&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)。  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 本机模式。  
  
## <a name="options"></a>“常规”  
 **操作**  
 选择您要执行的任务。 您可以在本机模式或 SharePoint 集成模式下创建新的数据库。 或者，您也可以选择现有的报表服务器数据库以将其与当前报表服务器实例一起使用。  
  
 **数据库服务器**  
 指定的名称[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)]承载报表服务器数据库的实例。 可以使用本地或远程计算机上的默认或命名实例。 如果你要连接到命名实例，则按以下格式输入服务器名称： \<*服务器*>\\<*实例*>。  
  
 若要连接到[!INCLUDE[ssDE](../../includes/ssde-md.md)]实例，必须使用有权登录到服务器和更新数据库信息的凭据。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager 使用您当前的 Windows 凭据，但如果你没有登录名或数据库权限，则必须指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库登录名。 您不能指定其他 Windows 凭据。 如果你想要以不同的 Windows 用户，该用户的登录身份连接，然后启动[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]Configuration Manager。  
  
 如果要连接到远程实例，您需要先为该实例启用远程连接。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的某些版本和版本类别在默认情况下不启用远程连接。 若要确认是否允许进行远程连接，请使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]配置管理器并确认是否已启用了 TCP/IP 和命名管道协议。 如果远程实例还是一个命名实例，请验证目标服务器上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服务是否已启用且正在运行。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 浏览器提供到命名实例使用的端口号[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]Configuration Manager。  
  
 **“数据库”**  
 指定存储服务器数据的报表服务器数据库的名称。 可以指定现有的数据库或创建新的数据库。  
  
 当您在“操作”页面中选择 **“创建新数据库”** 时，用于创建新数据库的属性将显示在向导中。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager 将创建按名称绑定的两个数据库： 数据库以包含静态数据和临时数据库用于存储会话和工作数据。 有关详细信息，请参阅[报表服务器数据库&#40;SSRS 本机模式&#41;](../../reporting-services/report-server/report-server-database-ssrs-native-mode.md)中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]联机丛书。  
  
 您也可以选择现有的报表服务器数据库。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器不会将无效的数据库筛选出来。 有效的数据库是基于报表服务器数据库架构的（您不能选择缺少必要的表、视图或存储过程的数据库）。 如果你选择的早期版本创建的数据库[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]，该数据库将升级到当前格式。  
  
 **语言**  
 只有在创建新的报表服务器数据库时，才需设置此值。  
  
 利用此值，您可以指定以何种语言创建角色定义和说明。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 提供了一个基于角色的授权模型，此模型包含一组预定义的角色。 这些角色仅会以您指定的语言创建一次。 角色名称和说明绝不会以其他语言显示，即使您连接到报表服务器所用的浏览器的区域性或语言设置受此服务器支持，也不例外。 您指定的语言也决定了使用何种语言创建作为“我的报表”功能一部分的“我的报表”文件夹和“用户”文件夹的名称。  
  
 **服务器模式**  
 报表服务器数据库支持本机模式或 SharePoint 集成模式。 这两种模式是互斥的。  
  
 如果您要创建新的报表服务器数据库，必须指定一种模式。 你选择的模式决定了报表服务器数据库和集的结构`SharePointIntegrated`报告到的服务器系统属性`true`或`false`。  
  
 如果您要选择其他报表服务器数据库，则会显示当前数据库的模式，以便让您知道当前数据库的使用方式。  
  
 **凭据**  
 指定用于将报表服务器连接到报表服务器数据库的帐户。 有效的值包括报表服务器 Web 服务的服务帐户[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]上定义的数据库登录名[!INCLUDE[ssDE](../../includes/ssde-md.md)]实例正在使用来承载报表服务器，或者是 Windows 帐户。 如果你使用的 Windows 帐户，则可以指定本地帐户 (*\<computername >\\< 用户名\>*) 如果报表服务器和数据库位于同一台计算机或域用户帐户 (*\<域 >\\< 用户名\>*) 它们是否位于同一域中的不同计算机上。  
  
 报表服务器将创建一个数据库登录名，并为您指定的帐户分配数据库权限。  
  
 报表服务器自身不创建帐户。 您指定的帐户必须已经存在，并且对于部署配置而言必须是有效的。 具体来说，如果数据库位于远程计算机上并且您希望使用 Windows 帐户，则您必须指定对该计算机拥有登录权限的帐户。  
  
 如果计算机是在不同的或非受信任的域，请考虑使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库登录名。 有关选择帐户的详细信息，请参阅[配置报表服务器数据库连接&#40;SSRS 配置管理器&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)。  
  
 **摘要**  
 在安装程序配置连接前验证设置。  
  
 **进度和完成**  
 监视每个任务的进度。  
  
## <a name="see-also"></a>请参阅  
 [数据库&#40;SSRS 本机模式&#41;](../../../2014/sql-server/install/database-ssrs-native-mode.md)   
 [更改凭据向导&#40;SSRS 本机模式&#41;](../../../2014/sql-server/install/change-credentials-wizard-ssrs-native-mode.md)   
 [创建本机模式报表服务器数据库（SSRS 配置管理器）](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)   
 [Reporting Services 配置管理器的 F1 帮助主题&#40;SSRS 本机模式&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [配置报表服务器数据库连接&#40;SSRS 配置管理器&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)  
  
  