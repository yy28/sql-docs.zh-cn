---
title: Microsoft SQL Server Reporting Services SharePoint 共享服务是已安装并排 （升级顾问） |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6ae1017e-129b-4702-9ea7-00ac9b024062
caps.latest.revision: 6
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: 79f07ede92ee840ed50631c10d22bf4b015cf29b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36018802"
---
# <a name="microsoft-sql-server-reporting-services-sharepoint-shared-service-is-installed-side-by-side-upgrade-advisor"></a>并行安装 Microsoft SQL Server Reporting Services SharePoint 共享服务（升级顾问）
  升级顾问检测到[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]与以前版本的并行安装 SharePoint 共享服务[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式。|  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Description  
 升级顾问检测到[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]与以前版本的并行安装 SharePoint 共享服务[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]，不基于 SharePoint 共享服务体系结构。 因为计算机同时并行安装了新旧两种 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 相关技术，所以阻止升级。  
  
## <a name="corrective-action"></a>纠正措施  
 若要继续升级，必须卸载现有 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安装之一。 删除 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安装之后，重新运行升级顾问以确认没有任何其他升级问题。  
  
  