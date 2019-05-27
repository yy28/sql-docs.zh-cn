---
title: 执行帐户 （SSRS 本机模式） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.executionaccount.F1
ms.assetid: 440b5a09-5fd4-4c3a-b510-f3c33cbf1c82
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 17bbc891c54d28f5eedbebc1d51edf11d0ae405b
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66095340"
---
# <a name="execution-account-ssrs-native-mode"></a>执行帐户（SSRS 本机模式）
  使用此页可以配置用于无人参与处理的帐户。 只有在其他凭据源不可用的以下特殊情况时，才使用此帐户：  
  
-   当报表服务器连接到不需要凭据的数据源时。 可能不需要凭据的数据源示例包括 XML 文档和一些客户端数据库应用程序。  
  
-   当报表服务器连接到其他服务器以检索报表中所引用的外部图像文件或其他资源时。  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 本机模式。  
  
 设置此帐户是可选的，但如果不设置此帐户，则将限制您使用外部图像以及与一些数据源的连接。 在检索外部图像文件时，报表服务器将检查是否可以建立匿名连接。 如果连接受密码保护，报表服务器将使用无人参与的报表处理帐户来连接到远程服务器。 在为报表检索数据时，报表服务器或者模拟当前用户、提示用户提供凭据或使用存储的凭据，或者（如果数据源连接指定 **“无”** 作为凭证类型）使用无人参与的处理帐户。 在连接到其他计算机时，报表服务器不允许对其服务帐户凭据进行委托或模拟，因此，如果不能使用其他凭据，报表服务器就必须使用无人参与的处理帐户。  
  
 您指定的帐户不能是用于运行服务帐户的帐户。 如果配置了该帐户，它将作为加密值存储在 RSReportServer.config 文件中。 如果将在扩展部署中运行该报表服务器，则必须在每个报表服务器上以相同的方式配置此帐户。  
  
 您可以使用任何一个 Windows 用户帐户。 为获得最佳结果，请选择拥有读取权限和网络登录权限的帐户，以支持与其他计算机的连接。 对于您希望在报表中使用的任何外部图像或数据文件，它必须拥有对这些文件的读取权限。 切勿指定本地帐户，除非所有报表数据源和外部图像均存储在报表服务器计算机中。 只可将该帐户用于无人参与报表处理。  
  
> [!NOTE]  
>  如果使用的是带高级服务的 [!INCLUDE[ssExpressEd11](../../includes/ssexpressed11-md.md)]，则仅当在报表中引用外部图像并且访问该图像文件需要相应权限时才需要配置此帐户。 SQL Server Express 不支持到远程服务器的数据源连接。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]各版本支持的功能列表，请参阅 [SQL Server 2012 各个版本支持的功能](https://go.microsoft.com/fwlink/?linkid=232473)。  
  
 若要打开此页，请启动 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器，并在导航窗格中选择 **“执行帐户”** 。 有关详细信息，请参阅 [Reporting Services Configuration Manager（本机模式）](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)。  
  
## <a name="options"></a>选项  
 **指定执行帐户**  
 选择此选项可指定一个帐户。  
  
 **帐户**  
 输入一个 Windows 域用户帐户。 使用如下格式：\<domain>\\<user account\>。  
  
 **密码**  
 键入密码。  
  
 **确认密码**  
 重新键入密码。  
  
## <a name="see-also"></a>请参阅  
 [Reporting Services 配置管理器 F1 帮助主题&#40;SSRS 本机模式&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [存储加密的 Report Server 数据（SSRS 配置管理器）](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)   
 [配置无人参与的执行帐户（SSRS 配置管理器）](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)  
  
  
