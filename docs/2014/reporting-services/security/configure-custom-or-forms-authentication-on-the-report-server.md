---
title: 在报表服务器上配置自定义身份验证或窗体身份验证 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Forms authentication, configuring
- custom authentication [Reporting Services]
ms.assetid: e8601a8f-e66d-4649-8e4d-a46ca20ec7d0
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8969e3202a9c58b46fac2116912e3d90474d7072
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63242651"
---
# <a name="configure-custom-or-forms-authentication-on-the-report-server"></a>在报表服务器上配置自定义身份验证或窗体身份验证
  Reporting Services 提供了可扩展的体系结构，该体系结构允许您插入自定义的或基于窗体的身份验证模块。 如果部署要求不包含 Windows 集成安全性或基本身份验证，则可考虑实现自定义的身份验证扩展插件。 使用自定义身份验证的最常见情形是支持对 Web 应用程序的 Internet 或 Extranet 访问。 使用自定义身份验证扩展插件替换默认的 Windows 身份验证扩展插件，可更好地控制如何授予外部用户访问报表服务器的权限。  
  
 实际上，部署自定义身份验证扩展插件需要执行多个步骤，包括复制程序集和应用程序文件，修改配置文件以及测试。 本主题仅重点介绍您要在配置文件中指定的身份验证设置。  
  
> [!NOTE]  
>  若要创建自定义身份验证扩展插件，需要自定义代码并掌握 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 安全性方面的专业知识。 如果您不希望创建自定义身份验证扩展插件，则可以使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory 组和帐户，但应大幅减小报表服务器部署的范围。 有关自定义身份验证的详细信息，请参阅 [Implementing a Security Extension](../extensions/security-extension/implementing-a-security-extension.md)。  
  
 此外，如果希望在与 SharePoint 产品集成的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 环境中使用窗体身份验证或自定义身份验证扩展插件，则必须将 SharePoint 站点配置为使用您所选的身份验证方法。 有关在 SharePoint 中配置身份验证的详细信息，请参阅 [Developer Network (MSDN) 上的](https://go.microsoft.com/fwlink/?LinkId=115575) Authentication Samples [!INCLUDE[msCoName](../../includes/msconame-md.md)] 身份验证示例。  
  
### <a name="to-configure-a-report-server-to-use-custom-authentication"></a>将报表服务器配置为使用自定义身份验证  
  
1.  在文本编辑器中打开 RSReportServer.config。  
  
2.  查找 <`Authentication`>。  
  
3.  复制以下 XML 结构：  
  
    ```  
    <Authentication>  
          <AuthenticationTypes>  
                 <Custom />  
          </AuthenticationTypes>  
          <EnableAuthPersistence>true</EnableAuthPersistence>  
    </Authentication>  
    ```  
  
4.  将它粘贴到的现有条目 <`Authentication`>。  
  
     请注意，不能将 `Custom` 与其他身份验证类型一起使用。  
  
5.  保存该文件。  
  
6.  打开报表服务器的 Web.config 文件。 默认情况下，该文件位于 \Program Files\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\ReportServer 下。  
  
7.  查找`authentication mode`并将其设置`Forms`。  
  
    ```  
    <authentication mode = "Forms" />  
    ```  
  
8.  查找 `identity impersonate` 并将其设置为 `False`。  
  
    ```  
    <identity impersonate = "false" />  
    ```  
  
9. 打开报表管理器的 Web.config 文件。 默认情况下，该文件位于 \Program Files\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\ReportManager 下。  
  
10. 查找`authentication mode`并将其设置`Forms`。  
  
    ```  
    <authentication mode = "Forms" />  
    ```  
  
11. 查找 `identity impersonate` 并将其设置为 `False`。  
  
    ```  
    <identity impersonate = "false" />  
    ```  
  
12. 将 `PassThroughCookies` 元素结构添加到配置文件中。 有关详细信息，请参阅 [配置报表管理器以便传递自定义身份验证 Cookie](configure-the-web-portal-to-pass-custom-authentication-cookies.md)。  
  
13. 保存该文件。  
  
14. 如果配置了扩展部署，请对该部署中的其他报表服务器重复以上所有步骤。  
  
15. 重新启动报表服务器以清除当前打开的任何会话。  
  
## <a name="see-also"></a>请参阅  
 [Implementing a Security Extension](../extensions/security-extension/implementing-a-security-extension.md)   
 [针对报表服务器的身份验证](authentication-with-the-report-server.md)   
 [RSReportServer 配置文件](../report-server/rsreportserver-config-configuration-file.md)   
 [在报表服务器上配置基本身份验证](configure-basic-authentication-on-the-report-server.md)   
 [在报表服务器上配置 Windows 身份验证](configure-windows-authentication-on-the-report-server.md)  
  
  
