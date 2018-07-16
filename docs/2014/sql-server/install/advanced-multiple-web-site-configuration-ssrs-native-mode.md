---
title: 高级多网站配置 （SSRS 本机模式） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.advancedmultiplewebsiteconfig.F1
ms.assetid: af4ede43-2225-45b5-ae7e-9202411551ba
caps.latest.revision: 6
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: eafcc3b69916ba253b430a61fb5b510eb3480d91
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37220727"
---
# <a name="advanced-multiple-web-site-configuration-ssrs-native-mode"></a>高级多网站配置（SSRS 本机模式）
  使用此对话框可创建和管理用于访问报表服务器或报表管理器的 URL。 **“高级多网站配置”** 对话框用于创建附加 URL 和包含主机标头名称的自定义 URL，或者用于指定 IPv4 或 IPv6 格式的 IP 地址。  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 本机模式。  
  
 如果要配置多种不同的方式来访问报表服务器，则创建多个 URL 非常有用。 例如，通过 Intranet 和 Extranet 连接访问报表服务器通常对于每种类型的连接需要具有不同的 URL。  
  
 若要打开**高级多网站配置**对话框中，单击**高级**上**Web 服务 URL**或**报表管理器 URL**页中[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]配置管理器。 **“高级多网站配置”** 对话框打开后，可以单击 **“添加”** 或 **“编辑”** 来定义新的 URL，或者修改或删除现有的 URL。  
  
 单击 **“确定”** 保存所做的更改。 如果添加或删除 URL 后，没有先单击 **“确定”** 就关闭了对话框，所做的更改将丢失。  
  
## <a name="options"></a>“常规”  
 **IP 地址**  
 标识 TCP/IP 网络上的报表服务器计算机。 有效值包括：  
  
-   **“所有已分配的”** 指定分配给计算机的任何 IP 地址均可用在指向报表服务器应用程序的 URL 中。 此值还包含友好主机名（如计算机名），域名服务器可将该主机名解析为分配给该计算机的 IP 地址。 此为 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] URL 的默认值。  
  
-   **“所有未分配的”** 指定报表服务器将接受任何未完全匹配 IP 地址或主机名的请求。 如果其他 Web 应用程序已在使用此值，请不要再使用它。 如果仍使用此值，将中断其他应用程序的服务。  
  
-   **127.0.0.1** 用于访问本地主机。 它支持对报表服务器计算机进行本地管理。 如果仅选择此值，则只有在本地登录到报表服务器计算机的用户可以访问应用程序。  
  
-   *Nnn.nnn.nnn.nnn* 是计算机网络适配器的 IPv4 地址。 如果您的网络使用 IPv6 寻址，IP 地址将是 8 个 4 字节字段类似于以下格式为 128 位值：\<标头 >:*nnnn:nnnn:nnnn:nnnn*。  
  
     如果有多个网络适配器，您将看到每个网络适配器都有一个 IP 地址。 如果仅选择此值，它将限制对该 IP 地址（以及域名服务器映射到该地址的任何主机名）的应用程序访问。 您不能使用 localhost 访问报表服务器，也不能使用安装在报表服务器计算机上的其他网络适配器的 IP 地址。  
  
 **端口**  
 指定报表服务器监视请求的端口。 端口 80 为默认端口。 如果使用端口 80，则不必将其包含在 URL 中。 如果使用其他任何端口号，你必须始终将其包含在 URL 中 (例如， http://localhost:8181/reports)。  
  
 **主机标头**  
 如果已有一个在域名服务器上定义的主机标头解析为您的计算机，则可以在为报表服务器访问配置的 URL 中指定该主机标头。  
  
 主机标头是允许多个网站共享一个 IP 地址和端口的唯一名称。 主机标头名称比 IP 地址和端口号更容易记住和键入。 这里有一个主机标头名称的示例：www.adventure-works.com。  
  
 **SSL 端口**  
 为 SSL 连接指定端口。 SSL 的默认端口为 443。  
  
 **SSL 证书**  
 指定安装在此计算机上的 SSL 证书的证书名称。 如果证书映射到某个通配符，则可以将其用于报表服务器连接。  
  
 指定为其注册证书的完全限定的计算机名称。 指定的名称必须与为其注册证书的名称相同。  
  
 必须先安装证书，才能使用此选项。 还必须修改 RSReportServer.config 文件中的 UrlRoot 配置设置，以便指定要为其注册证书的计算机的完全限定名称。 有关详细信息，请参阅 [联机丛书中的](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md) 配置本机模式报表服务器上的 SSL 连接 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
 **颁发给**  
 显示为其创建证书的计算机的名称。  
  
 **“添加”**  
 定义附加 URL。  
  
 **编辑**  
 修改 URL 语法的任何部分。  
  
 **删除**  
 从列表中清除 URL 项。  
  
## <a name="see-also"></a>请参阅  
 [Reporting Services 配置管理器&#40;本机模式&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)   
 [配置 URL（SSRS 配置管理器）](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)   
 [配置报表服务器 URL（SSRS 配置管理器）](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)  
  
  
