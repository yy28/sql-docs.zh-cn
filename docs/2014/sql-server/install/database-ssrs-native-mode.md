---
title: 数据库 （SSRS 本机模式） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.databasesetup.F1
ms.assetid: 8c9bb3b3-ea77-4a5b-ba35-7451ed11083d
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: d79b50e70f3eae3d9183ae220002136b39717e46
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63278561"
---
# <a name="database-ssrs-native-mode"></a>数据库（SSRS 本机模式）
  使用“数据库”页创建和配置为一个或多个报表服务器实例提供内部存储的报表服务器数据库。 如果要配置报表服务器以使用远程报表服务器数据库，则必须使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器来创建该数据库。  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 本机模式。  
  
 创建报表服务器数据库和配置连接是一个多步骤过程。 为了指导您完成各个步骤，此页为每种类型的任务都提供了向导。 还将为您创建或更新权限和登录名。 您可以在“进度”页中监视每个步骤的状态。 如果出现错误，您可以单击该错误以获取如何解决该错误的相关信息。  
  
 报表服务器数据库必须支持特定服务器模式。 默认模式为本机模式，但如果是在较大的 SharePoint 产品或技术部署中运行报表服务器，则也可以创建 SharePoint 集成模式下的报表服务器。 有关详细信息，请参阅[创建本机模式报表服务器数据库（SSRS 配置管理器）](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)。  
  
 若要打开此页，请启动 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器，然后单击导航窗格中的 **“数据库”** 。 有关详细信息，请参阅 [Reporting Services Configuration Manager（本机模式）](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)。  
  
## <a name="options"></a>选项  
 **SQL Server 名称**  
 在“当前报表服务器数据库”中， **“SQL Server 名称”** 指定运行报表服务器数据库的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的名称。 可以使用本地或远程计算机上的默认或命名实例。  
  
 **Database Name**  
 指定存储服务器数据的报表服务器数据库的名称。  
  
 **报表服务器模式**  
 指示报表服务器数据库是支持本机模式还是支持 SharePoint 集成模式。 有关详细信息，请参阅[Reporting Services 报表服务器](../../../2014/reporting-services/reporting-services-report-server.md)。  
  
 **更改数据库**  
 启动一个向导以指导您完成创建或选择报表服务器数据库所需的所有步骤。  
  
 **凭据类型**  
 指定报表服务器用来连接报表服务器数据库的凭据。 可以指定的凭据类型包括服务帐户、Windows 域用户、Windows 本地用户或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库登录名。 有关选择凭据的详细信息，请参阅[配置报表服务器数据库连接&#40;SSRS 配置管理器&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)。  
  
 **用户名**  
 如果使用的是 Windows 凭据，请指定域用户帐户；如果使用的是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 凭据，则指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名。 如果使用的 Windows 凭据，它们按以下格式指定： *\<域 >\\< 帐户\>*。  
  
 **密码**  
 指定帐户的密码。  
  
 **更改凭据**  
 启动可指导您完成以下操作所需的所有步骤的向导，这些操作包括选择不同的帐户或更新用于连接到报表服务器数据库的帐户的密码。  
  
## <a name="see-also"></a>请参阅  
 [创建本机模式报表服务器数据库（SSRS 配置管理器）](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)   
 [Reporting Services 配置管理器 F1 帮助主题&#40;SSRS 本机模式&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [报表服务器数据库（SSRS 本机模式）](../../reporting-services/report-server/report-server-database-ssrs-native-mode.md)   
 [配置报表服务器数据库连接（SSRS 配置管理器）](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)  
  
  
