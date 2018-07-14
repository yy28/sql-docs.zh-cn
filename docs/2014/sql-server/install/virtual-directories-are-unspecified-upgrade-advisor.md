---
title: 未指定虚拟目录 （升级顾问） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- virtual directories [Reporting Services]
ms.assetid: 7d32b560-49d6-4558-b5d6-9127067f82d6
caps.latest.revision: 12
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: eba1359cc34a7b8e5fec19a71282d6b862b93102
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37265766"
---
# <a name="virtual-directories-are-unspecified-upgrade-advisor"></a>未指定虚拟目录（升级顾问）
  升级顾问检测不到报表服务器 Web 服务或报表管理器的虚拟目录设置。 升级完成后，你必须使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器为报表服务器配置 URL 预留。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 本机模式。|  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Description  
 升级 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安装包括为报表服务器 Web 服务和报表管理器保留新的 URL。 升级顾问检测不到要升级实例的报表服务器或报表管理器的虚拟目录，因此升级进程信息不足，无法为升级后的报表服务器创建 URL 预留。 升级可以继续，但在升级的安装后，报表服务器或报表管理器虚拟目录将是未定义的。  
  
## <a name="corrective-action"></a>纠正措施  
 升级完成后，请使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器为报表服务器和报表管理器设置 URL。 使用 IIS 管理器删除不再需要的所有虚拟目录。  
  
 有关详细信息，请参阅[配置 URL &#40;SSRS 配置管理器&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]联机丛书。  
  
## <a name="see-also"></a>请参阅  
 [Reporting Services 升级问题&#40;升级顾问&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
