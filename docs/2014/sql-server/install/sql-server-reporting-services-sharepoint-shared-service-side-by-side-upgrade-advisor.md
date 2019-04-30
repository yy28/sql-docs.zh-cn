---
title: Microsoft SQL Server Reporting Services SharePoint 共享服务是已安装并排显示 （升级顾问） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 6ae1017e-129b-4702-9ea7-00ac9b024062
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 93bbc8ca6c2a67ec2ec224db51c780a38534c098
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63267912"
---
# <a name="microsoft-sql-server-reporting-services-sharepoint-shared-service-is-installed-side-by-side-upgrade-advisor"></a>并行安装 Microsoft SQL Server Reporting Services SharePoint 共享服务（升级顾问）
  升级顾问检测到[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]与早期版本的并行安装 SharePoint 共享服务[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式。|  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Description  
 升级顾问检测到[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 共享服务安装与以前版本的并行[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]的不基于 SharePoint 共享服务体系结构。 因为计算机同时并行安装了新旧两种 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 相关技术，所以阻止升级。  
  
## <a name="corrective-action"></a>纠正措施  
 若要继续升级，必须卸载现有 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安装之一。 删除 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安装之后，重新运行升级顾问以确认没有任何其他升级问题。  
  
  
