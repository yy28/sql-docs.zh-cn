---
title: "DBCC FLUSHAUTHCACHE (Transact SQL) |Microsoft 文档"
ms.custom:
- MSDN content
- MSDN - SQL DB
ms.date: 07/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3ba6a519ebcdbbc70bf19ec491539a3b07fb6c85
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-flushauthcache-transact-sql"></a>DBCC FLUSHAUTHCACHE (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

清空数据库身份验证缓存包含登录名和防火墙规则中的当前用户数据库有关的信息[!INCLUDE[ssSDS](../../includes/sssds-md.md)]。 此语句不适用于的逻辑 master 数据库，因为 master 数据库包含登录名和防火墙规则有关的信息的物理存储。 执行该语句的用户和其他当前连接的用户保持连接状态。 (有关当前不支持 DBCC FLUSHAUTHCACHE [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)]。)
 
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
DBCC FLUSHAUTHCACHE [ ; ]  
```  
  
## <a name="arguments"></a>参数  
无。
  
## <a name="remarks"></a>注释  
身份验证缓存创建登录名和服务器防火墙规则存储在 master 中并将它们放在用户数据库中的内存的副本。  由于包含的数据库用户的信息已存储在用户数据库，包含的数据库用户都不是身份验证缓存的一部分。
连续活动连接[!INCLUDE[ssSDS](../../includes/sssds-md.md)]需要重新授权 (由[!INCLUDE[ssDE](../../includes/ssde-md.md)]) 至少每隔 10 小时。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]尝试重新授权使用最初提交的密码和无用户输入是必需的。 出于性能原因，在重置密码时[!INCLUDE[ssSDS](../../includes/sssds-md.md)]，将不会对连接重新进行身份验证，即使该连接由于连接池而重置。 这是本地行为不同[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如果已更改了密码，因为最初授权连接，必须终止连接，并使用新密码建立新连接。 具有 KILL DATABASE CONNECTION 权限的用户可以显式终止与连接[!INCLUDE[ssSDS](../../includes/sssds-md.md)]使用[KILL &#40;Transact SQL &#41;](../../t-sql/language-elements/kill-transact-sql.md)命令。
  
## <a name="permissions"></a>Permissions  
需要[!INCLUDE[ssSDS](../../includes/sssds-md.md)]管理员帐户。
  
## <a name="example"></a>示例  
下面的语句清除当前数据库的身份验证缓存。
  
```sql
DBCC FLUSHAUTHCACHE;  
```  
  
## <a name="see-also"></a>另请参阅  
[DBCC (Transact-SQL)](../../t-sql/database-console-commands/dbcc-transact-sql.md)
  
  

