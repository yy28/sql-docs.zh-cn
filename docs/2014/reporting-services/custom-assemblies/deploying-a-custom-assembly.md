---
title: 部署自定义程序集 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- deploying custom assemblies [Reporting Services]
- custom assemblies [Reporting Services], deploying
- custom assemblies [Reporting Services], updating
- updating custom assemblies
ms.assetid: c6674cd8-0de7-4a5a-9e7c-12ffa49f6fd2
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 98f498ceb1f0d2d05261c08e14d7adb0b7cfd716
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56020688"
---
# <a name="deploying-a-custom-assembly"></a>部署自定义程序集
  为了在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中部署自定义程序集，请将程序集同时放到报表设计器和报表服务器的应用程序文件夹中。 默认情况下，将在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中向自定义程序集授予 `Execution` 权限。 若要向自定义程序集授予超过执行权限的特权，需要对报表服务器编辑 rssrvpolicy.config 配置文件，并对报表设计器预览窗口编辑 rspreviewpolicy.config 配置文件。 也可以选择将自定义程序集安装到全局程序集缓存 (GAC) 中。  
  
> [!NOTE]  
>  报表设计器有两种预览模式：“预览”选项卡以及在以 `DebugLocal` 模式下启动报表项目时启动的弹出式预览窗口。 “预览”选项卡使用 `FullTrust` 权限集执行所有报表表达式，它不应用安全策略设置。 弹出式预览窗口旨在模拟报表服务器的功能，因此具有策略配置文件，您或管理员必须修改该文件才能在报表设计器中使用自定义程序集。 此弹出式预览还锁定自定义程序集。 因此，您需要关闭预览窗口，才能修改或更新自定义程序集代码。  
  
###### <a name="to-deploy-a-custom-assembly-in-reporting-services"></a>在 Reporting Services 中部署自定义程序集  
  
1.  将自定义程序集从生成位置复制到报表服务器的 bin 文件夹或报表设计器文件夹中。 报表服务器的 bin 文件夹的默认位置为 %ProgramFiles%\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\Reporting Services\ReportServer\bin。 报表设计器的默认位置为 %ProgramFiles%\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies。  
  
     通过将自定义程序集放入报表服务器 bin 文件夹中，您可以发布引用自定义程序集的报表；而通过将其放在报表设计器文件夹中，您可以在报表设计器中运行和调试引用自定义程序集的报表。  
  
     如果您需要向自定义程序集代码授予超过默认执行权限的权限，请执行以下操作：  
  
2.  打开相应的配置文件。 rssrvpolicy.config 的默认位置为 %ProgramFiles%\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\Reporting Services\ReportServer。 rspreviewpolicy.config 的默认位置为 %ProgramFiles%\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies。  
  
3.  为自定义程序集添加代码组。 有关详细信息，请参阅[安全开发 (Reporting Services)](../extensions/secure-development/secure-development-reporting-services.md)。  
  
## <a name="updating-custom-assemblies"></a>更新自定义程序集  
 有时，您可能需要更新当前正在由多个已发布报表引用的自定义程序集的版本。 如果该程序集已位于报表服务器的 bin 目录或报表服务器中，并且程序集的版本号以某种方式递增或更改，则当前发布的报表将不再正常工作。 您需要在报表定义的 `CodeModules` 元素中更新所引用的程序集的版本，并重新发布报表。 如果您知道您将频繁地更新自定义程序集，并且您当前发布的报表需要引用新程序集，则您可能需要考虑在特定程序集的所有更新中使用同一个版本号。  
  
 如果您不需要当前发布的报表引用程序集的新版本，则可以将自定义程序集部署到全局程序集缓存。 全局程序集缓存可以保持同一个程序集的多个版本，这样，您当前的报表可以引用程序集的前一个版本，而新发布的报表可以引用更新后的程序集。 此外，另一个方法是设置报表服务器的绑定重定向，以强制将旧程序集的所有请求重定向到新程序集。 您需要修改报表服务器 Web.config 文件和报表服务器 ReportService.exe.config 文件。 该条目可能如下所示：  
  
```  
<configuration>  
   <runtime>  
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
         <dependentAssembly>  
            <assemblyIdentity name="myAssembly"  
                              publicKeyToken="32ab4ba45e0a69a1"  
                              culture="neutral" />  
            <bindingRedirect oldVersion="1.0.0.0"  
                             newVersion="2.0.0.0"/>  
         </dependentAssembly>  
      </assemblyBinding>  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>请参阅  
 [将自定义程序集用于报表](using-custom-assemblies-with-reports.md)   
 [使用程序集和全局程序集缓存](https://go.microsoft.com/fwlink/?LinkId=63912)  
  
  
