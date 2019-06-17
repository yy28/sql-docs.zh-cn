---
title: 安装 Microsoft SharePoint 2007 （升级顾问） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 6f1da295-d9b7-4948-99d3-ebd3587337c6
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 3487d84f95b559c115f9be6310b07dd4d0429fea
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66094029"
---
# <a name="microsoft-sharepoint-2007-is-installed-upgrade-advisor"></a>安装 Microsoft SharePoint 2007（升级顾问）
  升级顾问检测到 SharePoint 产品或技术的不支持版本。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式。|  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Description  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 无法升级或安装在 SharePoint 2007 上。 已阻止升级。  
  
## <a name="corrective-action"></a>纠正措施  
 若要继续升级，您必须卸载 SharePoint 2007 或将 SharePoint 2007 升级到 SharePoint 2010 产品。 更新 SharePoint 安装之后，重新运行升级顾问以确认没有任何其他升级问题。  
  
 不能直接从 SharePoint 2007 升级到 SharePoint 2013。 但可以做什么被称为"双跃点"数据库附加升级到 SharePoint Server 2010 Office SharePoint Server 2007 从，然后从 SharePoint Server 2010 部署到 SharePoint Server 2013。  
  
## <a name="see-also"></a>请参阅  
 [Reporting Services 升级问题&#40;升级顾问&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
