---
title: MSReportServer_ConfigurationSetting 属性 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
api_name:
- MSReportServer_ConfigurationSetting Properties
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- WMI provider [Reporting Services], MSReportServer_ConfigurationSetting class
- MSReportServer_ConfigurationSetting class
ms.assetid: e75fe1e5-197b-4c65-859b-370821cad003
caps.latest.revision: 45
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: d79503c958729d95fe9ee223accb709e8369cf9b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37313291"
---
# <a name="msreportserverconfigurationsetting-properties"></a>MSReportServer_ConfigurationSetting 属性
  MSReportServer_ConfigurationSetting 类用于表示报表服务器实例的安装和运行时参数。 这些设置存储在 RSReportServer.config 配置文件中。  
  
## <a name="public-properties"></a>公共属性  
  
|||  
|-|-|  
|[ConnectionPoolSize](configurationsetting-property-connectionpoolsize.md)|返回报表服务器与承载报表服务器数据库的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例通信时使用的连接池大小。 只读。|  
|[DatabaseLogonAccount](configurationsetting-property-databaselogonaccount.md)|指定报表服务器连接到承载报表服务器数据库的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例时使用的登录帐户。 只读。|  
|[DatabaseLogonTimeout](configurationsetting-property-databaselogontimeout.md)|指定尝试登录到报表服务器数据库失败前等待的秒数。 只读。|  
|[DatabaseLogonType](configurationsetting-property-databaselogontype.md)|指定报表服务器是使用 Windows 服务帐户、Windows 用户帐户还是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名访问报表服务器数据库。 只读。|  
|[DatabaseName](configurationsetting-property-databasename.md)|指定承载报表服务器数据库的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的名称。|  
|[DatabaseQueryTimeout](configurationsetting-property-databasequerytimeout.md)|指定命令失败或超时之前必须等待的秒数。报表服务器会根据 SQL Server 目录对进程进行计时，而不会根据报表的数据源计时。|  
|[DatabaseServerName](configurationsetting-property-databaseservername.md)|指定用来安装报表服务器数据库的服务器的名称。|  
|[InstallationID 属性](configurationsetting-property-installationid.md)|返回特定报表服务器实例的唯一标识符。|  
|[InstanceName](configurationsetting-property-instancename.md)|指定特定计算机上报表服务器实例的名称。|  
|[IsInitialized](configurationsetting-property-isinitialized.md)|指示报表服务器实例是否已初始化。  只读。|  
|[IsSharePointIntegrated](configurationsetting-property-issharepointintegrated.md)|指示报表服务器是否配置为 SharePoint 集成模式。|  
|[IsWebServiceEnabled](configurationsetting-property-iswebserviceenabled.md)|指示是否已启用报表服务器 Web 服务。 只读。|  
|[IsWindowsServiceEnabled](configurationsetting-property-iswindowsserviceenabled.md)|指示是否已启用报表服务器 Windows 服务。 只读。|  
|[MachineAccountIdentity 属性&#40;WMI&#41;](configurationsetting-property-machineaccountidentity.md)|获取安装了报表服务器的计算机的计算机帐户标识。|  
|[PathName](configurationsetting-property-pathname.md)|指定报表服务器实例的安装路径。|  
|[SecureConnectionLevel](configurationsetting-property-secureconnectionlevel.md)|返回 RSReportServer.config 文件中指定的安全连接级别。|  
|[SenderEmailAddress](configurationsetting-property-senderemailaddress.md)|从报表服务器获取用于发送电子邮件的地址。 只读。|  
|[SendUsingSMTPServer](configurationsetting-property-sendusingsmtpserver.md)|指定电子邮件配置中 SendUsing 属性是否设置为 TRUE。|  
|[SMTPServer](configurationsetting-property-smtpserver.md)|从 RSReportServer.config 文件中获取 SMTP 服务器属性。 只读。|  
|[UnattendedExecutionAccount](configurationsetting-property-unattendedexecutionaccount.md)|指定以无人参与方式运行报表时报表服务器将模拟的登录用户帐户。 只读。|  
|[版本](configurationsetting-property-version.md)|返回报表服务器的版本。|  
|[VirtualDirectoryReportManager 属性&#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-property-virtualdirectoryreportmanager.md)|返回报表管理器应用程序的虚拟目录。|  
|[VirtualDirectoryReportServer 属性&#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-property-virtualdirectoryreportserver.md)|返回报表服务器 Web 服务应用程序的虚拟目录。|  
|[WindowsServiceIdentityActual](configurationsetting-property-windowsserviceidentityactual.md)|返回报表服务器 Windows 服务运行时实际使用的标识。 只读。|  
|[WindowsServiceIdentityConfigured](windowsserviceidentityconfigured-property.md)|返回在上次配置报表服务器 Windows 服务时所指定的运行时要使用的标识。 只读。|  
  
## <a name="see-also"></a>请参阅  
 [MSReportServer_ConfigurationSetting 成员](msreportserver-configurationsetting-members.md)  
  
  
