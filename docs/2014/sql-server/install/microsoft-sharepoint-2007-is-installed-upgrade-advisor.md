---
title: 已安装 Microsoft SharePoint 2007 （升级顾问） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 6f1da295-d9b7-4948-99d3-ebd3587337c6
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 84672ddf6a9b2912f3d53eef8d40727369376ba5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "71952093"
---
# <a name="microsoft-sharepoint-2007-is-installed-upgrade-advisor"></a>安装 Microsoft SharePoint 2007（升级顾问）
  升级顾问检测到 SharePoint 产品或技术的不支持版本。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]SharePoint 模式。|  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>说明  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]不会在 SharePoint 2007 上升级或安装。 已阻止升级。  
  
## <a name="corrective-action"></a>纠正措施  
 若要继续升级，您必须卸载 SharePoint 2007 或将 SharePoint 2007 升级到 SharePoint 2010 产品。 更新 SharePoint 安装之后，重新运行升级顾问以确认没有任何其他升级问题。  
  
 不能直接从 SharePoint 2007 升级到 SharePoint 2013。 但你可以执行所谓的 "双跃点" 数据库连接，将其从 Office SharePoint Server 2007 升级到 SharePoint Server 2010，然后从 SharePoint Server 2010 升级到 SharePoint Server 2013。  
  
## <a name="see-also"></a>另请参阅  
 [升级顾问 &#40;Reporting Services 升级问题&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
