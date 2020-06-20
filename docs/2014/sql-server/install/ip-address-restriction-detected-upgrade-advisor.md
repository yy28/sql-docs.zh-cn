---
title: 检测到 IP 地址限制（升级顾问） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], upgrade issues
ms.assetid: 9a154455-c68f-4403-a3a7-b90f4d35eecb
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 2028e59e91d42bfdced2d18fa6ce129dfb108302
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85059236"
---
# <a name="ip-address-restriction-detected-upgrade-advisor"></a>检测到 IP 地址限制（升级顾问）
  升级顾问已检测到承载报表服务器或报表管理器虚拟目录的 IIS 网站上存在一个或多个 IP 地址限制。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 不为 IP 地址限制提供本机支持。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]本机.|  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>说明  
 安装程序不能针对升级后的报表服务器创建的 URL 定义 IP 地址限制。 升级可以继续，但不会针对 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] URL 定义 IP 地址限制。  
  
## <a name="corrective-action"></a>纠正措施  
 升级后，使用 ISA Server、防火墙软件或其他解决方案允许或排除从特定 IP 地址到报表服务器的请求。  
  
## <a name="see-also"></a>另请参阅  
 [升级顾问 &#40;Reporting Services 升级问题&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
