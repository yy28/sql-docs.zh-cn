---
title: 未检测到 IIS 向后兼容组件（升级顾问） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- IIS [Reporting Services]
ms.assetid: e794185a-0a77-480a-9aea-d09f8760a6b8
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b5557b86eb52416d77b46301be3601848079d2e0
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85042493"
---
# <a name="iis-backward-compatibility-components-were-not-detected-upgrade-advisor"></a>未检测到 IIS 向后兼容组件（升级顾问）
  升级顾问未检测到用于为安装程序提供所需信息以创建新 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] URL 的 IIS 组件和设置。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]本机模式。|  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>说明  
 IIS 包括了可提供报表服务器和报表管理器虚拟目录相关信息的组件，而这些组件未安装在报表服务器计算机上。 升级可继续进行，但升级操作不会重新创建报表服务器或报表管理器的 URL。  
  
## <a name="corrective-action"></a>纠正措施  
 升级完成后，请使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置工具为报表服务器或报表管理器设置 URL。 使用 IIS 管理器删除不再需要的虚拟目录。  
  
 有关详细信息，请参阅联机丛书中[的配置 URL &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="see-also"></a>另请参阅  
 [升级顾问 &#40;Reporting Services 升级问题&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
