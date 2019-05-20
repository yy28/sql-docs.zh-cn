---
title: 设置 Reporting Services 脚本文件的格式 | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: conceptual
helpviewer_keywords:
- scripts [Reporting Services], formats
- formats [Reporting Services], script files
ms.assetid: 85a207dd-4e0f-4d40-a41e-0c75f65d719c
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 1979e19b3d93e9687d6abb137758bc71548b10ce
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 05/14/2019
ms.locfileid: "65577798"
---
# <a name="format-a-reporting-services-script-file"></a>设置 Reporting Services 脚本文件的格式
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 脚本是用来定义 Reporting Services SOAP API 的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic .NET 代码文件，该文件是针对基于 Web 服务描述语言 (WSDL) 构建的代理编写的。 脚本文件以 Unicode 或 UTF-8 文本文件形式存储，扩展名为 .rss。  
  
 脚本文件充当 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 模块，以包含用户定义的过程和模块级变量。 为了使脚本文件成功运行，其中必须包含 Main 过程。 Main 过程是脚本文件运行时访问的第一个过程。 在 Main 过程中，可以添加您的 Web 服务操作并运行您的用户定义子过程。 下面的代码将创建一个 Main 过程：  
  
```  
Public Sub Main()  
    ' Your code goes here.  
End Sub  
```  
  
 脚本环境会自动连接到报表服务器，创建 Web 代理类，并生成一个指向 Web 服务代理对象的引用变量 (*rs*)。 所创建的各个语句只需引用 *rs* 模块级变量即可执行 Web 服务库中所提供的任何 Web 服务操作。 下面的 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 代码从脚本文件中调用 Web 服务 <xref:ReportService2010.ReportingService2010.ListChildren%2A> 方法：  
  
```  
Public Sub Main()  
    Dim items() As CatalogItem  
    items = rs.ListChildren("/", True)  
  
    Dim item As CatalogItem  
    For Each item In items  
        Console.WriteLine(item.Name)  
    Next item  
End Sub   
```  
  
> [!IMPORTANT]  
>  用户凭据由脚本环境管理，并通过使用 RS.exe 来传递命令提示符参数。 尽管可以使用 *rs* 变量来设置对 Web 服务的身份验证，但是仍建议您使用脚本环境。 不必在脚本文件本身中对 Web 服务进行身份验证。 有关对脚本环境进行身份验证的详细信息，请参阅 [RS.exe 实用工具 (SSRS)](../../reporting-services/tools/rs-exe-utility-ssrs.md)。  
  
 在脚本文件中不必声明命名空间。 通过脚本环境提供了几个有用的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 命名空间： **System.Web.Services**, **System.Web.Services.Protocols**, **System.Xml**和 **System.IO**。  
  
 有关脚本示例，请参阅 [SQL Server Reporting Services Product Samples](https://go.microsoft.com/fwlink/?LinkId=177889)（SQL Server Reporting Services 产品示例）。  
  
## <a name="see-also"></a>另请参阅  
 [报表服务器 Web 服务](../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [技术参考 (SSRS)](../../reporting-services/technical-reference-ssrs.md)   
 [RS.exe 实用工具 (SSRS)](../../reporting-services/tools/rs-exe-utility-ssrs.md)  
  
  
