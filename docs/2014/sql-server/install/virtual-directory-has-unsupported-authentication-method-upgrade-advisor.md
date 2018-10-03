---
title: 虚拟目录具有不受支持的身份验证方法 （升级顾问） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- virtual directories [Reporting Services]
ms.assetid: 216eca6f-9a66-42e1-aa54-dcf99cec9f7d
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: ca6cfaa5047ea16a4a8f4380fdf2cf150d0967d5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48119637"
---
# <a name="virtual-directory-has-unsupported-authentication-method-upgrade-advisor"></a>虚拟目录包含不支持的身份验证方法（升级顾问）
  升级顾问检测到报表管理器或报表服务器虚拟目录上存在不支持的身份验证方法。 升级不支持的身份验证方法包括匿名、摘要式和 .NET Passport 身份验证。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 本机模式。|  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Description  
 安装程序不能升级使用以下身份验证方法之一的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 系统  
  
-   匿名  
  
-   摘要  
  
-   .NET Passport  
  
 若要继续，可以修改在 Internet Information Services (IIS) 中为 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 虚拟目录指定的身份验证方法，也可以迁移您的安装。 有关迁移安装的详细信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书。  
  
## <a name="corrective-action"></a>纠正措施  
 若要继续升级，请在 IIS 中修改 ReportServer 和 Reports 虚拟目录的身份验证方法。 有关在 IIS 中修改身份验证方法的详细信息，请参阅 IIS 文档。 在修改 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 虚拟目录的身份验证方法之后，请重新运行升级顾问以确认没有其他升级问题。  
  
## <a name="see-also"></a>请参阅  
 [Reporting Services 升级问题&#40;升级顾问&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
