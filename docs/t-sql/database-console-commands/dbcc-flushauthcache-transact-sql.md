---
title: DBCC FLUSHAUTHCACHE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DBCC FLUSHAUTHCACHE
- FLUSHAUTHCACHE
- DBCC_FLUSHAUTHCACHE_TSQL
- FLUSHAUTHCACHE_TSQL
helpviewer_keywords:
- DBCC FLUSHAUTHCACHE
ms.assetid: 681ef31d-ceb9-4da5-86bf-bf1240df950f
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 3cb7b06efe21d7dd6d4179c3454b6638ea636165
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33258702"
---
# <a name="dbcc-flushauthcache-transact-sql"></a>DBCC FLUSHAUTHCACHE (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

为 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 中当前用户数据库清空包含有关登录名和防火墙规则信息的数据库身份验证缓存。 此语句不适用于逻辑 master 数据库，因为 master 数据库包含有关登录名和防火墙规则信息的物理存储。 执行该语句的用户和当前连接的其他用户保持连接状态。 （[!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] 当前不支持 DBCC FLUSHAUTHCACHE。）
 
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
DBCC FLUSHAUTHCACHE [ ; ]  
```  
  
## <a name="arguments"></a>参数  
无。
  
## <a name="remarks"></a>Remarks  
身份验证缓存创建登录名和服务器防火墙规则（存储在 master 中）的副本并将它们放在用户数据库的内存中。  由于已包含数据库用户的信息已存储在用户数据库中，因此已包含数据库用户不是身份验证缓存的一部分。
与 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 持续保持活动连接需要至少每隔 10 小时进行重新授权（由 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 执行）。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 使用最初提交的密码尝试重新授权，且无需用户输入。 出于性能原因，在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 中重置密码时，连接将不会重新进行身份验证，即使该连接因连接池而重置。 这与本地 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的行为不同。 如果自最初授权连接时已更改密码，则必须终止连接，并使用新密码建立新连接。 具有 KILL DATABASE CONNECTION 权限的用户可使用 [KILL (Transact-SQL)](../../t-sql/language-elements/kill-transact-sql.md) 命令，显式终止与 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 的连接。
  
## <a name="permissions"></a>权限  
需要 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 管理员帐户。
  
## <a name="example"></a>示例  
以下语句会清除当前数据库的身份验证缓存。
  
```sql
DBCC FLUSHAUTHCACHE;  
```  
  
## <a name="see-also"></a>另请参阅  
[DBCC (Transact-SQL)](../../t-sql/database-console-commands/dbcc-transact-sql.md)
  
  
