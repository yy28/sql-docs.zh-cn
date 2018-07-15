---
title: SQL Server 代理服务不能使用 SQL Server 身份验证 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- authentication [SQL Server Agent]
- SQL Server Authentication [SQL Server Agent]
ms.assetid: c39f3ec3-fc2c-4c12-940f-60d8d3d17660
caps.latest.revision: 19
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 263f3e865a59b215ccbfc0382958dffe5cfb518e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37238257"
---
# <a name="sql-server-agent-service-cannot-use-sql-server-authentication"></a>SQL Server Agent 服务不能使用 SQL Server 身份验证
  当 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理仅支持 Windows 身份验证。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理  
  
## <a name="description"></a>Description  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务只能通过使用 Windows 身份验证登录到数据库。 也就是说，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务帐户必须为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用户。  
  
 有关详细信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书中的“自动管理的安全性”和“实现 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理安全性”主题。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 代理升级问题](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)  
  
  
