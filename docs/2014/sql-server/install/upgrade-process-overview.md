---
title: 升级过程概述 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- upgrading SQL Server
- Upgrade Advisor [SQL Server], process description
- SQL Server Upgrade Advisor, process description
- upgrade process [Upgrade Advisor]
ms.assetid: f77ffbab-a195-4124-acce-9c538f7ca9ce
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fb4bfb2073427d0f48b3d4a7ac7b7ab496299030
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66091522"
---
# <a name="upgrade-process-overview"></a>升级过程概述
  本主题提供了 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 升级顾问的最佳实践信息并概括介绍了升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的推荐过程。  
  
## <a name="upgrade-process"></a>升级过程  
 运行 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]、[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 或 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 的服务器可升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。 有些 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件可以就地升级，其他组件则必须迁移，并且仍然有一些其他组件已被新的组件取代。 例如，从 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 开始，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ([!INCLUDE[ssIS](../../includes/ssis-md.md)]) 便取代了 Data Transformation Services (DTS)，并且 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中不再支持 DTS。 当设计升级计划时，您可能需要计划将当前 DTS 包升级为 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 包。  
  
 利用升级顾问，可以对当前 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装、组件和相关文件进行评估，以便识别在升级或迁移到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的过程中及其后会导致问题的已知问题。 其中一些已知问题会阻止[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]升级。 在升级顾问的报表中，这些问题被标识为“阻止升级的问题”。 如果在运行安装程序前未解决阻止升级的问题，[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安装程序将退出并建议您运行升级顾问以找出妨碍升级的特定问题。  
  
 作为一种最佳做法，在升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 之前，我们建议您备份数据和系统设置，并且按照为组织机构定义的操作指南中概括的关键步骤进行操作。 使用以下步骤完成升级：  
  
1.  阅读 [Hardware and Software Requirements for Installing SQL Server 2014](hardware-and-software-requirements-for-installing-sql-server.md)。  
  
2.  备份数据和系统设置。  
  
3.  运行升级顾问。  
  
     升级顾问不修改计算机中的数据或更改计算机中的设置。  
  
4.  查看升级顾问报告中标识的问题。  
  
5.  解决任何妨碍您升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的问题。  
  
6.  解决所有其他升级前的问题。  
  
7.  运行升级顾问以确认所有已知问题均以解决。  
  
8.  运行 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安装程序。  
  
9. 解决所有升级后的问题和迁移问题。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;用户界面运行升级顾问&#41;](../../../2014/sql-server/install/running-upgrade-advisor-user-interface.md)   
 [使用报表](../../../2014/sql-server/install/using-reports.md)   
 [使用升级顾问](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
