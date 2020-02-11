---
title: 未指定虚拟目录（升级顾问） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- virtual directories [Reporting Services]
ms.assetid: 7d32b560-49d6-4558-b5d6-9127067f82d6
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: c9ee7f745fc683a9ed93f2ca09ac94e1bf580f71
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "71952382"
---
# <a name="virtual-directories-are-unspecified-upgrade-advisor"></a>未指定虚拟目录（升级顾问）
  升级顾问检测不到报表服务器 Web 服务或报表管理器的虚拟目录设置。 升级完成后，你必须使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器为报表服务器配置 URL 预留。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]本机模式。|  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>说明  
 升级 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安装包括为报表服务器 Web 服务和报表管理器保留新的 URL。 升级顾问检测不到要升级实例的报表服务器或报表管理器的虚拟目录，因此升级进程信息不足，无法为升级后的报表服务器创建 URL 预留。 升级可以继续，但在升级的安装后，报表服务器或报表管理器虚拟目录将是未定义的。  
  
## <a name="corrective-action"></a>纠正措施  
 升级完成后，请使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器为报表服务器和报表管理器设置 URL。 使用 IIS 管理器删除不再需要的所有虚拟目录。  
  
 有关详细信息，请参阅联机丛书中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [的配置 URL &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md) 。  
  
## <a name="see-also"></a>另请参阅  
 [升级顾问 &#40;Reporting Services 升级问题&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
