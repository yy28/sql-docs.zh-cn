---
title: "安装 Reporting 和 Internet 信息服务的并行 |Microsoft 文档"
ms.custom: 
ms.date: 07/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- deploying [Reporting Services], IIS
ms.assetid: 9b651fa5-f582-4f18-a77d-0dde95d9d211
caps.latest.revision: 40
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: dcf26be9dc2e502b2d01f5d05bcb005fd7938017
ms.openlocfilehash: f7e12ebcec8e06828430e10c377205e2421f50f4
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---

# <a name="install-reporting-and-internet-information-services-side-by-side"></a>安装 Reporting 和 Internet 信息服务的并行

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

你可以安装和在同一台计算机上运行 SQL Server Reporting Services (SSRS) 和 Internet 信息服务 (IIS)。 所用 IIS 的版本确定了必须解决的互操作性问题。  
  
|IIS 版本|问题|说明|  
|-----------------|------------|-----------------|  
|8.0，8.5|一个应用程序收到发往另一个应用程序的请求。<br /><br /> HTTP.SYS 强制实施了 URL 保留的优先规则。 在向多个具有相同虚拟目录名称且共同监视端口 80 的应用程序发出请求时，如果目标应用程序的 URL 保留相对于另一个应用程序的 URL 保留较弱，则这些请求可能无法到达预期的目标。|在某些情况下，取代 URL 保留方案中另一个 URL 端点的已注册端点可能会收到发往其他应用程序的 HTTP 请求。<br /><br /> 为报表服务器 Web 服务和 [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] 使用唯一的虚拟目录名有助于避免发生这种冲突。<br /><br /> 本主题中提供了有关此方案的详细信息。|  
  
## <a name="precedence-rules-for-url-reservations"></a>URL 保留的优先规则  
 必须了解 URL 保留优先规则，才能解决 IIS 和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]之间的互操作性问题。 优先规则可以归纳为如下表述：具有更明确定义值的 URL 保留将首先收到与该 URL 相匹配的请求。  
  
-   指定了虚拟目录的 URL 保留将比忽略了虚拟目录的 URL 保留更为明确。  
  
-   指定了单个地址（IP 地址、完全限定的域名、网络计算机名称或主机名）的 URL 保留比使用通配符的 URL 保留更为明确。  
  
-   指定了强通配符的 URL 保留比指定了弱通配符的 URL 保留更为明确。  
  
 下面的几个示例演示了一系列 URL 保留，按照从最明确到最不明确的顺序排列：  
  
|示例|请求|  
|-------------|-------------|  
|`http://123.234.345.456:80/reports`|接收发送到的所有请求`http://123.234.345.456/reports`或`http://\<computername>/reports`如果域名服务可以为该主机名解析的 IP 地址。|  
|`http://+:80/reports`|只要 URL 包含“reports”虚拟目录名，就将接收发送到对于该计算机有效的任何 IP 地址或主机名的任何请求。|  
|`http://123.234.345.456:80`|接收的任何请求都指定`http://123.234.345.456`或`http://\<computername>`如果域名服务可以为该主机名解析的 IP 地址。|  
|`http://+:80`|对于映射到 **“所有已分配的”**的任何应用程序端点，接收尚未由其他应用程序接收的请求。|  
|`http://*:80`|对于映射到 **“所有未分配的”**的应用程序端点，接收尚未由其他应用程序接收的请求。|  
  
 端口冲突的一个迹象是看到以下错误消息：“System.IO.FileLoadException: 进程无法访问该文件，因为它正在被其他进程使用。 (HRESULT 异常: 0x80070020)”。  
  
## <a name="url-reservations-for-iis-80-85-with-sql-server-reporting-services"></a>IIS 8.0、 8.5 与 SQL Server Reporting Services 的 URL 保留项  
 使用上一节中概述的优先规则，即可以开始了解为 Reporting Services 和 IIS 定义的 URL 保留是如何提高互操作性的。 Reporting Services 接收为其应用程序明确指定了虚拟目录名的请求；IIS 接收所有的剩余请求，这些请求随后可定向到运行于 IIS 进程模型中的应用程序。  
  
|应用程序|URL 保留|说明|请求接收情况|  
|-----------------|---------------------|-----------------|---------------------|  
|报表服务器|`http://+:80/ReportServer`|针对端口 80 使用强通配符，带有报表服务器虚拟目录。|接收端口 80 上指定了报表服务器虚拟目录的所有请求。 报表服务器 Web 服务接收到 http:// 的所有请求\<计算机名 > / reportserver。|  
|Web 门户|`http://+:80/Reports`|针对端口 80 使用强通配符，带有 Reports 虚拟目录。|接收端口 80 上指定了 reports 虚拟目录的所有请求。 [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)]接收到 http:// 的所有请求\<计算机名 > / 报表。|  
|IIS|`http://*:80/`|针对端口 80 使用弱通配符。|接收端口 80 上尚未由其他应用程序接收的所有剩余请求。|  

## <a name="side-by-side-deployments-of-sql-server-reporting-services-on-iis-80-85"></a>通过并行部署的 IIS 8.0、 8.5 上的 SQL Server Reporting Services

 当 IIS 网站的虚拟目录名与 Reporting Services 所使用的虚拟目录名相同时，IIS 和 Reporting Services 之间会出现互操作性问题。 例如，假设您具有以下配置：  
  
-   IIS 中一个分配到端口 80 的网站，以及名为“Reports”的虚拟目录。  
  
-   安装在默认配置中，其中 URL 保留还指定了端口 80 的报表服务器实例和[!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)]应用程序也使用"Reports"作为虚拟目录名称。  
  
 在此配置，发送到 http:// 请求\<computername >: 80/reports 将收到[!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)]。 安装报表服务器实例之后，通过在 IIS 中的 Reports 虚拟目录访问的应用将不再接收请求。  
  
 如果您并行运行所部署的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]的新旧版本，则有可能会遇到上面描述的路由问题。 这是由于所有版本的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 都使用“ReportServer”和“Reports”作为报表服务器和 [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] 应用程序的虚拟目录名，从而增加了在 IIS 中拥有“reports”和“reportserver”虚拟目录的可能性。  
  
 为了确保所有的应用程序都能收到请求，请遵循下面的准则：  
  
-   对于 Reporting Services 安装，请使用 Reporting Services 所在端口上的 IIS 网站尚未使用的虚拟目录名。 如果存在冲突，请在“仅文件”模式（使用“安装”，但是不在安装向导中配置服务器选项）下安装 Reporting Services，以便可以在安装完成后配置虚拟目录。 您的配置存在冲突的一个迹象是看到以下错误消息：“System.IO.FileLoadException: 进程无法访问该文件，因为它正在被其他进程使用。 (HRESULT 异常: 0x80070020)”。  
  
-   对于手动配置的安装，请在所配置的 URL 中使用默认的命名约定。 如果以命名实例形式安装 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] ，请在创建虚拟目录时包括实例名称。  

## <a name="next-steps"></a>后续步骤

[配置报表服务器 Url](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
[配置 URL](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)   
[安装 Reporting Services 本机模式报表服务器](../../reporting-services/install-windows/install-reporting-services-native-mode-report-server.md)  

更多问题？ [尝试的 Reporting Services 论坛](http://go.microsoft.com/fwlink/?LinkId=620231)
