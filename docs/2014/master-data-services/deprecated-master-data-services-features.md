---
title: SQL Server 2014 中弃用的 Master Data Services 功能 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
ms.assetid: d8506bda-66dd-45a4-bfc9-3a10fa665acc
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 89d2d5d8cee989d6541cdb256b0a7aaf48d00162
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48142207"
---
# <a name="deprecated-master-data-services-features-in-sql-server-2014"></a>SQL Server 2014 中不推荐使用的 Master Data Services 功能
  本主题介绍 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 中仍然可用但不推荐使用的 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]功能。 按照计划， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]未来版本将不再具有这些功能。 在新的应用程序中不应使用这些不推荐使用的功能。  
  
## <a name="staging-process"></a>临时过程  
 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 中使用的临时过程在[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 应用程序将不再可用，但是仍可在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中使用。  
  
 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 临时过程的临时错误将不再显示在 UI 中。 在临时过程中填充的错误代码在临时表中仍然可用并可在此处找到： [ http://msdn.microsoft.com/library/ff487022.aspx ](http://msdn.microsoft.com/library/ff487022.aspx)。  
  
 临时表（tblStgMember、tblStgMemberAttribute 和 tblStgRelationship）在数据库中仍然可用。 用于启动临时过程的存储过程 (mdm.udpStagingSweep) 在数据库中仍然可用。  
  
 调用临时过程的 Web 服务方法仍然可用。  
  
 在 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]中设置的临时间隔适用于 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 和 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 中的临时过程。  
  
 已在 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 中实现性能更高的新临时过程。 有关详细信息，请参阅[数据导入 (Master Data Services)](overview-importing-data-from-tables-master-data-services.md)。  
  
## <a name="metadata"></a>元数据  
 尽管元数据模型仍显示在[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 应用程序中，但不应使用该模型。 未来的版本会将其删除。 用户也无法再查看中的元数据**资源管理器**功能区域中，并且您无法再创建元数据模型的版本。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 2014 中已停止使用的 Master Data Services 功能](discontinued-master-data-services-features.md)  
  
  
