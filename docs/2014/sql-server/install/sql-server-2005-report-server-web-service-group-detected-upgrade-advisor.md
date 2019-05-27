---
title: 检测到的 SQL Server 2005 报表服务器 Web 服务组 （升级顾问） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- deployment [Reporting Services]
ms.assetid: 699d24eb-7756-4b41-9294-ef1a94b2f267
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 4f379675a4d7b37b9eab69598f7c04bc57306d46
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66092112"
---
# <a name="sql-server-2005-report-server-web-service-group-detected-upgrade-advisor"></a>检测到 SQL Server 2005 报表服务器 Web 服务组（升级顾问）
  升级顾问检测到的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]与实例相关联[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]报表服务器 Web 服务组。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 本机模式。|  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Description  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 不使用[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]报表服务器 Web 服务组。 从 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 时，将删除此服务组，并且在升级期间不保留此组的自定义访问控制列表 (ACL) 或属于此组的用户。  
  
## <a name="corrective-action"></a>纠正措施  
 在升级之前，请备份任何自定义 ACL 或属于 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 报表服务器 Web 服务组的用户。 若要执行此操作，可以使用**Icacls.exe**中的命令行工具[!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)]SP2 及更高版本或之前的 Windows 操作系统中的 Cacls.exe 命令行工具[!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)]SP2。 有关这些工具的语法的详细信息，请参阅 Windows 产品文档。 在安装程序成功完成之后，请对报表服务器实例的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 报表服务器 Windows 组应用自定义 ACL 或用户。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]报表服务器 Windows 组采用 SQLServerReportServerUser$\<*computer_name*>$\<*instance_name*>。  
  
## <a name="see-also"></a>请参阅  
 [Reporting Services 升级问题&#40;升级顾问&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
