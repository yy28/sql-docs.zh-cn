---
title: MSReportServer_ConfigurationSetting 方法 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
api_name:
- MSReportServer_ConfigurationSetting Methods
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- WMI provider [Reporting Services], MSReportServer_ConfigurationSetting class
- MSReportServer_ConfigurationSetting class
ms.assetid: a08c2476-5b8e-4792-94da-1360fe231c6e
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: d726e3982636b89819afed3a8500a581eebffc13
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56019618"
---
# <a name="msreportserverconfigurationsetting-methods"></a>MSReportServer_ConfigurationSetting 方法
  报表服务器 WMI 提供程序的 MSReportServer_ConfigurationSetting 类提供了以下公共方法。  
  
## <a name="public-methods"></a>公共方法  
  
|||  
|-|-|  
|[BackupEncryptionKey](configurationsetting-method-backupencryptionkey.md)|备份实例的加密密钥。 加密密钥会在使用密码加密后存储。|  
|[CreateSSLCertificateBinding 方法 (WMI MSReportServer_ConfigurationSetting)](configurationsetting-method-createsslcertificatebinding.md)|创建 SSL 证书绑定。|  
|[DeleteEncryptedInformation](configurationsetting-method-deleteencryptedinformation.md)|从报表服务器数据库删除加密信息。|  
|[DeleteEncryptionKey](configurationsetting-method-deleteencryptionkey.md)|从报表服务器数据库删除加密密钥。|  
|[GenerateDatabaseCreationScript](configurationsetting-method-generatedatabasecreationscript.md)|生成可用于创建报表服务器数据库的 SQL 脚本。|  
|[GenerateDatabaseRightsScript](configurationsetting-method-generatedatabaserightsscript.md)|生成可用来向用户授予报表服务器数据库权限的 SQL 脚本。|  
|[GenerateDatabaseUpgradeScript](configurationsetting-method-generatedatabaseupgradescript.md)|生成可用于升级报表服务器数据库的 SQL 脚本。|  
|[GetAdminSiteUrl 方法 (WMI)](configurationsetting-method-getadminsiteurl.md)|获取管理中心网站的绝对 URL。|  
|[GetDatabaseVersionDisplayName](configurationsetting-method-getdatabaseversiondisplayname.md)|获取给定报表服务器数据库版本字符串的显示名称。|  
|[InitializeReportServer](configurationsetting-method-initializereportserver.md)|初始化指定报表服务器实例。|  
|[ListInstalledSharePointVersions 方法 (WMI)](configurationsetting-method-listinstalledsharepointversions.md)|返回一组标记，表示与报表服务器安装在同一台计算机上的 Microsoft [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] [!INCLUDE[offSPServ](../../includes/offspserv-md.md)], [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]、 or [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] 版本。|  
|[ListIPAddresses 方法 (WMI MSReportServer_ConfigurationSetting)](configurationsetting-method-listipaddresses.md)|列出计算机的 IP 地址。|  
|[ListReportServersInDatabase](configurationsetting-method-listreportserversindatabase.md)|返回报表服务器数据库中存在的报表服务器安装列表，无论这些安装是否具有访问安全信息的权限。|  
|[ListReservedURLs 方法 (WMI MSReportServer_ConfigurationSetting)](configurationsetting-method-listreservedurls.md)|列出为报表服务器上所有应用程序保留的 URL。|  
|[ListSSLCertificateBindings 方法 (WMI MSReportServer_ConfigurationSetting)](configurationsetting-method-listsslcertificatebindings.md)|列出 HTTP.SYS 中存在的以及 RSReportServer.config 中应有的 SSL 证书绑定。|  
|[ListSSLCertificates 方法 (WMI MSReportServer_ConfigurationSetting)](configurationsetting-method-listsslcertificates.md)|列出计算机上安装的 SSL 证书。|  
|[ReencryptSecureInformation](configurationsetting-method-reencryptsecureinformation.md)|生成新的加密密钥，并使用新密钥对报表服务器数据库中的所有安全信息进行重新加密。|  
|[RemoveSSLCertificateBindings 方法 (WMI MSReportServer_ConfigurationSetting)](configurationsetting-method-removesslcertificatebinding.md)|删除 SSL 证书绑定。|  
|[RemoveUnattendedExecutionAccount](configurationsetting-method-removeunattendedexecutionaccount.md)|从报表服务器配置中删除无人参与的执行帐户条目。|  
|[RemoveURL 方法 (WMI MSReportServer_ConfigurationSetting)](configurationsetting-method-removeurl.md)|删除为报表服务器保留的 URL。|  
|[ReserveURL 方法 (WMI MSReportServer_ConfigurationSetting)](configurationsetting-method-reserveurl.md)|为给定的应用程序添加一个 URL 预留。|  
|[RestoreEncryptionKey](configurationsetting-method-restoreencryptionkey.md)|将指定的加密密钥重新应用于报表服务器数据库。|  
|[SetDatabaseConnection](configurationsetting-method-setdatabaseconnection.md)|设置与特定报表服务器数据库的报表服务器数据库连接。|  
|[SetDatabaseLogonTimeout](configurationsetting-method-setdatabaselogontimeout.md)|为报表服务器数据库登录尝试指定默认超时值。|  
|[SetDatabaseQueryTimeout](configurationsetting-method-setdatabasequerytimeout.md)|为报表服务器数据库查询指定默认超时值。|  
|[SetEmailConfiguration](configurationsetting-method-setemailconfiguration.md)|配置报表服务器用来发送电子邮件的电子邮件传递扩展插件。|  
|[SetSecureConnectionLevel](configurationsetting-method-setsecureconnectionlevel.md)|设置报表服务器的安全连接级别。|  
|[SetServiceState](configurationsetting-method-setservicestate.md)|打开和关闭报表服务器服务。|  
|[SetUnattendedExecutionAccount](configurationsetting-method-setunattendedexecutionaccount.md)|指定用于以无人参与方式运行报表的帐户。|  
|[SetVirtualDirectory 方法 (WMI MSReportServer_ConfigurationSetting)](configurationsetting-method-setvirtualdirectory.md)|设置应用程序的虚拟目录。|  
|[SetWindowsServiceIdentity](configurationsetting-method-setwindowsserviceidentity.md)|将报表服务器服务作为指定的 Windows 用户运行，并授予此帐户足够的文件系统权限以允许操作报表服务器。|  
  
## <a name="see-also"></a>请参阅  
 [MSReportServer_ConfigurationSetting Class](msreportserver-configurationsetting-class.md)  
  
  
