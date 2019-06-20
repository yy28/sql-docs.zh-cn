---
title: 升级将 SQL Server 代理用户代理帐户更改为临时的 UpgradedProxyAccount |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server Agent]
ms.assetid: cd2d08c3-4e56-4034-8b68-0c78df8b5471
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a82cbcc9ef1ab57279b44cc83509cb1efad855ca
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66091403"
---
# <a name="upgrading-will-change-the-sql-server-agent-user-proxy-account-to-the-temporary-upgradedproxyaccount"></a>升级会将 SQL Server 代理用户的代理帐户更改为临时的 UpgradedProxyAccount
  启用了日志传送的数据库维护计划在升级后将不会启用。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理  
  
## <a name="description"></a>Description  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供了一组不直接与数据库维护计划兼容的新日志传送功能。  
  
## <a name="corrective-action"></a>纠正措施  
 具有包含日志传送功能的数据库维护计划的 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 用户应使用新的功能配置日志传送。 有关详细信息，请在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书中搜索“日志传送”。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 代理日志传送作业类别导致升级失败](../../../2014/sql-server/install/sql-server-agent-log-shipping-job-category-causes-upgrade-to-fail.md)   
 [升级后日志传送不会运行](../../../2014/sql-server/install/log-shipping-will-not-run-after-upgrading.md)  
  
  
