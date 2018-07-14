---
title: 报表服务器 （升级顾问） 上检测到自定义报表项 |Microsoft Docs
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
- custom report items, upgrading
ms.assetid: aee32006-65b2-4dfe-9570-d85a249d17b2
caps.latest.revision: 14
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 2f7548a78ebbb4d7d01f8bfb9e796d32a9b3b28d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37261903"
---
# <a name="custom-report-items-were-detected-on-the-report-server-upgrade-advisor"></a>在报表服务器上检测到自定义报表项（升级顾问）
  早期版本创建的自定义报表项[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]都不符合[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。 可以继续升级，但使用该自定义报表项的报表将不会按预期运行。 升级顾问检测到了自定义报表项。 可以继续升级，但您必须在升级完成后，手动将自定义报表项文件移到新的安装文件夹。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 本机模式 | [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式。|  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Description  
 升级顾问在配置文件中检测到自定义 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 扩展插件设置，这指示安装中包含报表的一个或多个自定义程序集。  
  
## <a name="corrective-action"></a>纠正措施  
 在升级完成之后，手动将自定义报表项文件移到新的安装文件夹。  
  
## <a name="see-also"></a>请参阅  
 [Reporting Services 升级问题&#40;升级顾问&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
