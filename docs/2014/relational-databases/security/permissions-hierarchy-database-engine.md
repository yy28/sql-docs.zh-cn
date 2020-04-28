---
title: 权限层次结构（数据库引擎）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql12.swb.server.permissions.f1--May use common.permissions
helpviewer_keywords:
- security [SQL Server], denying access
- hierarchies [SQL Server], permissions
- securables [SQL Server]
- security [SQL Server], permissions
- permissions [SQL Server], hierarchy
- security [SQL Server], granting access
ms.assetid: f6d20a55-ef03-4e14-85f9-009902889866
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 607ac55fe426cd086ce31ade33d3e772e7a3d9a9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81487130"
---
# <a name="permissions-hierarchy-database-engine"></a>权限层次结构（数据库引擎）
  [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 管理着可以通过权限进行保护的实体的分层集合。 这些实体称为“安全对象”  。 最主要的安全对象是服务器和数据库，但可以在更细化的级别设置各种权限。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 通过验证主体是否已被授予适当权限来控制主体对安全对象的操作。

 下图显示了 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 权限层次结构之间的关系。

 ![数据库引擎权限层次结构图](../../database-engine/media/wj-security-layers.gif "数据库引擎权限层次结构图")

## <a name="chart-of-sql-server-permissions"></a>SQL Server 权限图表
 有关 pdf 格式的所有[!INCLUDE[ssDE](../../../includes/ssde-md.md)]权限的海报大小的图表，请[https://github.com/microsoft/sql-server-samples/blob/master/samples/features/security/permissions-posters/Microsoft_SQL_Server_2017_and_Azure_SQL_Database_permissions_infographic.pdf](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/security/permissions-posters/Microsoft_SQL_Server_2017_and_Azure_SQL_Database_permissions_infographic.pdf)参阅。

## <a name="working-with-permissions"></a>使用权限
 可以使用常见的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查询 GRANT、DENY 和 REVOKE 来操作权限。 有关权限的信息，可以在 [sys.server_permissions](/sql/relational-databases/system-catalog-views/sys-server-permissions-transact-sql) 和 [sys.database_permissions](/sql/relational-databases/system-catalog-views/sys-database-permissions-transact-sql) 目录视图中看到。 也可以使用内置函数来查询权限信息。

## <a name="see-also"></a>另请参阅
 [保护 SQL Server](securing-sql-server.md) [权限 &#40;数据库引擎&#41;](permissions-database-engine.md) [安全对象](securables.md)[主体 &#40;数据库引擎&#41;](authentication-access/principals-database-engine.md) [授予 &#40;transact-sql&#41;](/sql/t-sql/statements/grant-transact-sql) [REVOKE &#40;transact-sql&#41;](/sql/t-sql/statements/revoke-transact-sql) [DENY &#40;transact-sql&#41;](/sql/t-sql/statements/deny-transact-sql) [HAS_PERMS_BY_NAME](/sql/t-sql/functions/has-perms-by-name-transact-sql) [&#40;&#41;fn_builtin_permissions](/sql/relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql) &#40;transact-sql&#41;sys. server_permissions &#40;&#41;database_permissions transact-sql &#40;[的](/sql/relational-databases/system-catalog-views/sys-database-permissions-transact-sql) [&#41;。](/sql/relational-databases/system-catalog-views/sys-server-permissions-transact-sql)


