---
title: 检测到 SQL Server 2005 报表服务器 Web 服务组（升级顾问） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- deployment [Reporting Services]
ms.assetid: 699d24eb-7756-4b41-9294-ef1a94b2f267
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: bfeff5eae569b481edfcc1cacc89c26e44edaece
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "71952376"
---
# <a name="sql-server-2005-report-server-web-service-group-detected-upgrade-advisor"></a>检测到 SQL Server 2005 报表服务器 Web 服务组（升级顾问）
  升级顾问检测到该[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例与[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]报表服务器 Web 服务组关联。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]本机模式。|  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>说明  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]不使用[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]报表服务器 Web 服务组。 从 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 时，将删除此服务组，并且在升级期间不保留此组的自定义访问控制列表 (ACL) 或属于此组的用户。  
  
## <a name="corrective-action"></a>纠正措施  
 在升级之前，请备份任何自定义 ACL 或属于 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 报表服务器 Web 服务组的用户。 为此，可以在[!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] sp2 和更高版本中使用[!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] **Icacls**命令行工具，或在 sp2 之前的 Windows 操作系统中使用 Cacls 命令行工具。 有关这些工具的语法的详细信息，请参阅 Windows 产品文档。 在安装程序成功完成之后，请对报表服务器实例的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 报表服务器 Windows 组应用自定义 ACL 或用户。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]报表服务器 Windows 组\<采用 SQLServerReportServerUser $*computer_name*>$\<*instance_name*> 形式。  
  
## <a name="see-also"></a>另请参阅  
 [升级顾问 &#40;Reporting Services 升级问题&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
