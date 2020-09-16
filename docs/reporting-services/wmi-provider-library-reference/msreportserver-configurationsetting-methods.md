---
description: MSReportServer_ConfigurationSetting 方法
title: MSReportServer_ConfigurationSetting 方法 | Microsoft Docs
ms.date: 03/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- MSReportServer_ConfigurationSetting Methods
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- WMI provider [Reporting Services], MSReportServer_ConfigurationSetting class
- MSReportServer_ConfigurationSetting class
ms.assetid: a08c2476-5b8e-4792-94da-1360fe231c6e
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 7b51e79a99f47886627f6479f58b7a2980629d88
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88472605"
---
# <a name="msreportserver_configurationsetting-methods"></a>MSReportServer_ConfigurationSetting 方法
  报表服务器 WMI 提供程序的 MSReportServer_ConfigurationSetting 类提供了以下公共方法。  
  
## <a name="public-methods"></a>公共方法  
  
|方法|说明|  
|-|-|  
|[BackupEncryptionKey](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-backupencryptionkey.md)|备份实例的加密密钥。 加密密钥会在使用密码加密后存储。|  
|[CreateSSLCertificateBinding 方法 (WMI MSReportServer_ConfigurationSetting)](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-createsslcertificatebinding.md)|创建 TLS/SSL 证书绑定。|  
|[DeleteEncryptedInformation](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-deleteencryptedinformation.md)|从报表服务器数据库删除加密信息。|  
|[DeleteEncryptionKey](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-deleteencryptionkey.md)|从报表服务器数据库删除加密密钥。|  
|[GenerateDatabaseCreationScript](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-generatedatabasecreationscript.md)|生成可用于创建报表服务器数据库的 SQL 脚本。|  
|[GenerateDatabaseRightsScript](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-generatedatabaserightsscript.md)|生成可用来向用户授予报表服务器数据库权限的 SQL 脚本。|  
|[GenerateDatabaseUpgradeScript](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-generatedatabaseupgradescript.md)|生成可用于升级报表服务器数据库的 SQL 脚本。|  
|[GetAdminSiteUrl 方法 (WMI)](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-getadminsiteurl.md)|获取管理中心网站的绝对 URL。|  
|[GetDatabaseVersionDisplayName](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-getdatabaseversiondisplayname.md)|获取给定报表服务器数据库版本字符串的显示名称。|  
|[InitializeReportServer](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-initializereportserver.md)|初始化指定报表服务器实例。|  
|[ListInstalledSharePointVersions 方法 (WMI)](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-listinstalledsharepointversions.md)|返回一组标记，表示与报表服务器安装在同一台计算机上的 Microsoft [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] [!INCLUDE[offSPServ](../../includes/offspserv-md.md)]、[!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 或 [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] 版本。|  
|[ListIPAddresses 方法 (WMI MSReportServer_ConfigurationSetting)](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-listipaddresses.md)|列出计算机的 IP 地址。|  
|[ListReportServersInDatabase](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-listreportserversindatabase.md)|返回报表服务器数据库中存在的报表服务器安装列表，无论这些安装是否具有访问安全信息的权限。|  
|[ListReservedURLs 方法 (WMI MSReportServer_ConfigurationSetting)](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-listreservedurls.md)|列出为报表服务器上所有应用程序保留的 URL。|  
|[ListSSLCertificateBindings 方法 (WMI MSReportServer_ConfigurationSetting)](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-listsslcertificatebindings.md)|列出 HTTP.SYS 中存在的以及 RSReportServer.config 中应有的 TLS/SSL 证书绑定。|  
|[ListSSLCertificates 方法 (WMI MSReportServer_ConfigurationSetting)](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-listsslcertificates.md)|列出计算机上安装的 TLS/SSL 证书。|  
|[ReencryptSecureInformation](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-reencryptsecureinformation.md)|生成新的加密密钥，并使用新密钥对报表服务器数据库中的所有安全信息进行重新加密。|  
|[RemoveSSLCertificateBindings 方法 (WMI MSReportServer_ConfigurationSetting)](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-removesslcertificatebinding.md)|删除 TLS/SSL 证书绑定。|  
|[RemoveUnattendedExecutionAccount](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-removeunattendedexecutionaccount.md)|从报表服务器配置中删除无人参与的执行帐户条目。|  
|[RemoveURL 方法 (WMI MSReportServer_ConfigurationSetting)](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-removeurl.md)|删除为报表服务器保留的 URL。|  
|[ReserveURL 方法 (WMI MSReportServer_ConfigurationSetting)](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-reserveurl.md)|为给定的应用程序添加一个 URL 预留。|  
|[RestoreEncryptionKey](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-restoreencryptionkey.md)|将指定的加密密钥重新应用于报表服务器数据库。|  
|[SetDatabaseConnection](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setdatabaseconnection.md)|设置与特定报表服务器数据库的报表服务器数据库连接。|  
|[SetDatabaseLogonTimeout](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setdatabaselogontimeout.md)|为报表服务器数据库登录尝试指定默认超时值。|  
|[SetDatabaseQueryTimeout](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setdatabasequerytimeout.md)|为报表服务器数据库查询指定默认超时值。|  
|[SetEmailConfiguration](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setemailconfiguration.md)|配置报表服务器用来发送电子邮件的电子邮件传递扩展插件。|  
|[SetSecureConnectionLevel](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setsecureconnectionlevel.md)|设置报表服务器的安全连接级别。|  
|[SetServiceState](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setservicestate.md)|打开和关闭报表服务器服务。|  
|[SetUnattendedExecutionAccount](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setunattendedexecutionaccount.md)|指定用于以无人参与方式运行报表的帐户。|  
|[SetVirtualDirectory 方法 (WMI MSReportServer_ConfigurationSetting)](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setvirtualdirectory.md)|设置应用程序的虚拟目录。|  
|[SetWindowsServiceIdentity](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setwindowsserviceidentity.md)|将报表服务器服务作为指定的 Windows 用户运行，并授予此帐户足够的文件系统权限以允许操作报表服务器。|  
  
## <a name="see-also"></a>另请参阅  
 [MSReportServer_ConfigurationSetting 类](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
  
