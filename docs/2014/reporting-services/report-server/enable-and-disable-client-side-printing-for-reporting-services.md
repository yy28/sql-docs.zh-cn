---
title: 启用和禁用 Reporting Services 的客户端打印 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 0e709c96-7517-4547-8ef6-5632f8118524
caps.latest.revision: 7
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 1271756e0a8caf036872e03aa1f55fa1da259860
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37313128"
---
# <a name="enable-and-disable-client-side-printing-for-reporting-services"></a>启用和禁用 Reporting Services 的客户端打印
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] ActiveX 控件**RSClientPrint**，提供了在浏览器中查看报表的客户端打印。 该控件显示一个自定义打印对话框，它支持其他打印对话框常见的功能。 这些功能包括打印预览、指定特定页和范围的页面选择、页边距和打印方向等功能。 虽然默认情况下将启用客户端打印功能，但是您也可以将其禁用，以禁止使用该功能。  
  
> [!NOTE]  
>  下载 ActiveX 控件需要管理员权限。  
  
## <a name="downloading-the-activex-control"></a>下载 ActiveX 控件  
 对于希望使用打印功能的每个用户来说，都必须下载并安装提供客户端打印功能的 ActiveX 控件。 第一次用户单击**打印机**报表工具栏中，Microsoft ActiveX 控件下载到计算机上的图标。 下载该控件后，**打印**当用户单击对话框中显示**打印机**图标。  
  
 根据浏览器设置的不同，系统可能会提示用户安装控件，阻止用户安装控件，或者在后台透明地安装控件。  
  
 有关[!INCLUDE[msCoName](../../includes/msconame-md.md)]Internet Explorer 中，通过指定影响 ActiveX 控件下载和安装的设置**ActiveX 控件和插件**中的节点**安全设置**页Web 内容区域。 以下设置基于 Web 区域安全首选项，确定用户是否可以下载和运行打印控件：  
  
-   下载已签名的 ActiveX 控件。  
  
-   对标记为可安全执行脚本的 ActiveX 控件执行脚本。  
  
-   运行 ActiveX 控件和插件。  
  
 想要使用的用户**RSClientPrint**要执行客户端打印功能必须启用以下：  
  
-   **下载已签名的 ActiveX 控件**并**脚本的 ActiveX 控件标记为可安全执行脚本**以允许安装。  
  
-   **运行 ActiveX 控件和插件**为正在进行的打印操作。  
  
 **RSClientPrint** ActiveX 控件进行签名，这意味着它包含有效的数字证书从[!INCLUDE[msCoName](../../includes/msconame-md.md)]。  
  
## <a name="enabling-and-disabling-client-side-printing"></a>启用和禁用客户端打印功能  
 报表服务器管理员可以通过设置报表服务器系统属性禁用打印功能的选项**EnableClientPrinting**到`false`。 这将对该服务器管理的所有报表禁用客户端打印功能。 默认情况下**EnableClientPrinting**设置为`true`。 您可以通过下列方式禁用客户端打印功能：  
  
-   对于本机模式下的报表服务器 ：  
  
    1.  使用管理权限启动 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 。  
  
    2.  连接到 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中的报表服务器实例。  
  
    3.  右键单击报表服务器节点，然后单击“属性”。 如果 **“属性”** 选项被禁用，请确认您是在使用管理权限启动 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 。  
  
    4.  选择**允许下载 ActiveX 客户端打印控件**。  
  
    5.  单击“确定” 。  
  
-   对于 SharePoint 模式报表服务器 ：  
  
    1.  在 SharePoint 管理中心中，单击 **“应用程序管理”**。  
  
    2.  单击 **“管理服务应用程序”**。  
  
    3.  单击您的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务应用程序的名称，然后单击 SharePoint 功能区中的 **“管理”** 。  
  
    4.  单击 **“系统设置”**。  
  
    5.  选择 **“启用客户端打印”**。 **“启用客户端打印”** 选项位于页面的底部附近。  
  
    6.  单击“确定” 。  
  
-   编写脚本或代码，设置报表服务器系统属性**EnableClientPrinting**到 `false.`  
  
 下面的示例脚本说明了一种禁用客户端打印功能的方法。 编译并运行以下 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 代码，以将 **EnableClientPrinting** 属性设置为 **False**。 在运行代码后，请重新启动 IIS。  
  
### <a name="sample-script"></a>示例脚本  
  
```  
Imports System  
Imports System.Web.Services.Protocols  
Class Sample  
   Public Shared Sub Main()  
Dim rs As New ReportingService()  
      rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
        Dim props(0) As [Property]  
        Dim setProp As New [Property]  
        setProp.Name = "EnableClientPrinting"  
        setProp.Value = “False”   
        props(0) = setProp  
        Try  
            rs.SetSystemProperties(props)  
        Catch ex As System.Web.Services.Protocols.SoapException  
            Console.Write(ex.Detail.InnerXml)  
        Catch e as Exception  
            Console.Write(e.Message)  
        End Try  
    End Sub 'Main  
End Class 'Sample  
```  
  
  
