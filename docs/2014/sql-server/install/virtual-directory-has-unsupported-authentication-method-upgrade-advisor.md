---
title: 虚拟目录具有不受支持的身份验证方法（升级顾问） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- virtual directories [Reporting Services]
ms.assetid: 216eca6f-9a66-42e1-aa54-dcf99cec9f7d
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 26420df466860677f22d39d57133568a2f02bc68
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "71952010"
---
# <a name="virtual-directory-has-unsupported-authentication-method-upgrade-advisor"></a>虚拟目录包含不支持的身份验证方法（升级顾问）
  升级顾问检测到报表管理器或报表服务器虚拟目录上存在不支持的身份验证方法。 升级不支持的身份验证方法包括匿名、摘要式和 .NET Passport 身份验证。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]本机模式。|  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>说明  
 安装程序不能升级使用以下身份验证方法之一的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 系统  
  
-   匿名  
  
-   Digest  
  
-   .NET Passport  
  
 若要继续，可以修改在 Internet Information Services (IIS) 中为 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 虚拟目录指定的身份验证方法，也可以迁移您的安装。 有关迁移安装的详细信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书。  
  
## <a name="corrective-action"></a>纠正措施  
 若要继续升级，请在 IIS 中修改 ReportServer 和 Reports 虚拟目录的身份验证方法。 有关在 IIS 中修改身份验证方法的详细信息，请参阅 IIS 文档。 在修改 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 虚拟目录的身份验证方法之后，请重新运行升级顾问以确认没有其他升级问题。  
  
## <a name="see-also"></a>另请参阅  
 [升级顾问 &#40;Reporting Services 升级问题&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
