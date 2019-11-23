---
title: 在 Report Server 上检测到自定义报表项（升级顾问） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- custom report items, upgrading
ms.assetid: aee32006-65b2-4dfe-9570-d85a249d17b2
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 5788b94356ec887b8c83850a4cb2c47d34b7388f
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952285"
---
# <a name="custom-report-items-were-detected-on-the-report-server-upgrade-advisor"></a>在报表服务器上检测到自定义报表项（升级顾问）
  为以前版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 创建的自定义报表项与 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]不兼容。 可以继续升级，但使用该自定义报表项的报表将不会按预期运行。 升级顾问检测到了自定义报表项。 可以继续升级，但您必须在升级完成后，手动将自定义报表项文件移到新的安装文件夹。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 本机模式 | [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式。|  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>描述  
 升级顾问在配置文件中检测到自定义 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 扩展插件设置，这指示安装中包含报表的一个或多个自定义程序集。  
  
## <a name="corrective-action"></a>纠正措施  
 在升级完成之后，手动将自定义报表项文件移到新的安装文件夹。  
  
## <a name="see-also"></a>另请参阅  
 [Reporting Services 升级问题&#40;升级顾问&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
