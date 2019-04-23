---
title: 命令提示符处安装 Reporting Services SharePoint 模式和本机模式 |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 048169b3-512c-41e4-895a-0416eff41268
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ec74b3d16830eff3c78a3b74e07bc017287defb5
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59947523"
---
# <a name="command-prompt-installation-of-reporting-services-sharepoint-mode-and-native-mode"></a>从命令提示符处安装 Reporting Services SharePoint 模式和本机模式
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 支持从 SQL Server 安装程序进行命令行安装。 本主题包含特定于 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]的若干命令行安装示例。 有关可用于所有 SQL Server 组件的命令行选项的完整说明，请参阅[从命令提示符安装 SQL Server 2014](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)。 本主题不介绍用于 SharePoint 产品的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 外接程序的命令行选项。 有关该外接程序的命令行安装的信息，请参阅[使用安装文件 rsSharePoint.msi 安装外接程序](install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md#bkmk_install_rssharepoint)。  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式 | [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 本机模式  
  
## <a name="rsinstallmode-native-mode"></a>RSINSTALLMODE（本机模式）  
 用于安装 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的主要输入设置是 **/RSINSTALLMODE** 输入设置。 该设置具有两个选项：**DefaultNativeMode**和**FilesOnlyMode**  
  
 如果安装包括 SQL Server 数据库引擎，则默认 RSINSTALLMODE 为 DefaultNativeMode。如果安装不包括 SQL Server 数据库引擎，则默认 RSINSTALLMODE 为 FilesOnlyMode。如果选择了 DefaultNativeMode 但安装不包括 SQL Server 数据库引擎，则安装会自动将 RSINSTALLMODE 更改为 FilesOnlyMode。 有关输入设置的详细信息，请参阅[从命令提示符安装 SQL Server 2014](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)。  
  
## <a name="rsshpinstallmode-sharepoint-mode"></a>RSSHPINSTALLMODE（SharePoint 模式）  
 用于在 SharePoint 模式下安装 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的输入设置是 **/RSSHPINSTALLMODE**。 输入的设置具有一个选项：SharePointFilesOnlyMode。 此选项将安装 SharePoint 模式所需的所有文件，但以下安装需要进行配置。 使用 SharePoint 管理中心完成其他配置步骤。 有关详细信息，请参见 [安装用于 SharePoint 2010 的 Reporting Services SharePoint 模式](../../sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)  
  
## <a name="examples-of-sharepoint-mode-installation"></a>SharePoint 模式安装示例  
 下面的示例将在 SharePoint 模式中安装 SQL Server 数据库引擎服务和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 以及 SharePoint [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 外接程序 (RS_SHPWFE)。  
  
```  
setup /q /ACTION=install /FEATURES=SQL, RS_SHP, RS_SHPWFE,TOOLS /INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="BUILTIN\ADMINISTRATORS" /RSSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE" /SQLSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE" /AGTSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE"  
```  
  
 下面的示例仅安装 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式。  
  
```  
Setup.exe /q /ACTION="Install" /IACCEPTSQLSERVERLICENSETERMS /FEATURES="RS_SHP" /INSTANCEDIR="C:\Program Files\Microsoft SQL Server" /INSTALLSHAREDDIR="C:\Program Files\Microsoft SQL Server" /INSTALLSHAREDWOWDIR="C:\Program Files (x86)\Microsoft SQL Server" /INSTALLSQLDATADIR="C:\Program Files\Microsoft SQL Server" /SECURITYMODE="SQL" /SAPWD="*****" /PID="[Your PID Value]" /SQLSYSADMINACCOUNTS="[Account Name]" "AutoSql Admin Group" /ASSYSADMINACCOUNTS="[Account Name]" /UPDATEENABLED="False"  
  
```  
  
 下面的示例将安装包括 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 本机模式和 SharePoint 模式在内的所有 SQL Server 功能。  
  
```  
Setup.exe /q /ACTION="Install" /INSTANCENAME="MSSQLSERVER" /FEATURES="SQLEngine,Replication,SNAC,SNAC_SDK,Browser,Writer,AS,IS,MDS,Adv_SSMS,BC,BOL,Conn,SDK,DReplay_CTLR,DReplay_CLT, RS_SHP,RS_SHPWFE,DQC,BIDS,FullText, RS,DQ,SSMS" /INSTANCEDIR="C:\Program Files\Microsoft SQL Server" /INSTALLSHAREDDIR="C:\Program Files\Microsoft SQL Server" /INSTALLSHAREDWOWDIR="C:\Program Files (x86)\Microsoft SQL Server" /INSTALLSQLDATADIR="C:\Program Files\Microsoft SQL Server" /SQLSVCACCOUNT="[Account Name]" /SQLSVCPASSWORD="********" /AGTSVCACCOUNT="[Account Nam]" /AGTSVCPASSWORD="********" /CTLRSVCACCOUNT="[Account Nam]" /CTLRSVCPASSWORD="********" /CLTSVCACCOUNT="[Account Nam]" /CLTSVCPASSWORD="********" /ASSVCACCOUNT="[Account Nam]" /ASSVCPASSWORD="********" /RSSVCACCOUNT="[Account Nam]" /RSSVCPASSWORD="********" /FTSVCACCOUNT="[Account Nam]" /FTSVCPASSWORD="********" /SECURITYMODE="SQL" /SAPWD="********" /PID="[Your PID Value]" /SQLSYSADMINACCOUNTS="[Account Nam]" "AutoSql Admin Group" /ASSYSADMINACCOUNTS="BUILTIN\ADMINISTRATORS" /UPDATEENABLED="False" /IACCEPTSQLSERVERLICENSETERMS /RSSHPINSTALLMODE="SharePointFilesOnlyMode" /RSINSTALLMODE="DefaultNativeMode"  
```  
  
## <a name="examples-of-sharepoint-mode-upgrade"></a>SharePoint 模式升级示例  
 下面的示例将升级 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式。 **RSUPGRADEPASSWORD** 是现有 Report Server 服务帐户的密码。 RSUPGRADEPASSWORD 是升级方案中必需的字段，除非 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务帐户是内置帐户。  
  
```  
Setup.exe /q /ACTION="Upgrade" /INSTANCENAME="MSSQLSERVER" /PID="[PID value]" /FTSVCACCOUNT="[DOMAIN\ACCOUNT]" /FTSVCPASSWORD="[ACCOUNTPASSSWORD]" /UPDATEENABLED="False" /IACCEPTSQLSERVERLICENSETERMS /RSUPGRADEPASSWORD="******"  
```  
  
 下面的示例可用于升级基于 SharePoint 共享服务体系结构的 SharePoint 模式安装。 该示例使用 ALLOWUPGRADEFORSSRSSHAREPOINTMODE 开关。 升级不基于共享服务体系结构的旧版本不需要该开关：  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
```  
Setup.exe /q /ACTION="Upgrade" /INSTANCENAME="MSSQLSERVER" /PID="[Your PID Value]" /FTSVCACCOUNT="[ACCOUNT Name]" /FTSVCPASSWORD="****" /UPDATEENABLED="False" /IACCEPTSQLSERVERLICENSETERMS /ALLOWUPGRADEFORSSRSSHAREPOINTMODE="True"  
```  
  
## <a name="examples-of-native-mode-installation"></a>本机模式安装示例  
  
```  
Setup.exe /q /ACTION="Install" /INSTANCENAME="MSSQLSERVER" /FEATURES="SQLEngine,Replication,SNAC,SNAC_SDK,Browser,Writer,AS,IS,MDS,Adv_SSMS,BC,BOL,Conn,SDK,DReplay_CTLR,DReplay_CLT,DQC,BIDS,FullText, RS,DQ,SSMS" /INSTANCEDIR="C:\Program Files\Microsoft SQL Server" /INSTALLSHAREDDIR="C:\Program Files\Microsoft SQL Server" /INSTALLSHAREDWOWDIR="C:\Program Files (x86)\Microsoft SQL Server" /INSTALLSQLDATADIR="C:\Program Files\Microsoft SQL Server" /SQLSVCACCOUNT="[Account Name]" /SQLSVCPASSWORD="********" /AGTSVCACCOUNT="[Account Nam]" /AGTSVCPASSWORD="********" /CTLRSVCACCOUNT="[Account Nam]" /CTLRSVCPASSWORD="********" /CLTSVCACCOUNT="[Account Nam]" /CLTSVCPASSWORD="********" /ASSVCACCOUNT="[Account Nam]" /ASSVCPASSWORD="********" /RSSVCACCOUNT="[Account Nam]" /RSSVCPASSWORD="********" /FTSVCACCOUNT="[Account Nam]" /FTSVCPASSWORD="********" /SECURITYMODE="SQL" /SAPWD="********" /PID="[Your PID Value]" /SQLSYSADMINACCOUNTS="[Account Nam]" "AutoSql Admin Group" /ASSYSADMINACCOUNTS="BUILTIN\ADMINISTRATORS" /UPDATEENABLED="False" /IACCEPTSQLSERVERLICENSETERMS /RSINSTALLMODE="DefaultNativeMode"  
```  
  
## <a name="see-also"></a>请参阅  
 [从命令提示符安装 SQL Server 2014](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)   
 [SysPrep 参数](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md#SysPrep)   
 [使用命令提示符安装 PowerPivot](../../sql-server/install/install-powerpivot-from-the-command-prompt.md)  
  
  
