---
title: 回收 SQL Server 代理错误日志
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.errorlog.recyclesqlagenterrorlogs.f1
ms.assetid: 10bc2dd1-0505-4527-8ec7-d3b4e5d6352b
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 5c6079a5cab1972721fdac6c2d097fa6abb938ca
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "75247354"
---
# <a name="recycle-sql-server-agent-error-logs"></a>回收 SQL Server 代理错误日志
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL 数据库托管实例](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支持大多数但并非所有 SQL Server 代理功能。 有关详细信息，请参阅 [Azure SQL 数据库托管实例与 SQL Server 之间的 T-SQL 差异](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

使用此页，可以回收 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理错误日志。 回收该日志将关闭当前的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理错误日志并启动新的错误日志，而且不会重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务。 注意， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理保留九个最新的错误日志。 如果已经有九个错误日志，则回收错误日志会导致 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理删除最早的错误日志。  
  
## <a name="see-also"></a>另请参阅  
[SQL Server 代理错误日志](../../ssms/agent/sql-server-agent-error-log.md)  
  
