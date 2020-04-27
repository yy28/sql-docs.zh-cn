---
title: SQL Server 代理服务无法使用 SQL Server 身份验证 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- authentication [SQL Server Agent]
- SQL Server Authentication [SQL Server Agent]
ms.assetid: c39f3ec3-fc2c-4c12-940f-60d8d3d17660
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e16882247a123b32ba07fbbae0d1f3573fd2d678
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66092070"
---
# <a name="sql-server-agent-service-cannot-use-sql-server-authentication"></a>SQL Server Agent 服务不能使用 SQL Server 身份验证
  当 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理仅支持 Windows 身份验证。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理  
  
## <a name="description"></a>说明  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务只能通过使用 Windows 身份验证登录到数据库。 也就是说，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务帐户必须为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用户。  
  
 有关详细信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书中的“自动管理的安全性”和“实现 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理安全性”主题。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 代理升级问题](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)  
  
  
