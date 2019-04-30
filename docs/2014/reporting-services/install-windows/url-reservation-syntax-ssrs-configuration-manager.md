---
title: URL 预留语法（SSRS 配置管理器）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- URL reservations
ms.assetid: 30e4be2e-e65d-462c-895a-5a0a636d042f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 885e8ffb9eaa02aae02db590c8d042dadb1f2ab0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63224922"
---
# <a name="url-reservation-syntax--ssrs-configuration-manager"></a>URL 预留语法（SSRS 配置管理器）
  本主题介绍报表服务器 Web 服务和报表管理器的 URL 字符串的各部分。 该内部存储的 URL 字符串的结构不同于在浏览器窗口的地址栏中键入的 URL 的结构。 URL 预留字符串会在你配置 URL 时显示在 Reporting Services 配置工具的“结果”窗口中，也会出现在 RSReportServer.config 文件中。 如果要解决 URL 预留中存在的问题，或者要查询 HTTP.SYS 以查看服务器上定义的内部 URL 预留，则了解该 URL 字符串的定义方式会很有用。  
  
## <a name="url-syntax"></a>URL 语法  
 报表服务器 URL 存储在 `UrlString` 元素和 `VirtualDirectory` 元素中。 将 `UrlString` 和 `VirtualDirectory` 区分为不同元素的原因是您可以具有多个 URL 字符串，但每个 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 应用程序只有一个虚拟目录名。  
  
 在 HTTP.SYS 中，URL 预留包括 `UrlString` 和 `VirtualDirectory`。 URL 预留的语法包含以下部分：  
  
 \<scheme>://\<hostname>:\<port>/\<virtualdirectory>  
  
 下表说明了每个属性及其有效值。  
  
|属性|有效值|Description|  
|--------------|------------------|-----------------|  
|Scheme|http 或 https|针对非 SSL 连接和 SSL 连接的前缀。|  
|Hostname|(+) 强通配符，相当于 IP 地址的值为“(所有已分配的)”。<br /><br /> (\*) 弱通配符，相当于 IP 地址为“(所有未分配的)”。<br /><br /> 完全限定域名<br /><br /> 计算机名称<br /><br /> IP 地址 (IPV4)<br /><br /> IP 地址 (IPV6)|标识网络上的服务器。<br /><br /> (+) 强通配符是默认值。 HTTP.SYS 将接受给定端口和虚拟目录组合的所有网络适配器上的所有请求。 报表服务器将接受该端口上的任何请求。<br /><br /> (\*) 弱通配符。 HTTP.SYS 接受给定端口和虚拟目录组合的所有网络适配器上未由其他 URL 预留处理的所有请求。<br /><br /> 计算机名称是网络上计算机的 NETBIOS 名称。<br /><br /> 完全限定域名包含域地址和服务器名，如域控制器或公共域名服务器中所注册的那样。<br /><br /> IP 地址 (IPV4) 是采用 IPV4 格式 *nnn.nnn.nnn.nnn*的计算机网络适配器的 IP 地址。<br /><br /> IP 地址 (IPV6) 是采用 IPV6 格式的、计算机网络适配器的 IP 地址：\<header>:\<header>:*nnn.nnn.nnn.nnn*。|  
|端口|80<br /><br /> 443<br /><br /> \<custom>|端口 80 是与服务器之间的 HTTP 请求的标准端口。<br /><br /> 端口 443 是用于 SSL 连接的标准端口。<br /><br /> 您可以使用任何未被其他应用程序保留的端口。|  
|VirtualDirectory|ReportServer *[_InstanceName]*<br /><br /> Reports *[_InstanceName]*<br /><br /> \<custom>|指定应用程序的名称。 该值是一个字符串。 默认情况下， [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 使用 ReportServer 和 Reports 作为报表服务器 Web 服务和报表管理器应用程序的应用程序名称。 您可以根据需要使用不同的名称。<br /><br /> 此值是必需的。 它用于标识应用程序。<br /><br /> 为每个应用程序实例仅指定一个虚拟目录。 若要为同一实例中的同一应用程序创建多个 URL，可以创建 `UrlString` 的多个版本。 若要为多个应用程序实例创建唯一的虚拟目录名，可以考虑将实例名称包含在虚拟目录名中，即使用下划线字符 (_) 追加实例名称。 *InstanceName* 是可选的，但是如果同一台计算机上有多个实例，则建议使用此选项。 有关如何为命名实例设置预留的详细信息，请参阅[多实例报表服务器部署的 URL 预留（SSRS 配置管理器）](url-reservations-for-multi-instance-report-server-deployments.md)。<br /><br /> 虚拟目录的值不区分大小写。 您可以使用任意字符串，只要它不包含 URL 分隔符或 URL 编码即可。|  
  
## <a name="see-also"></a>请参阅  
 [配置报表服务器 URL（SSRS 配置管理器）](configure-report-server-urls-ssrs-configuration-manager.md)   
 [配置 URL（SSRS 配置管理器）](configure-a-url-ssrs-configuration-manager.md)  
  
  
