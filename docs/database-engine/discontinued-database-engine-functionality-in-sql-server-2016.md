---
title: SQL Server 2016 中弃用的数据库引擎功能 | Microsoft Docs
ms.custom: ''
ms.date: 02/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: release-landing
ms.topic: conceptual
helpviewer_keywords:
- VIA protocol
- unsupported features [SQL Server]
- SQL Mail
- discontinued functionality [SQL Server]
- RESTORE WITH DBO_ONLY
- BACKUP WITH PASSWORD
- user instances enabled
- BACKUP WITH MEDIAPASSWORD
- AWE
- SQL-DMO
- '*= and =*'
- 80 compatibility levels
- COMPUTE BY
- user instance timeout
- sp_dropalias
- COMPUTE
- WITH APPEND
- sys.database_principal_aliases
- sp_dboption
- DATABASEPROPERTY
- FASTFIRSTROW hint
- SET DISABLE_DEF_CNST_CHK
ms.assetid: d686cdf0-d11d-4dba-9ec8-de1a5f189f25
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: d9649b6c969a0b60b6d23ae3e44dc8c76bc37463
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66795044"
---
# <a name="discontinued-database-engine-functionality-in-sql-server-2016"></a>SQL Server 2016 中废止的数据库引擎功能
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  本主题介绍 [!INCLUDE[ssDE](../includes/ssde-md.md)] 中不再可用的 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]功能。  
  
## <a name="discontinued-features-in-includesssql15includessssql15-mdmd"></a>[!INCLUDE[ssSQL15](../includes/sssql15-md.md)]  
  
- [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] 是 64 位应用程序。 32 位安装已停止使用，不过，某些元素仍以 32 位组件运行。  
  
- 已不再使用兼容级别 90。 有关详细信息，请参阅 [ALTER DATABASE 兼容级别 (Transact-SQL)](../t-sql/statements/alter-database-transact-sql-compatibility-level.md)。  

- ActiveX 子系统已停止使用。 请改用命令行或 PowerShell 脚本。
  
## <a name="previous-versions"></a>先前版本  
  
- [SQL Server 2014 中废止的数据库引擎功能](http://docs.microsoft.com/sql/database-engine/discontinued-database-engine-functionality-in-sql-server-2016?view=sql-server-2014)

## <a name="see-also"></a>另请参阅  
 [SQL Server 2016 中不推荐使用的数据库引擎功能](../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)   
 [SQL Server 复制中不推荐使用的功能](../relational-databases/replication/deprecated-features-in-sql-server-replication.md)  
  
 
