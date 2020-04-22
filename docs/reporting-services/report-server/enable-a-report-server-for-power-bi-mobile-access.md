---
title: 启用报表服务器以允许进行 Power BI 移动访问 | Microsoft Docs
ms.date: 12/17/2015
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
ms.assetid: c1a71522-394b-46a7-b9ec-f964bdd81d82
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 4dfeb99dc01a0ed2aaade9c0c21e4ce3ddd5da49
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2020
ms.locfileid: "81486741"
---
# <a name="enable-a-report-server-for-power-bi-mobile-access"></a>启用报表服务器以允许进行 Power BI 移动访问
可以通过 Power BI 移动应用来使用移动报表。 要将 Power BI 移动应用连接到 Reporting Services，需要进行一些配置。  
  
-   [移动报表需要 Reporting Services 本机模式](#nativemode)  
-   [启用 Reporting Services 的基本身份验证](#basicauth) （适用于 CTP 3.2）  
-   [建议启用 HTTPS 以及客户端设备的有效证书信任](#https)  
-   [查看防火墙设置](#firewall)  
  
<a name="nativemode"/> 

## <a name="reporting-services-native-mode-required"></a>需要 Reporting Services 本机模式  
移动报表是本机模式的一项功能。 它们在 SharePoint 集成模式下不可用。 Power BI 移动应用只适用于本机模式实例。  
  
<a name="basicauth"/>  

## <a name="enable-basic-authentication"></a>启用基本身份验证  
iOS Power BI 移动应用需要基本身份验证才能连接和使用移动报表。 默认情况下，Reporting Services 不会配置已启用的基本身份验证。 有关如何配置基本身份验证的信息，请参阅 [在报表服务器上配置基本身份验证](../../reporting-services/security/configure-windows-authentication-on-the-report-server.md)。  
  
还需要启用 Windows 身份验证以允许发布服务器应用发布移动报表。  
  
<a name="https"/>  

## <a name="enable-https"></a>启用 HTTPS  
如要启用基本身份验证，建议在 Reporting Services 中启用 HTTPS。 如果启用 HTTPS，请确保运行 iOS Power BI 移动应用的客户端设备信任使用的证书。 这意味着证书链需要有效且可用于客户端设备。  
  
如果需要使用自签名证书来进行开发或评估，可以从报表服务器中导出证书并将其安装到移动设备上。 请参阅有关如何在该设备上安装证书的设备文档。  
  
若要详细了解如何启用 TLS，请参阅[在本机模式报表服务器上配置 TLS 连接](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md)。  
  
<a name="firewall"/>
  
## <a name="review-firewall-settings"></a>查看防火墙设置  
建议查看防火墙设置，以确保所有设备都可以成功连接到 Reporting Services。   
  
有关如何配置 Windows 防火墙的详细信息，请参阅 [将防火墙配置为允许报表服务器访问](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)。  
  
## <a name="see-also"></a>另请参阅  
  
[在报表服务器上配置基本身份验证](../../reporting-services/security/configure-windows-authentication-on-the-report-server.md)  
[在本机模式报表服务器上配置 TLS 连接](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md)  
[将防火墙配置为允许报表服务器访问](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)  
  
  
  
  
  
  

