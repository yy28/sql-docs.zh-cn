---
title: Microsoft SQL Server Reporting Services SharePoint 共享服务并行安装（升级顾问） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 6ae1017e-129b-4702-9ea7-00ac9b024062
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b8a26fedd892dfb26dea4616efd46d3b3748b508
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85035992"
---
# <a name="microsoft-sql-server-reporting-services-sharepoint-shared-service-is-installed-side-by-side-upgrade-advisor"></a>并行安装 Microsoft SQL Server Reporting Services SharePoint 共享服务（升级顾问）
  升级顾问检测到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 共享服务与以前版本的并行安装 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]SharePoint 模式。|  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>说明  
 升级顾问检测到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] sharepoint 共享服务与以前版本的并行安装 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ，该版本不基于 SharePoint 共享服务体系结构。 因为计算机同时并行安装了新旧两种 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 相关技术，所以阻止升级。  
  
## <a name="corrective-action"></a>纠正措施  
 若要继续升级，必须卸载现有 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安装之一。 删除 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安装之后，重新运行升级顾问以确认没有任何其他升级问题。  
  
  
