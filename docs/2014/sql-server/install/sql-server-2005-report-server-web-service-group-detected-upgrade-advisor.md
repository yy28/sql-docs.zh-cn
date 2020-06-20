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
ms.openlocfilehash: 70be2b9c4e7abd55daaa752830a73cbe6e222659
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85054666"
---
# <a name="sql-server-2005-report-server-web-service-group-detected-upgrade-advisor"></a>检测到 SQL Server 2005 报表服务器 Web 服务组（升级顾问）
  升级顾问检测到该 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例与 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 报表服务器 Web 服务组关联。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]本机模式。|  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>说明  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]不 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 使用 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]报表服务器 Web 服务组。 从 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 时，将删除此服务组，并且在升级期间不保留此组的自定义访问控制列表 (ACL) 或属于此组的用户。  
  
## <a name="corrective-action"></a>纠正措施  
 在升级之前，请备份任何自定义 ACL 或属于 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 报表服务器 Web 服务组的用户。 为此，你可以在 sp2 和更高版本中使用**Icacls.exe**命令行工具， [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] 或在 Sp2 之前的 Windows 操作系统中使用 Cacls.exe 命令行工具 [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] 。 有关这些工具的语法的详细信息，请参阅 Windows 产品文档。 在安装程序成功完成之后，请对报表服务器实例的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 报表服务器 Windows 组应用自定义 ACL 或用户。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]报表服务器 Windows 组采用 SQLServerReportServerUser $ 的形式 \<*computer_name*> $ \<*instance_name*> 。  
  
## <a name="see-also"></a>另请参阅  
 [升级顾问 &#40;Reporting Services 升级问题&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
