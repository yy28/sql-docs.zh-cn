---
title: 升级将 SQL Server 代理用户代理帐户更改为临时的 UpgradedProxyAccount |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- log shipping [SQL Server Agent]
ms.assetid: cd2d08c3-4e56-4034-8b68-0c78df8b5471
caps.latest.revision: 18
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 9bae867b97a9fc63b97506fd8900e68b670b8013
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36014933"
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
 [日志传送升级后将不会运行](../../../2014/sql-server/install/log-shipping-will-not-run-after-upgrading.md)  
  
  