---
title: 报表服务器网站 （升级顾问） 上的客户端证书 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], upgrade issues
ms.assetid: 5ecce26b-99df-4109-8e51-d150d369dff7
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 808bb63a527e8c08063d934fd6a378e1955b7617
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48173397"
---
# <a name="client-certificates-on-the-report-server-web-site-upgrade-advisor"></a>报表服务器网站上的客户端证书（升级顾问）
  升级顾问已检测到承载报表服务器或报表管理器虚拟目录的 IIS 网站存在一个或多个客户端证书。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 本机模式。|  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Description  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 不支持使用客户端证书对用户进行身份验证。 可以继续升级，但升级后的报表服务器将不使用客户端证书。  
  
## <a name="corrective-action"></a>纠正措施  
 必须使用单独的解决方案（如 ISA Server）以确保满足任何客户端证书身份验证要求。  
  
## <a name="see-also"></a>请参阅  
 [Reporting Services 升级问题&#40;升级顾问&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
