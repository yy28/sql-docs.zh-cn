---
title: 报表服务器配置为电子邮件传递 （SSRS 配置管理器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services], distributing
- report servers [Reporting Services], e-mail delivery
- remote SMTP service [Reporting Services]
- distributing reports [Reporting Services], e-mail
- CDO
- Collaboration Data Objects
- SMTP settings [Reporting Services]
- e-mail [Reporting Services]
- sending reports
- mail [Reporting Services]
- local SMTP service [Reporting Services]
ms.assetid: b838f970-d11a-4239-b164-8d11f4581d83
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 17e210356aadaa17394abf0b68bf9303461943d2
ms.sourcegitcommit: 96032813f6bf1cba680b5e46d82ae1f0f2da3d11
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/15/2019
ms.locfileid: "54300334"
---
# <a name="configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager"></a>针对电子邮件传递配置报表服务器（SSRS 配置管理器）

  > [!div class="nextstepaction"]
  > [请分享你有关 SQL Docs 表的内容的反馈 ！](https://aka.ms/sqldocsurvey)


  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 包括电子邮件传递扩展插件，以便可以通过电子邮件分发报表。 根据定义电子邮件订阅的方式，传递可能由通知、链接、附件或嵌入报表组成。 电子邮件传递扩展插件可与现有的邮件服务器技术一起使用。 邮件服务器必须是 SMTP 服务器或转发器。 报表服务器通过操作系统提供的协作数据对象 (CDO) 库 (cdosys.dll) 连接到 SMTP 服务器。  
  
 默认情况下，未配置报表服务器电子邮件传递扩展插件。 必须使用 Reporting Services 配置管理器最低配置此扩展插件。 若要设置高级属性，必须编辑 `RSReportServer.config` 文件。 如果无法将报表服务器配置为使用此扩展插件，则可以将报表传递到共享文件夹。 有关详细信息，请参阅 [File Share Delivery in Reporting Services](../../reporting-services/subscriptions/file-share-delivery-in-reporting-services.md)。  
  
||  
|-|  
|[!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 本机模式|  
  
 
  
##  <a name="bkmk_configuration_requirements"></a> 配置要求  
  
-   报表服务器电子邮件传递在协作数据对象 (CDO) 上实现，且需要本地或远程的简单邮件传输协议 (SMTP) 服务器或 SMTP 转发器。 所有 Windows 操作系统都不支持 SMTP。 如果使用的是基于 Itanium 的 Windows Server 2008 版本，则也不支持 SMTP。 有关通过 CDO 提供的配置选项的详细信息，请参阅 MSDN 上的 [Configuration CoClass](https://go.microsoft.com/fwlink/?LinkId=98237) （配置 CoClass）。  
  
-   报表服务器服务帐户必须对 SMTP 服务器拥有权限才能发送邮件。  
  
-   电子邮件传递扩展插件在电子邮件附件中使用 UTF-8 编码。 您无法修改此编码；HTML 呈现扩展插件仅支持 UTF-8。  
  
> [!NOTE]  
>  默认电子邮件传递扩展插件不支持给待发邮件进行数字签名或加密。  
  
 
  
##  <a name="bkmk_configure_for_local_or_remote_SMTP"></a> 报表服务器配置为本地或远程 SMTP 服务  
 可以使用本地 SMTP 服务或远程 SMTP 服务器或转发器来支持电子邮件传递。 如果具有现有远程 SMTP 服务器的访问权限，则应该考虑使用该服务器。 若没有可用的 SMTP 服务器或随后由于计算机连接失败而遇到报表传递错误，则应该进行切换以使用本地 SMTP 服务。 有关如何为本地或远程服务配置报表服务器的详细信息，将稍后在本主题中进一步说明。  
  
  
  
##  <a name="bkmk_setting_email_delivery"></a> 为电子邮件传递设置配置选项  
 必须先设置确定使用哪一个 SMTP 服务器的配置值，才能使用报表服务器电子邮件传递。  
  
 若要针对电子邮件传递配置报表服务器，请执行下列操作：  
  
-   如果要仅指定一个 SMTP 服务器和一个具有发送电子邮件权限的用户帐户，则使用 Reporting Services 配置管理器。 以下是配置报表服务器电子邮件传递扩展插件所需的最低设置。 有关详细信息，请参阅[电子邮件设置-配置管理器&#40;SSRS 本机模式&#41;](../../reporting-services/install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md)并[Reporting Services 中的电子邮件传递](../../reporting-services/subscriptions/e-mail-delivery-in-reporting-services.md)。  
  
-   （可选）使用文本编辑器在 RSreportserver.config 文件中指定其他设置。 此文件包含报表服务器电子邮件传递的所有配置设置。 如果要使用本地 SMTP 服务器或将电子邮件限定传递到特定主机，则需要在这些文件中指定其他设置。 有关查找和修改配置文件的详细信息，请参阅[修改 Reporting Services 配置文件&#40;RSreportserver.config&#41; ](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md) SQL Server 联机丛书中。  
  
> [!NOTE]  
>  报表服务器电子邮件设置都是基于 CDO。 若要了解有关特定设置的更多详细信息，可以参考 CDO 产品文档。  
  

  
##  <a name="bkmk_example_config_file"></a> 示例报表服务器电子邮件配置  
 下面的示例说明了远程 SMTP 服务器的 RSreportserver.config 文件中的设置： 若要了解设置说明及有效值，请参阅 [ssNoVersion](../../reporting-services/report-server/rsreportserver-config-configuration-file.md) 联机丛书中的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Books Onl联机丛书中的e or the CDO product documentation.  
  
```  
<RSEmailDPConfiguration>  
     <SMTPServer>mySMTPServer.Adventure-Works.com</SMTPServer>  
     <SMTPServerPort></SMTPServerPort>  
     <SMTPAccountName></SMTPAccountName>  
     <SMTPConnectionTimeout></SMTPConnectionTimeout>  
     <SMTPServerPickupDirectory></SMTPServerPickupDirectory>  
     <SMTPUseSSL></SMTPUseSSL>  
     <SendUsing>2</SendUsing>  
     <SMTPAuthenticate></SMTPAuthenticate>  
     <From>my-rs-email-account@Adventure-Works.com</From>  
     <EmbeddedRenderFormats>  
          <RenderingExtension>MHTML</RenderingExtension>  
     </EmbeddedRenderFormats>  
     <PrivilegedUserRenderFormats></PrivilegedUserRenderFormats>  
     <ExcludedRenderFormats>  
          <RenderingExtension>HTMLOWC</RenderingExtension>  
          <RenderingExtension>NULL</RenderingExtension>  
     </ExcludedRenderFormats>  
     <SendEmailToUserAlias>True</SendEmailToUserAlias>  
     <DefaultHostName></DefaultHostName>  
     <PermittedHosts>  
          <HostName>Adventure-Works.com</HostName>  
          <HostName>hotmail.com</HostName>  
     </PermittedHosts>  
</RSEmailDPConfiguration>  
```  
  

  
##  <a name="bkmk_setting_TO_field"></a> 配置选项设置为：消息中的“收件人：”字段的配置选项  
 根据“管理单独的订阅”  任务授予的权限而创建的用户定义订阅包含基于域用户帐户的预设用户名。 用户创建订阅时，“收件人:”  字段中的收件人姓名会使用创建该订阅的人员的域用户帐户自行转换为地址。  
  
 如果您所用的 SMTP 服务器或转发器使用了不同于域用户帐户的电子邮件帐户，则 SMTP 服务器尝试将报表传递给该用户时，报表传递会失败。  
  
 若要解决该问题，可以修改允许用户在“收件人:”  字段中输入名称的配置设置：  
  
1.  使用文本编辑器打开 RSReportServer.config。  
  
2.  将 `SendEmailToUserAlias` 设置为 `False`。  
  
3.  将 `DefaultHostName` 设置为 SMTP 服务器或转发器的域名系统 (DNS) 名称或 IP 地址。  
  
4.  保存该文件。  
  
  
  
##  <a name="bkmk_options_remote_SMTP"></a> 远程 SMTP 服务的配置选项  
 报表服务器与 SMTP 服务器或转发器之间的连接是由下列配置设置决定的：  
  
-   `SendUsing` 指定发送消息的方法。 您可以选择网络 SMTP 服务或本地 SMTP 服务拾取目录。 若要使用远程 SMTP 服务，必须在 RSReportServer.config 文件中将此值设置为 **2** 。  
  
-   `SMTPServer` 指定远程 SMTP 服务器或转发器。 如果使用远程 SMTP 服务器或转发器，则必须指定此值。  
  
-   `From` 设置显示在电子邮件的“发件人：”行中的值。 如果使用远程 SMTP 服务器或转发器，则必须指定此值。  
  
 其他用于远程 SMTP 服务的值包括以下值（请注意，除非您要覆盖默认值，否则无需指定这些值）：  
  
-   **SMTPServerPort** 配置为端口 25。  
  
-   “” 指定如何将报表服务器连接到远程 SMTP 服务器。 默认值为 0（或不进行身份验证）。 这种情况下，将通过匿名访问创建连接。 报表服务器和 SMTP 服务器可能需要成为同一域的成员，这取决于域配置。  
  
     若要向受限制的通讯组列表发送电子邮件（例如，只接受经过身份验证的帐户发来的邮件的通讯组列表），则将 **“SMTPAuthenticate”** 设置为 **“2”**。  
  

  
##  <a name="bkmk_options_local_SMTP"></a> 本地 SMTP 服务的配置选项  
 若要测试报表服务器电子邮件传递或解决所遇到的疑难问题，则配置本地 SMTP 服务会很有用。 默认情况下，不启用本地 SMTP 服务。 有关如何启用它的说明，请参阅[报表服务器配置为电子邮件传递 （SSRS 配置管理器）](../../../2014/sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)并[电子邮件设置-配置管理器&#40;SSRS 本机模式&#41;](../../reporting-services/install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md).  
  
 报表服务器与本地 SMTP 服务器或转发器之间的连接是由下列配置设置决定的：  
  
-   `SendUsing` 设置为**1**。  
  
-   将**SMTPServerPickupDirectory** 设置为本地驱动器中的文件夹。  
  
    > [!NOTE]  
    >  请确保不要设置`SMTPServer`如果使用本地 SMTP 服务器。  
  
-   `From` 设置显示在电子邮件的“发件人：”行中的值。 此值是必需的。  
  
 
  
##  <a name="bkmk_use_configuration_manager"></a> 若要配置报表服务器电子邮件使用 Reporting Services 配置管理器  
  
1.  请验证报表服务器 Windows 服务是否对 SMTP 服务器拥有 `Send As` 权限。  
  
2.  启动 Reporting Services 配置管理器，然后连接到报表服务器实例。  
  
3.  在“电子邮件设置”页上，输入 SMTP 服务器的名称。 此值可以是 IP 地址、企业 Intranet 上计算机的 UNC 名称或者完全限定域名。  
  
4.  在 **“发件人地址”** 中，输入有权从 SMTP 服务器发送电子邮件的帐户的名称。  
  
5.  单击 **“应用”**。  
  

  
##  <a name="bkmk_confiugre_remote_SMTP"></a> 若要配置报表服务器的远程 SMTP 服务  
  
1.  请验证报表服务器 Windows 服务是否对 SMTP 服务器拥有 `Send As` 权限。  
  
2.  在文本编辑器中打开 RSReportServer.config 文件。  
  
3.  验证 <`UrlRoot`> 已设置为报表服务器 URL 地址。 此值是在您配置报表服务器时设置的，应该已经填写。 如果未设置此值，则请键入报表服务器 URL 地址。  
  
4.  在“传递”部分中，查找 <`ReportServerEmail`>。  
  
5.  在 <`SMTPServer`> 中，键入 SMTP 服务器的名称。 此值可以是 IP 地址、企业 Intranet 上计算机的 UNC 名称或者完全限定域名。  
  
6.  验证 <`SendUsing`> 已设置为 2。 如果将其设置为其他值，则报表服务器无法配置为使用远程 SMTP 服务。  
  
7.  在 <`From`> 中，键入有权从 SMTP 服务器发送电子邮件的帐户的名称。  
  
8.  保存该文件。  
  
     报表服务器将自动使用新的设置；不需要重新启动该服务。 您可以指定其他 SMTP 设置，以进一步配置如何将 SMTP 服务器用于报表服务器电子邮件传递。 有关详细信息，请参阅 [ssNoVersion](../../../2014/sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md) 和 [ssNoVersion](../../reporting-services/report-server/rsreportserver-config-configuration-file.md) 联机丛书中的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Books Onl联机丛书中的e.  
  

  
##  <a name="bkmk_confiugre_local_SMTP"></a> 若要配置报表服务器的本地 SMTP 服务  
  
1.  在“控制面板”中，单击 **“添加或删除程序”**。  
  
2.  单击 **“添加/删除 Windows 组件”** 启动 Windows 组件向导。  
  
3.  选择 **“应用程序服务器”** ，然后单击 **“详细信息”**。  
  
4.  选择 **“Internet 信息服务 (IIS)”** ，然后单击 **“详细信息”**。  
  
5.  选中 **“SMTP 服务”** 复选框，然后单击 **“确定”**。  
  
6.  在 Windows 组件向导中，单击 **“下一步”**。 单击 **“完成”**。  
  
7.  验证服务是否正在 **“服务”** 控制台上运行。  
  
8.  在文本编辑器中打开 **RSReportServer.config** 文件。  
  
9. 验证 `<UrlRoot>` 已设置为报表服务器 URL 地址。 此值是在您配置报表服务器时设置的，应该已经填写。 如果未设置此值，则请键入报表服务器 URL 地址。  
  
10. 在“传递”部分中，查找 `<ReportServerEmail>.`。  
  
11. 在 `<SMTPServer>`中，清除此设置的所有值，但不要删除标记。  
  
12. 将 `<SendUsing>` 设置为 1。 如果将其设置为其他值，则无法将报表服务器配置为使用本地 SMTP 服务。  
  
13. 将 `<SMTPServerPickupDirectory>` 设置为本地驱动器上的文件夹。  
  
14. 将 `<From>` 设置为有权从 SMTP 服务器发送电子邮件的帐户。  
  
15. 保存该文件。  
  
 
  
## <a name="see-also"></a>请参阅  
 [Reporting Services Configuration Manager（本机模式）](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)  
  
  
