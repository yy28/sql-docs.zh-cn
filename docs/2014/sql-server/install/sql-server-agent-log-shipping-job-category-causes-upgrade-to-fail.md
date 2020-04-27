---
title: SQL Server 代理日志传送作业类别导致升级失败 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server Agent]
- job categories [SQL Server Agent]
ms.assetid: ef05ce53-c6ce-42ec-9df8-46c951626424
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7145d846657613b50706ebe75c9832f40f49383e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66092043"
---
# <a name="sql-server-agent-log-shipping-job-category-causes-upgrade-to-fail"></a>SQL Server 代理的日志传送作业类别导致升级失败
  如果存在名为“日志传送”的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业类别，升级过程将失败。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理  
  
## <a name="description"></a>说明  
 存在名为“日志传送”的系统作业类别。 如果要进行升级的安装已包含用户创建的名为“日志传送”的作业类别，则必须先重命名该作业类别，然后才可进行升级；否则，升级过程将失败。  
  
## <a name="see-also"></a>另请参阅  
 [日志传送在升级后将不运行](../../../2014/sql-server/install/log-shipping-will-not-run-after-upgrading.md)   
 [升级会将 SQL Server 代理用户代理帐户更改为临时 UpgradedProxyAccount](../../../2014/sql-server/install/upgrading-changes-sql-server-agent-user-proxy-account-to-temporary-account.md)   
 [SQL Server 代理升级问题](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)  
  
  
